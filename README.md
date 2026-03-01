# security-alerting-framework

A sanitized, public-facing reference architecture for routing security events through a serverless edge worker, enriching suspicious indicators, and conditionally escalating alerts using Slack.

This repository contains no production secrets, URLs, or internal identifiers.
It demonstrates architecture patterns only.

---

## Overview

Event Source (Firewall / Edge / API)
        ↓
Serverless Router (Edge Worker Pattern)
        ↓
Primary Alert Channel (Slack)
        ↓
Conditional Threat Intelligence Enrichment (Threaded Reply)
        ↓
Escalation Channel (if risk threshold exceeded)

---

## Design Goals

- Low-noise alerting
- Threshold-based enrichment
- Threaded contextual intelligence
- Minimal state using KV-style memory
- Separation between routing and enrichment layers

---

## Core Components

### Event Router
- Accept authenticated POST events
- Normalize payload structure
- Extract indicators (IP or domain)
- Post base alert to Slack
- Invoke enrichment service

### Threat Intel Service Pattern
- Accept indicator via POST `/enrich`
- Return structured risk data:
  - score
  - country
  - ASN / org
  - privacy flags

### Conditional Escalation
- Thread enrichment when score >= 40
- Escalate when score >= 70

### 7-Day Indicator Memory
Tracks:
- first_seen_ms
- last_seen_ms
- count_7d
- last_score
- last_country

---

## Example Event

{
  "type": "abnormal_upload",
  "device": "Endpoint-01",
  "message": "Outbound data to 8.8.8.8",
  "timestamp": "2026-03-01T14:00:00Z"
}

---

## Example Enrichment Response

{
  "ok": true,
  "score": 55,
  "country": "NL",
  "org": "Example Hosting Provider",
  "privacy": {
    "hosting": true,
    "vpn": false,
    "tor": false
  }
}

---

## Scoring Reference

Allowlist example: US, CA, GB, AU, NZ

Modifiers (illustrative):
+30 Geo outside allowlist
+15 High-risk alarm type
+15 Repeat indicator (>=3 in 7 days)
+10 First time seen

Thread threshold: 40
Critical threshold: 70

---

## Technology Pattern

- Edge compute (Workers model)
- Slack Web API
- KV-style memory
- JSON service authentication

---

## Production Hardening (Not Included Here)

- Secret bindings for tokens
- Strict header validation
- Rate limiting
- Structured logging
- Environment separation
