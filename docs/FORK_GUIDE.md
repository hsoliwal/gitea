# Gitea fork: developer entry guide

[Repository README](../README.md) · [Setup](build-setup.md) · [Development](development.md) · [Tests](testing.md)

## Start with the right question

Gitea is a Go-based, self-hosted development service: Git hosting, review, issues, packages, and Actions integration. This fork's README describes a supporting repository-service role in the M3 programme. That direction is separate from evidence of a change to Gitea's implementation or performance; Java runtime proposals do not establish a benefit in this Go service.

This page is a short route through the existing developer documentation, not a deployment or migration recipe. For operating a real instance, use the [upstream administration documentation](https://docs.gitea.com/). Preserve [LICENSE](../LICENSE), upstream credits, and the original guides when making fork-specific changes.

## Architecture in one pass

The [backend guidelines](guidelines-backend.md) describe this dependency direction:

```text
cmd -> routers -> services -> models -> modules
```

| Area | Responsibility | Start reading |
| --- | --- | --- |
| Entry points | CLI commands and server startup | [cmd](../cmd), [main.go](../main.go) |
| HTTP boundaries | Web/API request handlers | [routers](../routers) |
| Business operations | Logic connecting handlers and persistent objects | [services](../services) |
| Persistence | Database models, fixtures, and schema changes | [models](../models), [modelmigration](../modelmigration) |
| Shared facilities | Git interaction, settings, reusable functionality | [modules](../modules) |
| Browser interface | Templates and frontend source; built assets are separate | [templates](../templates), [web_src](../web_src), [public](../public) |

A request can cross several layers. Do not assume that the similarly named model, service, and router package are interchangeable. See the guidelines before introducing an import in the reverse direction.

## Prerequisites and first build

Use [go.mod](../go.mod) for the Go/toolchain version and [package.json](../package.json) for Node.js and pnpm requirements. These are revision-specific, so check them after changing branches. Also install Git and Make; Git LFS is needed for integration tests. Python tooling through uv is needed for template, YAML, and Actions linting. See [setup](build-setup.md) for the complete requirements.

From a checkout of this fork:

```sh
git clone https://github.com/hsoliwal/gitea.git
cd gitea
git rev-parse HEAD
make help
make build
./gitea help
```

The Makefile may download dependencies and tools. `make build` builds frontend and backend; SQLite support is included by default in this revision. For a self-contained distribution, [build-source.md](build-source.md) documents `TAGS="bindata" make build`. Do not add packaging tags merely to read or edit the source.

Starting `./gitea web` starts a server and may initialize local state. Use a disposable development setup with reviewed configuration, never an existing production database or repository directory.

## Command cheat sheet

Run from the repository root after setup. These are documented entry points, not results of a test run.

| Goal | Command | Boundary |
| --- | --- | --- |
| Discover targets | `make help` | Prefer the checked-out Makefile over remembered commands |
| Build for development | `make build` | Compiles frontend and backend |
| Rebuild on changes | `make watch` | Starts long-running development processes |
| Backend unit tests | `make test-backend` | Unit coverage, not integration/e2e coverage |
| Frontend unit tests | `make test-frontend` | Vitest browser-mode setup required |
| Integration tests | `make test-integration` | Requires Git LFS; defaults to SQLite |
| Browser workflow tests | `make test-e2e` | Playwright against a running test instance |
| Migration tests | `make test-migration` | Relevant to database schema changes |
| Review documentation edits | `git diff --check` | Whitespace only; does not validate links or behavior |

For one backend test, replace both placeholders in `go test -run '^TestName$' ./modulepath/`. For one frontend test file, use `pnpm exec vitest <path-filter>`. For one e2e file, use `GITEA_TEST_E2E_FLAGS='<filepath>' make test-e2e`. Select actual paths/test names from the checkout.

Keep test databases disposable. The [testing guide](testing.md) explains non-SQLite services and warns that credentials/environment variables can switch recorded migration API tests to live recording.

## Worked exploration: repository API behavior

Before changing an API response, trace a small path without running a server:

```sh
git grep -n 'func GetByID' -- routers/api/v1/repo/repo.go
git grep -n 'GetRepositoryByID' -- routers/api/v1/repo/repo.go models
git grep -n 'CreateRepository' -- routers/api/v1/repo/repo.go services/repository
git ls-files 'tests/integration/*repo*' 'models/*/*_test.go'
```

1. Read `GetByID` in [repo.go](../routers/api/v1/repo/repo.go), including its error path and response conversion.
2. Follow the model lookup. Contrast this read path with repository creation, which delegates to a service. The layer map is a guide, not a claim that every request calls every layer.
3. Read neighboring integration tests before choosing a regression test.
4. For an actual API change, follow the [API guidelines](guidelines-backend.md#api-v1) and the documented Swagger generation/validation steps. A documentation edit alone does not need generated API changes.

Write down the route, input, permission assumptions, lookup or service operation, response, and failure case. Source reading establishes where to investigate; only a test run establishes observed behavior.

## Common setup mistakes

- Missing assets: use the combined build and keep the working directory at the repository root; see the IDE notes in [development.md](development.md#ide-configuration).
- Toolchain mismatch: reconcile Go and Node versions with the checked-out manifests before changing dependencies.
- Integration failures involving LFS: verify the prerequisite rather than treating every failure as an application defect.
- Unexpected network calls in tests: inspect credential-dependent recording behavior before running migration tests.
- Configuration changes: both settings code and the example configuration/documentation must be considered; see the development guide.

## Review and evidence

Read [CONTRIBUTING.md](../CONTRIBUTING.md) and [AGENTS.md](../AGENTS.md) before proposing changes. Keep fork-specific orientation separate from upstream product claims. Record the revision, commands actually run, results, and what remains unchecked. Disclose AI assistance and keep draft status until human review; the contribution policy asks contributors themselves to answer review questions.

This guide was checked against public repository sources on 2026-10-14. Build, lint, application startup, database tests, and browser tests were not executed as part of writing it. No speed, compatibility, or production-readiness result is implied.

## Worked diagnosis: why a repository lookup can return 404

The `GetByID` handler in [repo.go](../routers/api/v1/repo/repo.go) documents `GET /repositories/{id}`. Its source distinguishes several cases that can look identical to an API client:

| Handler stage | Source outcome | Investigation |
| --- | --- | --- |
| Model lookup says the repository does not exist | Not-found response | Verify the ID in an authorized test fixture |
| Model lookup returns another error | Internal-error response | Inspect the server-side error with secrets removed |
| Token cannot access the repository | Not-found response | Check the intended token's repository scope without printing the token |
| Permission lookup fails | Internal-error response | Inspect the permission lookup and its dependencies |
| User has no unit access | Not-found response | Check the test user's repository/unit access |
| Checks succeed | Converted repository response with status 200 | Inspect the permission-aware conversion |

Thus, a 404 does not prove that an ID is absent. Do not “fix” the symptom by removing permission checks or widening access. This is a trace of the handler, not an exhaustive description of authentication middleware or every route failure.

A source-only investigation can continue with:

```sh
git grep -n 'repo.GetByID' -- routers/api/v1
git grep -n 'TokenCanAccessRepo' -- services modules routers
git grep -n 'GetDoerRepoPermission' -- models/perm
git grep -n 'repoGetByID' -- tests/integration routers/api/v1
```

Read the route registration and middleware before interpreting handler behavior. For a disposable test setup, build a matrix of an existing accessible repository, a nonexistent ID, and an existing repository outside the caller's allowed scope. Record the status and sanitized response for each; the last case must not expose the inaccessible repository's details. These are proposed checks, not test results.

### Keeping this guide current

When routes, manifests, or Make targets change, verify the affected command against the same revision, update its source link, and recheck the worked example's branch conditions. Preserve the difference between source inspection and a request actually executed. A renamed symbol requires updating both the prose and its search command; a changed permission model needs renewed review of the diagnostic table.
