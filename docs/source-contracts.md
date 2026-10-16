# Selected source contracts

Read the [architecture guide](source-architecture.md) and
[coverage statement](source-coverage.md) first. Assertions below are based on
source bodies at
[`0ec192ded6c4d3bc577abd643872a27a423053d2`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2).
They describe selected contracts, not complete package/member coverage or
executed behavioral verification. Test links identify relevant tracked files;
their bodies and outcomes have not all been reviewed.

## Database session and transaction ownership

Source: [models/db/context.go](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/models/db/context.go).

`GetEngine(ctx)` returns an engine carried by the context when present, otherwise
it obtains a contextual session from the global XORM engine. Pass the callback's
context to participating model operations; replacing it with a fresh background
context loses this transaction association.

`WithTx(parentCtx, func(context.Context) error) error` has two paths:

1. With an existing transaction, it reuses that session. A callback error closes
   the session immediately, even if a caller later ignores the error
2. Without one, it creates a session, defers `Close`, begins the transaction,
   invokes the callback, and commits only after a nil callback error

Consequently, nested `WithTx` is not an independent savepoint transaction.
`WithTx2[T]` carries a value alongside the same error/transaction behavior; callers
must still check its returned error before using the result as committed data.

The older `TxContext` returns a `Committer`. Always close it on exit and call
`Commit` on success, including when no data changed. When reusing a transaction,
the returned half-committer's `Commit` only records local success; the outer owner
commits later. Closing it without that success mark closes the parent's session.
This can roll back work from callers higher in the stack.

`Get[T]` and `GetByID[T]` distinguish absence (`nil, false, nil`) from a query
error. `Get`, `Exist`, and `Delete` reject invalid conditions with a panic in the
specified cases; they do not convert programmer mistakes into an empty query
result. `DeleteByIDs` returns without work for an empty ID list. The development
session-safety check also guards against reusing a session context inside XORM
iteration; the source disables that check for non-test production operation.

Relevant tests: [context tests](../models/db/context_test.go),
[committer tests](../models/db/context_committer_test.go). No new claim of
cross-database equivalence or concurrent session safety follows from this review.

## Model operations are not an authorization boundary by themselves

Source: [models/issues/assignees.go](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/models/issues/assignees.go).

`GetAssigneeIDsByIssue` selects distinct assignee IDs without joining the user
table. Its source explicitly leaves any required permission checks to the caller.
An association result is not proof that the current requester may view or edit
that user or issue.

`ToggleIssueAssignee` wraps the association change and creation of its comment in
`db.WithTx`. It returns the removed flag and comment only after the wrapper
succeeds; on error it returns `false, nil, err`. This is a concrete transaction
participant, not evidence that every service side effect uses the same database
transaction. See [assignee tests](../models/issues/assignees_test.go).

## Repository model state and lookup errors

Source: [models/repo/repo.go](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/models/repo/repo.go).

`Repository` persists owner/name, status, visibility, fork/template references,
counts, and other application metadata. Some related fields are excluded from
XORM storage and loaded lazily. `AfterLoad` derives open counts from totals and
closed counts and fills a missing wiki branch from configuration. `LoadOwner`
mutates the model's cached owner pointer. `MustOwner` returns an error-display
placeholder user when loading fails, so a non-nil result is not proof of a real
persisted owner.

`IsUsableRepoName` returns an **error**, with nil meaning usable; its existing
comment describes a boolean but the signature/body do not. It rejects invalid
characters and repeated dots before consulting reserved names/patterns.
`IsValidSSHAccessRepoName` is a boolean check with the wiki-name exception. Neither
name validation nor `IsOwnedBy` is a complete requester permission check.

`GetRepositoryByID` and the name-based lookup helpers return a typed
`ErrRepoNotExist` on absence, unlike generic `db.Get`'s separate existence flag.
`ErrRepoNotExist.Unwrap` exposes `util.ErrNotExist`, while `IsErrRepoNotExist`
uses a direct type assertion at this revision. Do not assume that specific helper
recognizes every wrapped error. `MarkAsBrokenEmpty` changes the in-memory status
and empty flag together; the helper itself does not persist a database update.
See [repository tests](../models/repo/repo_test.go).

## Repository identity, paths, and managed locks

Sources: [repository facade](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/modules/git/gitrepo/gitrepo.go),
[Git initialization/locks](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/modules/git/git.go),
and [global-lock wrappers](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/modules/globallock/globallock.go).

`RepositoryFacade` provides a managed identity, location, and log representation.
It is not an open repository handle and does not itself perform authorization.
`RepositoryManaged(id, loc)` records the supplied identity and cleaned location.
`RepositoryUnmanaged(loc)` represents temporary or not-yet-managed repositories;
calling its `GitRepoManagedID` panics. Do not pass an unmanaged facade to an API
that needs a managed lock/cache key.

`RepoLocalPath` returns an absolute location unchanged. For a relative location,
it requires initialized `setting.RepoRootPath` and concatenates the root and
slash-converted location, relying on the facade's cleaned-path precondition.
This is path construction, not a path-traversal/security validator.
`RepoLocalFS` wraps the resulting directory with `os.DirFS`.

`LockConfigAndDo` uses a `repo-config:` key; `LockWriteAndDo` uses a separate
`repo-write:` key, each followed by the managed ID. One lock class must not be
assumed to exclude the other. `globallock.LockAndDo` acquires through the default
locker, returns acquisition errors without invoking the callback, and defers
release around the callback. `TryLockAndDo` returns whether acquisition succeeded
separately from an error or the callback result.

The default locker is initialized lazily using a mutex and atomic pointer;
configuration selects Redis or the memory implementation. The wrappers alone
do not establish lease duration, renewal, fairness, crash recovery, or a
distributed-transaction guarantee. Those require the specific locker bodies.
Relevant tracked tests: [global locks](../modules/globallock/globallock_test.go)
and [locker tests](../modules/globallock/locker_test.go).

## Git initialization is stateful

`InitSimple` requires a nonempty Git home path, configures the executable,
detects version features, and checks compatibility. It does not synchronize the
Git configuration, but it can set `GNUPGHOME` when absent. “Simple” does not mean
pure or free of process-global effects.

At this source revision the minimum checked Git version is `2.25.0`; `2.43.1`
has an explicit compatibility rejection. Feature flags have separate thresholds:
for example SHA-256 support requires at least `2.42` and the non-gogit path.
Do not infer all feature availability from the minimum version alone.

`InitFull` calls `InitSimple` and then synchronizes Git configuration. Its source
requires initialization once at process startup because it makes unsynchronized
global changes. The lazy fallback in `DefaultFeatures` is not evidence that
initialization is safe to race. [git_test.go](../modules/git/git_test.go) is the
nearby test entry, not an executed validation result.

## Git pipeline inputs, cancellation, and stream ownership

Sources: [gitcmd/context.go](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/modules/git/gitcmd/context.go)
and [pipeline/catfile.go](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/modules/git/pipeline/catfile.go).

`gitcmd.Context` extends `context.Context` with `CancelPipeline(error) error`.
Its implementation cancels the command context with a pipeline-specific error
wrapper and returns the supplied error. This preserves a distinction between
pipeline cancellation and parent-context cancellation; the command execution
and pipe-cleanup implementations still need separate review.

`CatFileBatch`, `CatFileBatchCheck`, and `CatFileBatchCheckAllObjects` add the
corresponding Git arguments to the supplied command, attach the repository, and
execute with stderr handling. They mutate the supplied command builder; do not
treat the argument as an immutable value.

`BlobsLessThan1024FromCatFileBatchCheck(in, out)` owns closing `out` via a deferred
call but does not close `in`. It scans lines, ignores empty/non-blob/missing-field
records, writes accepted object IDs followed by a newline, and returns write or
scanner errors. The implementation skips sizes **greater than 1024**, so it
includes exactly 1024 despite the helper's name/comment. It ignores numeric
conversion errors; callers must supply well-formed `git cat-file --batch-check`
output rather than treating this as a strict untrusted-input validator. The
deferred output-close error is not returned.

## Credential parsing and persisted access tokens

Sources: [HTTP authorization parser](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/modules/auth/httpauth/httpauth.go)
and [access-token model](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/models/auth/access_token.go).

`ParseAuthorizationHeader` requires two whitespace-separated fields. It accepts
case-insensitive Basic, token, and Bearer schemes. Basic decoding must succeed
and contain a colon; the first colon splits username and password. The boolean
reports syntactic recognition, not successful authentication or permission.

`AccessToken.Token` is excluded from XORM persistence; the model stores a hash,
salt, last-eight-byte suffix, owner, and scope. Token creation generates a value and
inserts the model. Regeneration selects by both token ID and owner ID and updates
the hash/salt/suffix while keeping the name and scope.

`GetAccessTokenBySHA` rejects values shorter than eight bytes. On a cache hit
it reloads the database row and checks the stored hash against the cached hash;
deleted or regenerated tokens invalidate that entry. On a miss it selects by
suffix and checks candidate hashes using the constant-time equality helper.
The suffix is a lookup aid, not an authentication result. Hash implementation and
complete request authentication/authorization remain distinct contracts.

Relevant tests: [HTTP header parser](../modules/auth/httpauth/httpauth_test.go)
and [access-token tests](../models/auth/access_token_test.go).

## Outbound policy checks and proxy trust

Source: [modules/egress/policy/policy.go](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/modules/egress/policy/policy.go).

`CheckHost` pre-screens a URL host; `CheckHostIPs` resolves addresses and requires
each returned address to pass, falling back to the host screen when none are
returned. `NewDialContext` installs an address check in the network dialer's
control callback, so a successful pre-screen alone is not the final connection
check. The policy evaluates blocked entries before allow behavior; strict mode
requires an allow match. `WithLocalNeedsIPAllow` requires an IP-based allow match
for restricted local addresses rather than accepting a hostname allow entry.

The dial callback wraps policy rejections with `ErrDenied`. Pre-screen methods
return their check errors directly, so callers should not assume every entry
point produces that same wrapped sentinel. Connection failures remain distinct.

`NewHTTPTransport` uses the policy's proxy selector and dial function together.
The selector records the chosen supported proxy dial address; that dial path can
exempt recorded proxy addresses from the target lists. Operator-selected proxies
therefore form a trust boundary. The existence of this policy type does not prove
that every outbound client in the application uses it. The policy's match-list
implementation, integration call sites, and [tests](../modules/egress/policy/policy_test.go)
need review before making an application-wide security claim.

## Password-hash compatibility and registration

Source: [modules/auth/password/hash/hash.go](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/modules/auth/password/hash/hash.go).

`PasswordHashAlgorithm.Hash` accepts a historical ten-byte salt directly and
otherwise hex-decodes the supplied salt, returning a decoding error if invalid.
`VerifyPassword` delegates to an algorithm-specific verifier when available;
otherwise it hashes and uses `subtle.ConstantTimeCompare`. A hash error is logged
and verification returns false.

`Parse` preserves historical stored algorithm specifications: an empty stored
specification becomes the legacy `pbkdf2` specification. It does not perform
configuration alias expansion, and an unknown/invalid factory result returns
nil. Do not equate a stored `pbkdf2` value with the current configured default
algorithm. `Register` returns an error for a duplicate name; `MustRegister`
panics on that error. Both registration functions are explicitly not thread-safe,
even though the last non-default parsed algorithm is cached atomically.
See [hash tests](../modules/auth/password/hash/hash_test.go).

## Migration version and failure boundaries

Sources: [migration coordinator](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/modelmigration/migrations.go)
and [database migration helpers](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/modelmigration/base/db.go).

`EnsureUpToDate` distinguishes uninitialized, too-old, and mismatched database
versions. `Migrate` synchronizes the version table, records the expected version
for a fresh installation, rejects unsupported old/newer-database states, and
initializes Git before pending migrations. It resets the mapper between tasks,
runs each task, and updates the stored version after that task succeeds. A task
error is wrapped with its migration ID and description.

This per-task sequence is not a single atomic transaction covering the whole
upgrade. Read each migration's schema and transaction operations before changing
it. `RecreateTable(s)` requires full bean definitions; the source warns callers
to commit the session, and `ModifyColumn` does not support SQLite. Historical
version directories must remain ordered evidence, not be treated as interchangeable
implementations to deduplicate.

Relevant tests: [migration coordinator](../modelmigration/migrations_test.go),
[base helpers](../modelmigration/base/db_test.go), and the per-version test files
listed in the [catalogue](package-catalog.md).

## Code-indexer lifecycle and failure policy

Source: [modules/indexer/code/indexer.go](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/modules/indexer/code/indexer.go).

The global indexer pointer starts with a dummy indexer. `Init` consults indexer
settings, creates a managed process context and termination callback, selects
Bleve or Elasticsearch, and creates a unique worker queue. Initialization runs
asynchronously; after a real indexer is installed, queue processing starts and a
new index is populated from existing repository IDs. An optional startup timeout
can cancel and close the indexer and log a fatal error.

For an item, the indexing path loads repository metadata, deletes index entries
for a missing repository, filters repository categories, opens/reuses a Git
repository with a deferred closer, computes changes, indexes, and only then
updates its recorded indexed revision. The handler logs item errors and returns
nil unhandled items deliberately: failures are **not requeued by this handler**.
Do not promise automatic retries or immediate search visibility after a push.

`UpdateRepoIndexer` enqueues a repository ID and logs enqueue failure. `IsAvailable`
pings the current code indexer; a successful ping is not proof that every
repository is indexed. Initial population deletes old index-status metadata and
works backward from a maximum repository ID captured for that pass.

Relevant tests: [code indexer](../modules/indexer/code/indexer_test.go) and
[Bleve implementation](../modules/indexer/code/bleve/bleve_test.go). Queue capacity,
full backend semantics, cancellation races, and runtime recovery are not verified
here.
