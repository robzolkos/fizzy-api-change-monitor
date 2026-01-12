# Fizzy API Monitor
GitHub Actions workflow that monitors changes to Fizzy API documentation.

## Workflow

**File:** `.github/workflows/check-fizzy-api.yml`

Monitors `docs/API.md` in [basecamp/fizzy](https://github.com/basecamp/fizzy) for changes.

**Schedule:** Daily at 9am UTC

**How it works:**
- Uses GitHub API to fetch commits that touched `docs/API.md` specifically (not the whole repo)
- Stores the last known commit SHA in the `history` branch
- Compares against the current latest SHA for that file
- If different, fetches all new commits and creates/updates an issue in [robzolkos/fizzy-cli](https://github.com/robzolkos/fizzy-cli)
- Updates the stored SHA after successful detection

This approach catches changes regardless of when commits were authored vs merged.

**Issue behavior:**
- If an open issue exists (label: `upstream-api-change`), updates it
- Closing the issue resets the cycle - next detected change creates a fresh issue

**Setup:**
1. Create a Personal Access Token with `repo` scope
2. Add it as a secret named `FIZZY_REPO_TOKEN` in this repo's settings

**Manual trigger:** Run from the Actions tab using "Run workflow"
