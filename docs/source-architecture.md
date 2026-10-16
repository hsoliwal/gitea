# Source architecture and coverage

This is a reading guide for the hsoliwal fork, pinned to
[`0ec192ded6c4d3bc577abd643872a27a423053d2`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2).
It describes inspected source and manifests, not a release certification. The M3
direction in the [README](../README.md) is a programme goal; it does not establish
an M3 runtime, Java integration, immutable storage, or performance improvements
inside this Go application.

## Read by task

- [Package catalogue](package-catalog.md): every tracked directory containing Go
  source, representative declarations where inspected, and remaining coverage
- [Selected contracts](source-contracts.md): transactions, repository identities,
  Git locks and pipelines, token lookup, migrations, and indexing
- [Tree and frontend map](source-tree.md): tracked scope, build inputs and outputs,
  frontend source units, fixtures, generated assets, and dependency custody
- [Coverage and verification](source-coverage.md): what was reviewed, what remains,
  and why a file inventory is not complete API documentation
- [Development](development.md), [build setup](build-setup.md),
  [build options](build-source.md), and [testing](testing.md): operational instructions

## Manifest-backed boundaries

The pinned tracked tree contains one `go.mod`, one `package.json`, and one
`pyproject.toml`, all at the repository root. These establish three toolchain
boundaries around one Gitea application; they do not establish three separately
deployed services or one project per directory.

| Boundary | Evidence and responsibility | Inputs, outputs, and consumers |
| --- | --- | --- |
| Go application and libraries | [go.mod](../go.mod) declares module `gitea.dev`, Go `1.27`, and toolchain `go1.27.1` | [main.go](../main.go) is the executable entry; Go packages supply CLI, HTTP handlers, services, persistence, migrations, and utility functions; `make backend` produces the executable |
| Frontend and JavaScript tooling | [package.json](../package.json) sets ESM mode, `pnpm@12.6.0`, Node `>= 22.18.0`, and pnpm `>= 11.0.0` | TypeScript, Vue, CSS, and SVG sources feed Vite and other tools; [vite.config.ts](../vite.config.ts) writes assets under `public/assets` |
| Python development tools | [pyproject.toml](../pyproject.toml) declares `gitea` version `0.0.0`, Python `>=3.10`, and a `dev` group | `djlint`, `yamllint`, and `zizmor` support lint targets through `uv`; this manifest is not evidence of a Python implementation of the server |

[pnpm-workspace.yaml](../pnpm-workspace.yaml) configures package-manager behavior,
including ignored dependency scripts; it has no `packages` workspace member list
at this revision. No nested Go, npm, or Python project manifests were found in the
complete tracked tree. Imported dependencies in lockfiles remain external
dependencies, not repository-owned packages.

These are declarations at the pinned revision. Toolchain availability,
dependency resolution, compatibility, compilation, and tests were not verified
by running them for this documentation pass.

## Backend responsibility map

The [backend guidelines](guidelines-backend.md) give the intended layering:
commands call routers, routers use services, services coordinate models, and
models use lower-level modules. Use this to locate an operation, then check the
actual imports and implementation. It is not a mechanically enforced description
of every dependency: [code-indexer initialization](../modules/indexer/code/indexer.go)
imports `models/db` and `models/repo` from under `modules`.

| Family | Responsibility and important boundaries |
| --- | --- |
| `cmd` | CLI construction, option plumbing, and subcommand entry points. `NewMainApp` chooses `web` as the default command and distinguishes configuration-using subcommands from standalone ones |
| `routers` | HTTP-facing source families: browser pages, API v1, package-registry APIs, Actions APIs, installation, and private endpoints. The family map does not prove middleware order or authorization of any particular route |
| `services` | Application operations and coordination. `services/context` is the request-context family; `services/repository` and `services/repository/files` are repository-operation families. Their full request and service lifecycle review remains open |
| `models` | Persisted entities, query options, and data operations. `models/repo.Repository` is application repository metadata; it is distinct from an open Git repository handle. `models/db` propagates a database session through `context.Context` |
| `modelmigration` | Ordered database-version migrations, historical schema operations, and migration-test helpers. Version directories are source packages, not independent Go modules |
| `modules` | Shared implementations such as configuration, Git invocation, queues, storage, rendering, and indexing. “Module” in the directory name is not a Go module boundary |

### Process entry and configuration handoff

[main.go](../main.go) initializes version/build metadata, calls the Git-proxy
entry hook, constructs the CLI with `cmd.NewMainApp`, and delegates execution to
`cmd.RunMainApp`. It also closes the log manager on the configured exit path and
after normal command completion.

In [cmd/main.go](../cmd/main.go), `PrepareSubcommandWithGlobalFlags` preserves and
runs an existing `Before` hook before preparing work/configuration paths. It passes
explicit `work-path`, `custom-path`, and `config` flags plus `os.Getenv` to
`setting.InitWorkPathAndCommonConfig`. This establishes the handoff, not the full
precedence rules inside `modules/setting`. Do not infer those rules solely from
CLI help text. The [configuration example](../custom/conf/app.example.ini) and
the setting package are the next sources to inspect for an individual option.

`RunMainApp` installs the command context and cancellation, installs usage-error
handlers, and delegates to the CLI runner. Usage errors and other command errors
use different reporting paths before the configured exit callback. This is the
process/CLI lifecycle; the unreviewed HTTP middleware chain is tracked separately
in [remaining work](source-coverage.md#remaining-contract-review).

### An operation crosses several ownership boundaries

For a repository operation, locate the route, its authorization middleware, the
service operation, the model transaction, and the Git/filesystem operation
separately. The [selected contracts](source-contracts.md) establish several
important lower-level rules already visible in inspected source:

- Reusing a database transaction does not create an independent nested commit
- A repository facade can describe an unmanaged repository but cannot supply a
  managed lock/cache identity in that state
- Configuration locks and write locks use different keys
- Background code-indexer work is asynchronous and deliberately does not requeue
  failed items in its handler

None of these rules alone proves that a complete user operation is authorized,
atomic across database and Git state, or safe to retry. Those claims require the
calling route/service implementation and relevant tests.

## Build and test entry points

The [Makefile](../Makefile) is the executable build specification. The following
are source-derived instructions, not commands executed in this pass.

| Entry point | What the target declares |
| --- | --- |
| `make help` | Lists documented targets; consult it on the checkout being built |
| `make build` | Runs `frontend` and `backend` |
| `make frontend` | Installs locked frontend dependencies when needed and builds with Vite |
| `make backend` | Runs backend generation and builds the Go executable |
| `make test-backend` | Runs the selected Go test packages with configured flags/tags |
| `make test-frontend` | Runs Vitest after the Playwright prerequisite |
| `make test-integration` | Builds the application and integration test binary, then invokes the integration runner |
| `make test-migration` | Runs integration migration and individual migration targets; individual packages use `-p 1` because they share a database |
| `make test-e2e` | Depends on Playwright, frontend, and backend before invoking the e2e runner |
| `make lint-md` | Runs `pnpm exec markdownlint *.md`; nested guides require explicit file arguments |

Read [testing.md](testing.md) before using database tests, fixtures, recorded
remote responses, or browser tests. Use disposable data and the declared test
configuration. No test filename in the catalogue is a passing-test receipt.

## Attribution and contribution boundaries

The fork retains [upstream license](../LICENSE),
[contribution](../CONTRIBUTING.md), [security](../SECURITY.md), and
[agent](../AGENTS.md) guidance. The existing
[first-party provenance notice](../M3-SYNEXIA-RIGHTS.md) distinguishes first-party
additions from upstream material; this guide does not replace licenses or claim
ownership of dependencies. Review generated/license artifacts through their
existing generators rather than editing their provenance away.
