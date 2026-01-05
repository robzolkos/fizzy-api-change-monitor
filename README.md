# Upstream Monitors

GitHub Actions workflows that monitor upstream repositories for changes and create issues in my repos.

## Workflows

### Fizzy API Monitor

**File:** `.github/workflows/check-fizzy-api.yml`

Monitors `docs/API.md` in [basecamp/fizzy](https://github.com/basecamp/fizzy) for changes.

**Schedule:** Daily at 9am UTC

**Behavior:**
- Fetches the Atom feed for `docs/API.md` commits
- If any commits occurred in the last 24 hours, creates/updates an issue in [robzolkos/fizzy-cli](https://github.com/robzolkos/fizzy-cli)
- Issue lists all recent commits with links, authors, and timestamps
- If an open issue already exists (label: `upstream-api-change`), updates it
- Closing the issue resets the cycle - next detected change creates a fresh issue

**Setup:**
1. Create a Personal Access Token with `repo` scope
2. Add it as a secret named `FIZZY_REPO_TOKEN` in this repo's settings

**Manual trigger:** Run from the Actions tab using "Run workflow"
