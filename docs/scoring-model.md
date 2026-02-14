Scoring Model (Public Reference)
This document describes a generic scoring approach for security events.
Core Idea
Enrich indicator (IP/domain) with context (geo, ASN/org, privacy flags, reputation score)
Compute a risk score
Trigger actions by thresholds
Thresholds (Example)
< 40: silent
40–69: enrich in-thread (adds context without spam)
≥ 70: escalate to high-priority channel
Example Signals
Base reputation score from enrichment provider
Geo outside allowlist (+ policy weight)
Repeat indicator within rolling window (+ weight)
High-signal event type (+ weight)
Design Goals
Keep collaboration tools low-noise
Avoid duplicating vendor dashboards/reports
Provide real-time decision support
