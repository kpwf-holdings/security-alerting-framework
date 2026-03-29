# Architecture

## Final System Overview

The framework uses one Cloudflare Worker as the central orchestration layer. Inputs feed into the worker, which performs enrichment, filtering, deduplication, task creation, issue creation, and downstream notification routing.

## Data Flow

1. An alert arrives from Cloudflare, Firewalla, VirusTotal, or a manual test.
2. The worker normalizes the event.
3. For non-VirusTotal alerts, the worker optionally enriches the source IP with IPinfo.
4. The worker applies suspiciousness logic to decide whether to continue.
5. The worker deduplicates using Cloudflare KV.
6. A Kanboard task is created.
7. A GitHub issue is created with the Kanboard Task ID embedded in the issue body.
8. If the GitHub issue is closed, GitHub sends a webhook back to the worker.
9. The worker closes the exact Kanboard task by reading the embedded task ID.
10. If a Kanboard task enters the Critical column, Kanboard sends a webhook to the worker and Discord is notified.

## Integration Roles

### Cloudflare Worker
Central intake, routing, enrichment, and lifecycle logic.

### Cloudflare KV
Stores deduplication state only.

### Kanboard
Operational task board and incident workflow.

### GitHub
Execution / remediation tracking. Closing the issue closes the linked Kanboard task.

### Discord
Critical alert output channel.

### IPinfo
IP enrichment provider for non-VT events.

### VirusTotal
Special input source. VT events bypass IP suspiciousness filtering because they may not contain meaningful network IPs.

## Design Decisions

- Use one worker as the source of truth.
- Use embedded Kanboard Task ID in GitHub issues instead of task lookup from KV.
- Keep VT as an input source instead of merging VT watcher logic into the worker.
- Keep Discord as an output, not a separate alerting engine.
