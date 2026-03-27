# Setup Guide

## Requirements
- Cloudflare Workers account
- Kanboard instance (with API enabled)
- GitHub repository
- Discord webhook

## Environment Variables

KANBOARD_URL
KANBOARD_TOKEN
KANBOARD_PROJECT_ID
KANBOARD_COLUMN_CRITICAL
KANBOARD_COLUMN_INVESTIGATING
KANBOARD_COLUMN_RESOLVED
KANBOARD_WEBHOOK_SECRET

GITHUB_TOKEN
GITHUB_REPO

DISCORD_WEBHOOK_URL

ALERT_KV (binding)

## Deployment

1. Deploy worker.js to Cloudflare Workers
2. Add all environment variables
3. Bind KV namespace
4. Set routes if needed

## Webhooks

GitHub:
- /github endpoint
- Events: Issues

Kanboard:
- /kanboard?key=SECRET
