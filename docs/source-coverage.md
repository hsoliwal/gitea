# Source documentation coverage and remaining work

[Architecture](source-architecture.md) · [Package catalogue](package-catalog.md) ·
[Selected contracts](source-contracts.md) · [Tree/frontend map](source-tree.md)

## Baseline and meaning of coverage

The source baseline is
[`0ec192ded6c4d3bc577abd643872a27a423053d2`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2).
The complete Git tree was enumerated, and root contribution/agent instructions,
the root Go/npm/Python manifests, pnpm configuration, Makefile, Vite configuration,
existing development guides, and 125 representative Go source bodies were read.
This is a documentation-only, static-source pass.

Inventory completeness and semantic completeness are different:

- Every tracked Go-containing directory is listed, including tests, tools,
  placeholders, generated-source candidates, and build-tagged code
- A partial source review explains an inspected representative file or selected
  contracts; it does not account for every public symbol, caller, build variant,
  error, resource, or side effect in that package
- An inventory-only entry has a verified path/count but an unread implementation
- Reviewed-complete requires substantive package/member coverage, reconciled
  callers/tests, navigation, and applicable verification. No whole package is
  marked reviewed-complete in this pass

## Accounting by level

| Level | Discovered / included | Partial source documentation | Inventory only / still unread | Reviewed-complete |
| --- | ---: | ---: | ---: | ---: |
| Repository | 1 / 1 | 1 | 0 | 0 |
| Root Go module | 1 / 1 | 1 | 0 | 0 |
| Manifest-based toolchain/project boundaries | 4 / 4 | 3 root boundaries | 1 contributed Jsonnet project | 0 |
| Go-containing source directories | 387 / 387 | 125 | 262 | 0 |
| Frontend JS/TS/Vue file candidates | 246 / 246 | 0 member reviews | 246 | 0 |

The four toolchain/project boundaries are Go, frontend/JavaScript tooling,
Python development tooling, and the contributed monitoring mixin. Docker, Snap,
Nix, BSD make, and service configuration entry points are also tracked in the
[tree map](source-tree.md#contributed-and-packaging-boundaries); their detailed
packaging/support contracts remain unread. These categories overlap by design
and must not be added into one “project coverage” percentage. A Python dev-tool
manifest, a Go package, an ESM file, and a deployable application are different
entities.

No ordinary package was excluded. The physical Go-directory accounting is
387/387; substantive complete-package coverage is 0/387. Build-active package
sets, external `_test` declarations, every member, and import-graph reachability
have not been resolved. A complete semantic module/member denominator remains
unknown. This prevents any overall “every package/module documented” claim.

### Go-family progress

| Family | Directories | Partial representative reviews | Inventory only |
| --- | ---: | ---: | ---: |
| Executable root | 1 | 1 | 0 |
| build | 2 | 2 | 0 |
| cmd | 2 | 2 | 0 |
| modelmigration | 26 | 26 | 0 |
| models | 41 | 41 | 0 |
| modules | 167 | 53 | 114 |
| routers | 73 | 0 | 73 |
| services | 70 | 0 | 70 |
| tests | 4 | 0 | 4 |
| tools | 1 | 0 | 1 |
| Total | 387 | 125 | 262 |

## Remaining contract review

1. Trace the HTTP lifecycle from `cmd/web.go` and `routers/init.go` through
   middleware, `services/context`, route registration, authentication and
   authorization, handlers, responses, and cleanup. The directory map alone
   cannot establish this ordering
2. Trace repository creation/mutation/deletion through services, model
   transactions, Git handles/commands, filesystem state, notifications, and
   background work. Establish what is atomic, retryable, or caller-owned
3. Read `modules/setting` initialization and each option family before describing
   precedence, defaults, validation, reloadability, or secret handling
4. Review the remaining 262 representative sources, then all relevant files and
   build variants in each package. Reconcile representative summaries with the
   full exported API and callers instead of treating the first file as coverage
5. Review queue/process/graceful/storage lifecycles, exact error classification,
   locking implementations, shutdown behavior, and race-sensitive interactions
6. Inspect frontend entry/component/worker bodies and their imports, exports,
   browser side effects, ownership, protocol, and test expectations
7. Read the contributed monitoring and packaging manifests, generated-source
   headers, and generators before assigning supported build outputs or custody
8. Reconcile inline package/member comments, examples, and signatures with the
   selected contracts. Inline source comments were not changed in this
   Markdown-only pass
9. Read and, in a separately authorized execution pass, run relevant tests and
   documentation checks against the resulting revision. Complete the external
   test/build-variant inventory and record real outcomes

The catalogue keeps each unread directory visible. The selected contracts also
retain non-obvious distinctions found in source: a no-op historical migration,
the database paginator placeholder, nested transaction ownership, distinct Git
lock classes, the batch-check size boundary, and the code-indexer's no-requeue
policy. Such observations are not an audit finding or a request to change code.

## Verification scope

The inventory is derived from a non-truncated Git tree; source statements cite
the pinned revision. Navigation and counts can be checked from that tree without
running repository code. This pass does not install dependencies, execute
generators or scripts from the repository, compile, run a server, run tests, or
change source comments, build definitions, CI, or licenses.

| Check | Status and limitation |
| --- | --- |
| Complete tracked-path enumeration | Observed: 7,756 entries, 6,359 blobs, 1,397 trees; response not truncated |
| Representative source review | Partial: 125 complete files; package/member coverage remains incomplete |
| Build manifests and commands | Read-only review; declared commands are instructions, not execution receipts |
| Markdown linter | Not run; requires the repository's dependency/tooling environment |
| Compile/type-check | Not run |
| Unit/integration/migration/browser tests | Not run |
| Runtime/security/performance evaluation | Not run |

The Makefile's Markdown target covers only root `*.md` files. In an authorized
environment with dependencies already available, explicitly include nested docs,
for example `pnpm exec markdownlint docs/source-architecture.md docs/source-contracts.md docs/package-catalog.md docs/source-tree.md docs/source-coverage.md`.
Review source links, table contents, anchors, and the exact diff as separate checks.
Running Markdown lint would not establish compilation, security, or behavioral
correctness. Opening a documentation PR is also not a CI pass or merge.
