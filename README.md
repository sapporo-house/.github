# sapporo-house/.github

Account-level defaults for **sapporo-house** — the OpenSumai project
(`opensumai.fyi`), a neutral processor for buying a house in Japan. Hosts the
reusable workflows every repo calls through a thin caller, plus the community-health
defaults GitHub applies to repos that don't ship their own.

## Reusable workflows

| File | Purpose |
| --- | --- |
| `code-review.yml` | AI code review (open-code-review) on PRs / on-demand `/open-code-review` |
| `security.yml` | gitleaks (secret scan) + semgrep / mobsfscan / actionlint, per-scanner toggles |
| `self-review.yml` | this repo reviews its own PRs |
| `self-scan.yml` | this repo scans its own history + lints its own workflows |

## Caller example

```yaml
# .github/workflows/code-review.yml in a consuming repo (private → on-demand only)
on:
  issue_comment:
    types: [created]
jobs:
  code-review:
    permissions:
      contents: read
      pull-requests: write
    uses: sapporo-house/.github/.github/workflows/code-review.yml@main
    secrets:
      llm_auth_token: ${{ secrets.OCR_LLM_AUTH_TOKEN }}
```

## Notes

- This repo is **private**; its reusable workflows resolve for repos under the same
  `sapporo-house` account.
- `OCR_LLM_AUTH_TOKEN` (the OpenCode Go API key) is a **per-repo** secret — there are no
  account-level secrets.
- Scans run on GitHub-hosted `ubuntu-latest` (no runner fleet).
