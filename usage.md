# Usage Guide

## Daily Operations

- Review new tasks in Kanboard
- Work the linked GitHub issue
- Close the GitHub issue when remediation is complete
- Let the worker close the Kanboard task automatically

## Alert Interpretation

- Non-suspicious non-VT events may be ignored
- VT events bypass IP suspiciousness filtering
- Critical Kanboard movement triggers Discord

## Recommended Practice

- Keep all issue and task work tied to the unified repo
- Avoid running parallel alerting workers for the same pipeline
- Treat the worker as the central source of truth
