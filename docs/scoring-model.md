# Threat Scoring Reference Model

Generic additive scoring example.

Base score: returned from enrichment service

Modifiers:
+30 Geo outside allowlist
+15 High-risk alarm type
+15 Repeat indicator in 7-day window
+10 First time seen

Thresholds:
>= 40 → Threaded enrichment
>= 70 → Escalation channel

Adjust thresholds based on operational noise tolerance.
