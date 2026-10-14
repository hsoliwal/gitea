# Tracked tree and frontend boundaries

[Architecture](source-architecture.md) · [Go packages](package-catalog.md) ·
[Coverage](source-coverage.md)

## Inventory method

The recursive Git tree for
[`0ec192ded6c4d3bc577abd643872a27a423053d2`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/) returned `truncated: false`:
**7,756 entries = 6,359 blobs + 1,397 trees**. There were no gitlink/submodule or
symlink entries in this response. Counts describe tracked paths at that revision,
not a built checkout, downloaded dependencies, ignored files, or deployment data.
The 22 root directories and 53 root-level files are accounted for below.

## Root ownership map

| Root directory | Tracked blobs recursively | Scope |
| --- | ---: | --- |
| [`.devcontainer`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/.devcontainer) | 1 | Development-container configuration; manifest body not reviewed |
| [`.github`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/.github) | 32 | CI, issue, and pull-request configuration; workflows not executed |
| [`.m3`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/.m3) | 3 | Auxiliary atomize-patternize README/scripts; presence is not proof of runtime integration or execution |
| [`assets`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/assets) | 5 | Build-support data including dependency-license records and spelling data |
| [`build`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/build) | 10 | Code/data generators, OpenAPI conversion helper and tests, and locale tooling |
| [`cmd`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/cmd) | 58 | CLI implementation and command tests |
| [`contrib`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/contrib) | 31 | Contributed service/development configurations and monitoring mixin; retains distinct toolchain boundary below |
| [`custom`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/custom) | 1 | Example application configuration; no live configuration is included by this guide |
| [`docker`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/docker) | 21 | Container support files and instructions; not evidence of a verified image |
| [`docs`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/docs) | 9 | Developer documentation at the baseline before these new guides |
| [`modelmigration`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/modelmigration) | 388 | Database migration coordinator, historical migration packages, and migration fixtures/tests |
| [`models`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/models) | 467 | Database entities/helpers and test fixtures |
| [`modules`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/modules) | 1298 | Shared implementation packages and package-specific test data |
| [`options`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/options) | 332 | Runtime option resources such as locales, licenses, labels, and file icons |
| [`public`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/public) | 492 | Tracked public/static resources; build output also lands here, so not every tracked file is a generated bundle |
| [`routers`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/routers) | 511 | HTTP route/handler families and their tests |
| [`services`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/services) | 681 | Application services, request contexts, and recorded migration data/tests |
| [`snap`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/snap) | 3 | Snap packaging files; manifest body not reviewed |
| [`templates`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/templates) | 599 | Server-rendered templates and Swagger/OpenAPI resources |
| [`tests`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/tests) | 934 | Shared test helpers, integration, browser/e2e, fuzz, and fixture data |
| [`tools`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/tools) | 18 | Build/lint/test shell, Go, and TypeScript utilities |
| [`web_src`](https://github.com/hsoliwal/gitea/tree/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src) | 412 | Frontend TypeScript/Vue, CSS, SVG, and Fomantic source inputs |

The 53 root-level tracked files are:

- [`.air.toml`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/.air.toml)
- [`.changelog.yml`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/.changelog.yml)
- [`.dockerignore`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/.dockerignore)
- [`.editorconfig`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/.editorconfig)
- [`.envrc`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/.envrc)
- [`.gitattributes`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/.gitattributes)
- [`.gitignore`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/.gitignore)
- [`.golangci.yml`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/.golangci.yml)
- [`.ignore`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/.ignore)
- [`.mailmap`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/.mailmap)
- [`.markdownlint.yaml`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/.markdownlint.yaml)
- [`.shellcheckrc`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/.shellcheckrc)
- [`.spectral.yaml`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/.spectral.yaml)
- [`.yamllint.yaml`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/.yamllint.yaml)
- [`AGENTS.md`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/AGENTS.md)
- [`BSDmakefile`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/BSDmakefile)
- [`CHANGELOG-archived.md`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/CHANGELOG-archived.md)
- [`CHANGELOG.md`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/CHANGELOG.md)
- [`CODE_OF_CONDUCT.md`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/CODE_OF_CONDUCT.md)
- [`CONTRIBUTING.md`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/CONTRIBUTING.md)
- [`DCO`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/DCO)
- [`Dockerfile`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/Dockerfile)
- [`Dockerfile.rootless`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/Dockerfile.rootless)
- [`LICENSE`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/LICENSE)
- [`M3-SYNEXIA-RIGHTS.md`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/M3-SYNEXIA-RIGHTS.md)
- [`MAINTAINERS`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/MAINTAINERS)
- [`Makefile`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/Makefile)
- [`README.md`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/README.md)
- [`README.zh-cn.md`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/README.zh-cn.md)
- [`README.zh-tw.md`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/README.zh-tw.md)
- [`SECURITY.md`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/SECURITY.md)
- [`crowdin.yml`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/crowdin.yml)
- [`eslint.config.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/eslint.config.ts)
- [`eslint.json.config.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/eslint.json.config.ts)
- [`flake.lock`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/flake.lock)
- [`flake.nix`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/flake.nix)
- [`go.mod`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/go.mod)
- [`go.sum`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/go.sum)
- [`main.go`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/main.go)
- [`main_timezones.go`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/main_timezones.go)
- [`package.json`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/package.json)
- [`playwright.config.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/playwright.config.ts)
- [`pnpm-lock.yaml`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/pnpm-lock.yaml)
- [`pnpm-workspace.yaml`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/pnpm-workspace.yaml)
- [`pyproject.toml`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/pyproject.toml)
- [`renovate.json5`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/renovate.json5)
- [`stylelint.config.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/stylelint.config.ts)
- [`tailwind.config.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/tailwind.config.ts)
- [`tsconfig.json`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/tsconfig.json)
- [`types.d.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/types.d.ts)
- [`uv.lock`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/uv.lock)
- [`vite.config.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/vite.config.ts)
- [`vitest.config.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/vitest.config.ts)

## Contributed and packaging boundaries

In addition to the three root toolchain manifests described in the
[architecture guide](source-architecture.md#manifest-backed-boundaries), the tree
contains a contributed monitoring project with
[jsonnetfile.json](../contrib/grafana-monitoring-mixin/jsonnetfile.json), its lockfile,
a [Makefile](../contrib/grafana-monitoring-mixin/Makefile), and Jsonnet/Libsonnet
sources. This is a separate candidate tooling/project boundary; its manifests,
dependency semantics, generated dashboards/rules, and build have not yet been
reviewed. It is not another Go module.

Root [Dockerfile](../Dockerfile), [Dockerfile.rootless](../Dockerfile.rootless),
[flake.nix](../flake.nix), [BSDmakefile](../BSDmakefile), and
[snap/snapcraft.yaml](../snap/snapcraft.yaml) are also tracked build/packaging
entry points. Their presence is included in scope, but no source-reviewed support
matrix or successful package/image build is asserted here. `contrib/service`
contains deployment examples rather than independently compiled Go packages.

## Frontend build contract

The inspected [Vite configuration](../vite.config.ts) establishes these production
entries: `web_src/js/index.ts`, `swagger.ts`, `external-render-frontend.ts`,
`user-events.sharedworker.ts`, `web_src/css/devtest.css`, and CSS theme files.
Additional IIFE builds handle `iife.ts` and `external-render-helper.ts`.
The dev-server/IIFE path keeps an in-memory build and reloads when its recorded
inputs change; the production path writes a bundle and updates Vite's manifest.

Outputs go to `public/assets`; JS, CSS, and font naming uses content hashes.
`base: './'` makes generated asset URLs relative. Source maps default to reduced
mode in production and full mode in development, with an environment override.
The configuration's reduced mode keeps selected standalone JS maps, not every
bundle map. A production license plugin combines Go-license records with bundled
JavaScript dependency licenses; development writes a license placeholder.

These facts come from build configuration. The behavior of the frontend entry
modules, shared-worker message protocol, DOM ownership, Vue components, and
individual exports has not been reviewed yet. A Vite entry is not a separate npm
package or deployed service.

The tracked `web_src` tree has 412 files: 246 under `js`, 92 under `css`, 67 under
`svg`, and 7 under `fomantic`. All 246 JS/TS/Vue source-file candidates are linked
below, including 51 `*.test.ts`/`*.test.js` files. These file counts deliberately
do not pretend to resolve an ESM import graph or runtime reachability.

### Frontend source-file inventory

#### web_src/fomantic/build

- [`fomantic.js`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/fomantic/build/fomantic.js)

#### web_src/fomantic/build/components

- [`api.js`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/fomantic/build/components/api.js)
- [`dropdown.js`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/fomantic/build/components/dropdown.js)
- [`modal.js`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/fomantic/build/components/modal.js)

#### web_src/js

- [`bootstrap.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/bootstrap.ts)
- [`external-render-frontend.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/external-render-frontend.ts)
- [`external-render-helper.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/external-render-helper.test.ts) (test; not run)
- [`external-render-helper.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/external-render-helper.ts)
- [`globals.d.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/globals.d.ts)
- [`globals.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/globals.ts)
- [`iife.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/iife.ts)
- [`index.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/index.ts)
- [`svg.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/svg.test.ts) (test; not run)
- [`svg.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/svg.ts)
- [`swagger.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/swagger.ts)
- [`types.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/types.ts)
- [`user-events.sharedworker.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/user-events.sharedworker.ts)
- [`utils.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils.test.ts) (test; not run)
- [`utils.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils.ts)
- [`vitest.setup.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/vitest.setup.ts)

#### web_src/js/components

- [`ActionRunArtifacts.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/ActionRunArtifacts.test.ts) (test; not run)
- [`ActionRunArtifacts.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/ActionRunArtifacts.ts)
- [`ActionRunJobView.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/ActionRunJobView.vue)
- [`ActionRunSummaryView.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/ActionRunSummaryView.vue)
- [`ActionRunView.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/ActionRunView.test.ts) (test; not run)
- [`ActionRunView.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/ActionRunView.ts)
- [`ActionStatusIcon.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/ActionStatusIcon.vue)
- [`ActivityHeatmap.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/ActivityHeatmap.vue)
- [`ChartCanvas.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/ChartCanvas.vue)
- [`ContextPopup.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/ContextPopup.vue)
- [`DashboardRepoList.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/DashboardRepoList.vue)
- [`DiffCommitSelector.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/DiffCommitSelector.vue)
- [`DiffFileExtensionFilter.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/DiffFileExtensionFilter.vue)
- [`DiffFileTree.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/DiffFileTree.vue)
- [`DiffFileTreeItem.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/DiffFileTreeItem.test.ts) (test; not run)
- [`DiffFileTreeItem.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/DiffFileTreeItem.vue)
- [`PullRequestMergeForm.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/PullRequestMergeForm.vue)
- [`RepoActionView.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/RepoActionView.vue)
- [`RepoActivityTopAuthors.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/RepoActivityTopAuthors.vue)
- [`RepoBranchTagSelector.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/RepoBranchTagSelector.vue)
- [`RepoCodeFrequency.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/RepoCodeFrequency.vue)
- [`RepoContributors.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/RepoContributors.vue)
- [`RepoFileSearch.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/RepoFileSearch.vue)
- [`RepoRecentCommits.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/RepoRecentCommits.vue)
- [`SvgIcon.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/SvgIcon.test.ts) (test; not run)
- [`SvgIcon.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/SvgIcon.vue)
- [`ViewFileTree.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/ViewFileTree.vue)
- [`ViewFileTreeItem.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/ViewFileTreeItem.vue)
- [`ViewFileTreeStore.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/ViewFileTreeStore.ts)
- [`WorkflowGraph.utils.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/WorkflowGraph.utils.test.ts) (test; not run)
- [`WorkflowGraph.utils.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/WorkflowGraph.utils.ts)
- [`WorkflowGraph.vue`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/components/WorkflowGraph.vue)

#### web_src/js/features

- [`captcha.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/captcha.ts)
- [`citation.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/citation.ts)
- [`code-frequency.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/code-frequency.ts)
- [`colorpicker.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/colorpicker.ts)
- [`common-actions-permissions.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/common-actions-permissions.ts)
- [`common-button.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/common-button.test.ts) (test; not run)
- [`common-button.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/common-button.ts)
- [`common-form.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/common-form.ts)
- [`common-issue-list.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/common-issue-list.test.ts) (test; not run)
- [`common-issue-list.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/common-issue-list.ts)
- [`common-organization.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/common-organization.ts)
- [`common-page.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/common-page.ts)
- [`contributors.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/contributors.ts)
- [`copycontent.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/copycontent.ts)
- [`dashboard.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/dashboard.ts)
- [`dropzone.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/dropzone.ts)
- [`emoji.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/emoji.ts)
- [`file-fold.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/file-fold.ts)
- [`file-view.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/file-view.ts)
- [`heatmap.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/heatmap.ts)
- [`imagediff.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/imagediff.ts)
- [`install.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/install.ts)
- [`issue.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/issue.ts)
- [`notification.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/notification.ts)
- [`oauth2-settings.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/oauth2-settings.ts)
- [`org-team.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/org-team.ts)
- [`packages.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/packages.test.ts) (test; not run)
- [`packages.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/packages.ts)
- [`pull-view-file.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/pull-view-file.ts)
- [`recent-commits.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/recent-commits.ts)
- [`ref-issue.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/ref-issue.ts)
- [`repo-actions.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-actions.test.ts) (test; not run)
- [`repo-actions.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-actions.ts)
- [`repo-branch.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-branch.ts)
- [`repo-code.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-code.ts)
- [`repo-commit.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-commit.ts)
- [`repo-common.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-common.test.ts) (test; not run)
- [`repo-common.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-common.ts)
- [`repo-diff-commit.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-diff-commit.ts)
- [`repo-diff-commitselect.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-diff-commitselect.ts)
- [`repo-diff-filetree.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-diff-filetree.ts)
- [`repo-diff.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-diff.ts)
- [`repo-editor.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-editor.ts)
- [`repo-findfile.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-findfile.test.ts) (test; not run)
- [`repo-findfile.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-findfile.ts)
- [`repo-graph.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-graph.ts)
- [`repo-home.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-home.ts)
- [`repo-issue-content.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-issue-content.ts)
- [`repo-issue-edit.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-issue-edit.ts)
- [`repo-issue-list.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-issue-list.ts)
- [`repo-issue-pull.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-issue-pull.ts)
- [`repo-issue-sidebar-combolist.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-issue-sidebar-combolist.test.ts) (test; not run)
- [`repo-issue-sidebar-combolist.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-issue-sidebar-combolist.ts)
- [`repo-issue-sidebar.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-issue-sidebar.ts)
- [`repo-issue.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-issue.ts)
- [`repo-legacy.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-legacy.ts)
- [`repo-migrate.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-migrate.ts)
- [`repo-migration.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-migration.ts)
- [`repo-milestone.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-milestone.ts)
- [`repo-new.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-new.ts)
- [`repo-projects.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-projects.ts)
- [`repo-release.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-release.test.ts) (test; not run)
- [`repo-release.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-release.ts)
- [`repo-search.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-search.ts)
- [`repo-settings-branches.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-settings-branches.test.ts) (test; not run)
- [`repo-settings-branches.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-settings-branches.ts)
- [`repo-settings.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-settings.ts)
- [`repo-switcher.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-switcher.ts)
- [`repo-unicode-escape.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-unicode-escape.ts)
- [`repo-view-file-tree.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-view-file-tree.ts)
- [`repo-watch.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-watch.ts)
- [`repo-wiki.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/repo-wiki.ts)
- [`sshkey-helper.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/sshkey-helper.ts)
- [`stopwatch.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/stopwatch.ts)
- [`tablesort.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/tablesort.ts)
- [`tribute.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/tribute.ts)
- [`user-auth-webauthn.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/user-auth-webauthn.ts)
- [`user-auth.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/user-auth.ts)
- [`user-settings.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/user-settings.ts)

#### web_src/js/features/admin

- [`common.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/admin/common.ts)
- [`config.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/admin/config.test.ts) (test; not run)
- [`config.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/admin/config.ts)
- [`selfcheck.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/admin/selfcheck.ts)
- [`users.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/admin/users.ts)

#### web_src/js/features/comp

- [`ComboMarkdownEditor.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/comp/ComboMarkdownEditor.ts)
- [`ConfirmModal.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/comp/ConfirmModal.ts)
- [`Cropper.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/comp/Cropper.ts)
- [`EasyMDEToolbarActions.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/comp/EasyMDEToolbarActions.ts)
- [`EditorMarkdown.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/comp/EditorMarkdown.test.ts) (test; not run)
- [`EditorMarkdown.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/comp/EditorMarkdown.ts)
- [`EditorUpload.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/comp/EditorUpload.test.ts) (test; not run)
- [`EditorUpload.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/comp/EditorUpload.ts)
- [`LabelEdit.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/comp/LabelEdit.ts)
- [`QuickSubmit.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/comp/QuickSubmit.ts)
- [`ReactionSelector.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/comp/ReactionSelector.ts)
- [`ScopedWorkflows.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/comp/ScopedWorkflows.test.ts) (test; not run)
- [`ScopedWorkflows.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/comp/ScopedWorkflows.ts)
- [`SearchRepoBox.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/comp/SearchRepoBox.ts)
- [`SearchUserBox.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/comp/SearchUserBox.ts)
- [`TextExpander.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/comp/TextExpander.ts)
- [`WebHookEditor.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/features/comp/WebHookEditor.ts)

#### web_src/js/markup

- [`anchors.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/markup/anchors.ts)
- [`codecopy.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/markup/codecopy.ts)
- [`common.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/markup/common.ts)
- [`content.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/markup/content.ts)
- [`html2markdown.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/markup/html2markdown.test.ts) (test; not run)
- [`html2markdown.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/markup/html2markdown.ts)
- [`math.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/markup/math.ts)
- [`mermaid.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/markup/mermaid.ts)
- [`render-iframe.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/markup/render-iframe.test.ts) (test; not run)
- [`render-iframe.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/markup/render-iframe.ts)
- [`tasklist.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/markup/tasklist.test.ts) (test; not run)
- [`tasklist.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/markup/tasklist.ts)

#### web_src/js/modules

- [`action-status-icon.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/action-status-icon.test.ts) (test; not run)
- [`action-status-icon.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/action-status-icon.ts)
- [`are-you-sure.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/are-you-sure.test.ts) (test; not run)
- [`are-you-sure.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/are-you-sure.ts)
- [`clipboard.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/clipboard.ts)
- [`devtest.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/devtest.ts)
- [`diff-file.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/diff-file.test.ts) (test; not run)
- [`diff-file.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/diff-file.ts)
- [`errors.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/errors.test.ts) (test; not run)
- [`errors.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/errors.ts)
- [`favicon-status.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/favicon-status.test.ts) (test; not run)
- [`favicon-status.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/favicon-status.ts)
- [`fetch-action.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/fetch-action.test.ts) (test; not run)
- [`fetch-action.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/fetch-action.ts)
- [`fetch.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/fetch.test.ts) (test; not run)
- [`fetch.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/fetch.ts)
- [`fomantic.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/fomantic.ts)
- [`gitea-actions.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/gitea-actions.ts)
- [`i18n.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/i18n.test.ts) (test; not run)
- [`i18n.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/i18n.ts)
- [`init.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/init.ts)
- [`observer.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/observer.ts)
- [`search.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/search.ts)
- [`shortcut.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/shortcut.ts)
- [`sortable.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/sortable.ts)
- [`tippy.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/tippy.test.ts) (test; not run)
- [`tippy.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/tippy.ts)
- [`toast.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/toast.test.ts) (test; not run)
- [`toast.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/toast.ts)
- [`user-settings.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/user-settings.ts)
- [`worker.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/worker.test.ts) (test; not run)
- [`worker.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/worker.ts)

#### web_src/js/modules/codeeditor

- [`command-palette.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/codeeditor/command-palette.ts)
- [`context-menu.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/codeeditor/context-menu.ts)
- [`linter.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/codeeditor/linter.ts)
- [`main.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/codeeditor/main.test.ts) (test; not run)
- [`main.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/codeeditor/main.ts)
- [`utils.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/codeeditor/utils.test.ts) (test; not run)
- [`utils.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/codeeditor/utils.ts)

#### web_src/js/modules/fomantic

- [`base.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/fomantic/base.ts)
- [`dimmer.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/fomantic/dimmer.ts)
- [`dropdown.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/fomantic/dropdown.test.ts) (test; not run)
- [`dropdown.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/fomantic/dropdown.ts)
- [`modal.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/fomantic/modal.ts)
- [`tab.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/fomantic/tab.ts)
- [`transition.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/modules/fomantic/transition.ts)

#### web_src/js/render

- [`ansi.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/render/ansi.test.ts) (test; not run)
- [`ansi.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/render/ansi.ts)
- [`plugin.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/render/plugin.ts)
- [`swagger.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/render/swagger.ts)

#### web_src/js/render/plugins

- [`frontend-asciicast.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/render/plugins/frontend-asciicast.ts)
- [`frontend-openapi-swagger.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/render/plugins/frontend-openapi-swagger.ts)
- [`frontend-viewer-3d.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/render/plugins/frontend-viewer-3d.ts)
- [`inplace-pdf-viewer.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/render/plugins/inplace-pdf-viewer.ts)

#### web_src/js/utils

- [`color.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/color.test.ts) (test; not run)
- [`color.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/color.ts)
- [`dom.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/dom.test.ts) (test; not run)
- [`dom.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/dom.ts)
- [`func.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/func.test.ts) (test; not run)
- [`func.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/func.ts)
- [`glob.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/glob.test.ts) (test; not run)
- [`glob.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/glob.ts)
- [`html.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/html.test.ts) (test; not run)
- [`html.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/html.ts)
- [`image.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/image.test.ts) (test; not run)
- [`image.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/image.ts)
- [`match.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/match.test.ts) (test; not run)
- [`match.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/match.ts)
- [`string.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/string.test.ts) (test; not run)
- [`string.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/string.ts)
- [`testhelper.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/testhelper.ts)
- [`time.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/time.test.ts) (test; not run)
- [`time.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/time.ts)
- [`url.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/url.test.ts) (test; not run)
- [`url.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/utils/url.ts)

#### web_src/js/webcomponents

- [`index.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/webcomponents/index.ts)
- [`overflow-menu.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/webcomponents/overflow-menu.ts)
- [`polyfill.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/webcomponents/polyfill.test.ts) (test; not run)
- [`polyfills.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/webcomponents/polyfills.ts)
- [`relative-time.test.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/webcomponents/relative-time.test.ts) (test; not run)
- [`relative-time.ts`](https://github.com/hsoliwal/gitea/blob/0ec192ded6c4d3bc577abd643872a27a423053d2/web_src/js/webcomponents/relative-time.ts)

## Fixtures, generated files, and external custody

Fixture-marker counts from the complete tracked path list are 120 paths with a
`fixtures` segment, 33 with `testdata`, and 170 with `_mock_data`. These are
path-marker counts, not a complete content-based classification: tests also keep
data in other locations. They stay in the repository inventory but are not
counted as production package APIs merely because a file is present.

No tracked path has a `vendor` or `node_modules` segment. That does not mean the
project has no third-party code or dependencies. Go/npm/Python lockfiles, embedded
resources, imported data, and contributed components have separate custody and
license obligations. The Makefile's `vendor` target can create a directory not
present in this snapshot.

The inspected Makefile explicitly identifies the two generated charset tables,
Swagger/OpenAPI JSON outputs, Vite assets/manifest, SVG/file-icon destinations,
Go-license output, and `bindata.*` destinations. Files named
`options_bindata.go`, `public_bindata.go`, or `templates_bindata.go` must not be
mistaken for all generated payloads merely because they contain “bindata” in the
name. They are separate tracked Go source paths. The tree also contains
`routers/api/actions/artifact.pb.go`, whose generated-code provenance still needs
source/header review.

Build tags and platform choices are part of package semantics: the tree includes
`gogit`/`nogogit`, PAM/stub, Windows/Unix, and static/dynamic asset variants. The
sampled `build/generate-bindata.go` has `go:build ignore`. A directory census is
not a valid replacement for checking all relevant constraints and running the
authorized build/test configuration.
