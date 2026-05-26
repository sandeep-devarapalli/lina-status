# Lina Status

Static, sanitized status page for Lina/OpenFang.

Published page:

https://sandeep-devarapalli.github.io/lina-status/

This repository should contain only:

- `index.html`
- `status.json`
- `README.md`
- `.gitignore`
- `.github/workflows/check-stale.yml`

It must not contain WhatsApp message text, chat names, JIDs, API keys, MCP keys,
webhook URLs, local filesystem paths, databases, logs, `.env`, QR codes, media,
or WhatsApp auth/session files.

Generate from the local WhatsApp MCP checkout, replacing the paths with your
local checkout and status-site locations:

```bash
cd <whatsapp-mcp-checkout>
go run ./cmd/lina-alerts lina-status-publish -out-dir <lina-status-site>
```

Before publishing, scan the files for local paths, WhatsApp identifiers,
credential names, token-like strings, local URLs, database paths, logs, and chat
content. The scan should return no matches.

## GitHub Freshness Check

`.github/workflows/check-stale.yml` runs every 15 minutes and can also be run
manually from GitHub Actions.

It only reads `status.json`. It does not use secrets, edit files, commit, push,
or call any external service beyond GitHub Actions checkout.

The workflow fails when:

- `last_seen_utc` is older than 30 minutes, or
- `overall` is not `ok`
