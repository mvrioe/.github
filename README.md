# .github

Defaults for every public repository of this account, plus reusable workflows.

- **Community health files** (`SECURITY.md`, issue and PR templates) apply to any repo that has none of its own.
- **Reusable workflows** in `.github/workflows/`: `node-ci` (pnpm), `flutter-ci` (fvm's `.fvmrc`), `codeql`, `dependency-review`. Call them pinned by commit SHA, never by branch:

  ```yaml
  jobs:
    ci:
      uses: mvrioe/.github/.github/workflows/node-ci.yml@<sha>
  ```

## Security baseline

- Every workflow defaults to `permissions: contents: read`; jobs request more only when needed.
- Actions are pinned by full commit SHA (Dependabot updates them, with a 7-day cooldown).
- Checkout runs with `persist-credentials: false`; dependency install scripts don't run in CI (`--ignore-scripts`).
- No `pull_request_target`, no secrets in reusable workflows.

Not inherited from this repo (GitHub limitation): `dependabot.yml` and workflows must live in each repo. Workflow templates only work for organizations.
