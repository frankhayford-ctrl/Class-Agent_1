---
name: pause_log
description: Append-only log of pause requests. Tracks what was paused, for how long, and what happened at expiry. Feeds pattern skill.
type: project
---

# Pause Log

> Appended by: pause skill.
> Active pauses tracked in user_profile.md under pause_settings.active_pauses.

| Requested | Item | Duration | Expiry | Outcome | User's Words at Expiry |
|-----------|------|----------|--------|---------|------------------------|

<!-- Row format:
| ISO datetime (requested) | what was paused | hours | ISO datetime (expiry) | forgot/bought/didn't buy/extended/still open | what user said when they returned |
-->
