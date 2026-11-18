- Never assume, verify before claiming
- List development targets with `make help`
- Before working on code, read the `docs` guides for every area touched: `guidelines-backend.md` for Go, `guidelines-frontend.md` for TS, CSS and Vue, both for templates, `testing.md` for tests, `development.md` for config options and migrations, `guidelines-refactoring.md` for refactors
- Before designing a feature or behavior, check prior art in GitHub and GitLab
- Don't add code for theoretical edge cases, only for ones that can realistically occur. Ask humans to make decisions if the edge case matters, comment the edge case for why it can be ignored if it doesn't matter
- Write docs concisely and user-facing, skip implementation details
- PR descriptions: minimal, only what and why, no task or file listings, no headings. Aim for less than 1000 characters. References go at the end of the description like `Fixes: <url>`.
- PR descriptions and update comments: Include screenshots for UI changes, before and after side by side. Take them at 4x scale in dark theme, cropped to the changes with some padding, and embed them at half CSS size
- Reference issues and PRs by full URL, not by number
- Use Conventional Commits for commit messages and PR titles, plus Gitea's `enhance` type for user-facing enhancements
- Add an `Assisted-by: AGENT_NAME:MODEL_VERSION` trailer to commit messages and PR descriptions, never `Co-Authored-By` or `Signed-off-by`
- Attribute agent authorship on one trailing line in issue and PR comments, never as a PR description section
- Never rewrite git history unless asked, update PRs with new commits and normal push
- Comments: write almost none, short and preferably same-line, explaining why for a future reader. Never narrate code, the change or the prompt. Preserve existing ones that still apply. If you need to write a paragraph-long comment, rethink your implementation, it is likely too complicated
- Add the current year to copyright headers of new `.go` files
- In `options/locale`, only edit `locale_en-US.json`, other locales are synced automatically
- In TS, use `!` instead of `?.`/`??` when a value always exists
- In Go, prefer to use modern language features wherever possible
- In Go, function-name prefixes in errors like `fmt.Errorf("Foo: %w", err)` must always name the function they are in
- Write sizes as multiplications like `64 * 1024`, not bit shifts like `64 << 10`
- Prefer `tw-*` utilities over inline `style` and `flex-*` helpers over per-child `tw-ml-*`/`tw-mr-*` margins, falling back to `tw-*` where specificity requires `!important`
- Run `make fmt` after `.go` edits, `make tidy` after `go.mod` edits, `make generate-swagger` after API changes, and lint what changed with `make lint-go`, `lint-js`, `lint-css` or `lint-templates`
- Fix the cause rather than disabling a linter or weakening a test. Where unavoidable, use the narrowest scope with a trailing comment giving the reason
- Run single tests with `go test -run '^TestName$' ./modulepath/` for Go, `pnpm exec vitest <path-filter>` for TS and `GITEA_TEST_E2E_FLAGS='<filepath>' make test-e2e` for e2e
- Write the fewest, fastest tests covering the behavior, extending an existing one where possible. Prefer unit tests where logic is testable in isolation
- Aim for sub-2s per integration test and sub-4s per e2e test. Wait on a deterministic condition rather than `sleep`, and prefer semantic locators in e2e tests


## Superset merge and history-audit rule (2026-11-18)

Read [.github/MERGE_RULE.md](.github/MERGE_RULE.md) before changing an existing implementation or integrating any branch or PR.
Preserve the supported additive API/behavior superset and select implementations by correctness, predictability, measured performance, then elegance.
Audit all reachable history back to every root, all branches/tags and all PR states for lost code or regressions; preserve append-only history.
Record actual UTC coverage and remaining work in [.github/HISTORY_AUDIT.tsv](.github/HISTORY_AUDIT.tsv); policy installation is not a completed source-history audit.
Prefer verified Apache-2.0 sources and independent implementations while preserving all existing third-party rights; LLM rewriting does not remove license obligations.
Detailed private recipe/proof records remain in canonical Synexia; the compact local policy and checkpoint make the rule discoverable here.
<!-- MERGE-SUPERSET-HISTORY-20261118-2 -->

## MOP SDK: known patterns and explicit machine residue (2026-11-18)

Before source changes, retrieve the [Synexia semantic atom/pattern law](https://github.com/hsoliwal/com.synexia/blob/develop/docs/M3-SCALE/invariants/SYNEXIA-UNIVERSAL-API-ATOM-PATTERN-EVOLUTION-1.md) and [MOP-13 invariant](https://github.com/hsoliwal/com.synexia/blob/develop/docs/M3-SCALE/invariants/SYNEXIA-MOP-SDK-BIDIRECTIONAL-LATTICE-1.md). Descend repository -> project/module -> package -> file -> declarations -> meaningful behavioral atoms, sealing interfaces, effects, ordering, concurrency, ownership and observable contracts. Recognize algorithms and patterns only with versioned catalogue IDs, roles, applicability and evidence. For unmatched structures preserve the source and record `UNKNOWN_ALGORITHM`, `UNKNOWN_PATTERN` or `UNPROVEN_MATCH` in canonical Synexia machine-readable inventory, with source-bound documentation/validated annotation links, proof status and review owner. Never invent uncompilable annotations, force unsound extraction or infer equivalence from names, hashes or an LLM. Recompose qualified atoms upward through the actual caller/dependency closure. Prepare independent files in bounded parallel, then verify and promote serially through source-sealed Synexia recipes and target-native gates. Preserve earlier APIs, history, licenses and notices; this product receives only qualified postimages, not private recipe engines. This policy is not evidence that full-history, atomization, compile/test/runtime or pattern recognition was executed.
