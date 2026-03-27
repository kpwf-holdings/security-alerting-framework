# Testing Guide

## Send Test Alert (PowerShell)

Invoke-RestMethod -Method POST `
  -Uri "YOUR_WORKER_URL" `
  -Headers @{ "Content-Type" = "application/json" } `
  -Body '{ "action": "block", "ray_id": "test-001", "severity": "medium" }'

## Expected Flow

1. Kanboard task created
2. GitHub issue created
3. Close GitHub issue
4. Task moves to Resolved

## Verify via API

Use getTask to confirm:
- column_id = resolved
- is_active = 0
