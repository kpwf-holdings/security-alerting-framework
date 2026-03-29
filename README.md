# Security Alerting Framework

Version: v1.0.0

A unified security alerting pipeline built on Cloudflare Workers. It ingests alerts, enriches them, deduplicates them, routes them into Kanboard and GitHub, and sends critical notifications to Discord.

## Current Workflow

Alert Source → Cloudflare Worker → Kanboard → GitHub → Worker → Kanboard (Resolved)

Critical Kanboard task movement also triggers Discord alerts.

## Supported Inputs

- Cloudflare alerts
- Firewalla alerts
- VirusTotal alerts
- Manual test payloads

## Core Capabilities

- Unified alert intake
- KV-based deduplication
- IP intelligence enrichment with IPinfo
- VirusTotal bypass for non-IP based malware events
- Kanboard task lifecycle tracking
- GitHub issue creation with embedded Kanboard Task ID
- GitHub issue close → Kanboard resolve + close
- Discord alerting for critical incidents

## Security Model

- GitHub resolution uses embedded Kanboard Task ID instead of KV lookup
- Discord webhook is protected behind Kanboard webhook secret validation
- Non-suspicious non-VT alerts can be filtered before task creation
- KV is used for deduplication only

## Required Configuration

See:
- `setup.md`
- `env.md`
- `testing.md`

## Repository Structure

- `worker.js` — unified production worker
- `README.md` — high-level project overview
- `architecture.md` — architecture details
- `DIAGRAM.md` — diagram source
- `setup.md` — deployment and configuration
- `env.md` — environment variable reference
- `testing.md` — validation steps
- `usage.md` — operating guide

## Known Operational Notes

- `GITHUB_REPO` must point to `kpwf-holdings/security-alerting-framework`
- Kanboard swimlane is currently assumed to be `29`
- Discord fires only when a task enters the Kanboard Critical column
- VT alerts bypass IP-based suspiciousness filtering

## Future Enhancements

- Smarter alert scoring and confidence thresholds
- Slack + Discord multi-channel output
- IP reputation-based escalation policy
- Alert grouping / threading
- Reporting dashboards
