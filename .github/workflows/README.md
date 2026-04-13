# Railway Log Sync

Pulls logs from all Basis Protocol Railway services every 15 minutes and commits them to `logs/`.

## Setup

1. **Add this workflow** to whichever repo you want logs stored in (could be `basis-protocol` main repo or a dedicated `basis-ops` repo).

2. **Add the Railway API token as a GitHub secret:**
   - Go to repo → Settings → Secrets and variables → Actions
   - Click "New repository secret"
   - Name: `RAILWAY_API_TOKEN`
   - Value: your Railway API token

3. **Enable GitHub Actions** if not already enabled.

4. **That's it.** Logs will appear in `logs/` every 15 minutes:
   ```
   logs/
   ├── LAST_PULL.txt          # Timestamp + summary
   ├── api-server.log
   ├── basis-provenance.log
   ├── basis-state.log
   ├── keeper.log
   └── scoring-worker.log
   ```

## Usage with Claude

Just say "check the logs" or "what's in the api-server logs" — Claude can pull from GitHub directly.

## Manual trigger

Go to Actions → Pull Railway Logs → Run workflow.

## Notes

- Logs are overwritten each run (latest 500 lines per service). Not a persistent archive.
- If you want log history, change the workflow to append with timestamps instead of overwriting.
- The Railway GraphQL API schema may change — if logs stop pulling, check https://docs.railway.com/reference/public-api
