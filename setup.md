# Setup Guide

## 1. Deploy the Worker

Deploy the unified worker to Cloudflare Workers as your main production script.

Recommended worker role:
- `security-alert-intake`

## 2. Bind KV

Create and bind:
- `ALERT_KV`

## 3. Add Environment Variables / Secrets

See `env.md` for the full list.

## 4. Configure GitHub

Repository webhook:
- Path: `/github`
- Events: `Issues` (required)
- Content type: `application/json`

Repository target:
- `kpwf-holdings/security-alerting-framework`

## 5. Configure Kanboard

- Enable API access
- Configure project and column IDs
- Configure Kanboard webhook:
  - Path: `/kanboard?key=KANBOARD_WEBHOOK_SECRET`

## 6. Configure Discord

Add a Discord webhook URL to:
- `DISCORD_WEBHOOK_URL`

## 7. Configure IPinfo

Add:
- `IPINFO_TOKEN`

## 8. Configure VirusTotal Input

Do not merge the VT watcher into the worker.
Instead, point the VT watcher to this worker endpoint and make sure the payload identifies the source as VirusTotal.
