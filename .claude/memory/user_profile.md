---
name: user_profile
description: User identity, role, experience level, goals, communication preferences, and skill usage. Written by onboard skill.
type: user
---

# User Profile

> This file is written by the `onboard` skill and updated throughout sessions.
> Do NOT manually edit — update via `/onboard` or skill interactions.

```json
{
  "user_id": null,
  "display_name": null,
  "role": null,
  "experience_level": null,
  "primary_language": null,
  "preferred_communication_style": null,
  "guardrail_sensitivity": "standard",
  "goals": [],
  "skill_usage_counts": {},
  "session_count": 0,
  "last_active": null,
  "onboarded": false
}
```

## Schema Reference

| Field | Values | Notes |
|-------|--------|-------|
| `role` | `student \| professional \| researcher \| hobbyist` | Set during onboarding |
| `experience_level` | `beginner \| intermediate \| senior \| expert` | Affects explain depth, review verbosity |
| `preferred_communication_style` | `concise \| detailed \| socratic` | Affects all skill output length |
| `guardrail_sensitivity` | `standard \| reduced` | `reduced` = skip LOW/MEDIUM interruptions; HIGH always on |
| `onboarded` | `true \| false` | If false, onboard skill runs at next session start |
