---
name: user_profile
description: User identity, values, flourishing vision, trigger patterns, fundamental needs profile, skill usage, and communication preferences. Written by welcome skill, updated throughout sessions.
type: user
---

# User Profile

> Written by the `welcome` skill. Updated by examine, pattern, and flourish skills.
> Values and vision are captured in the user's own words — never paraphrased by the agent.

```json
{
  "user_id": null,
  "display_name": null,
  "mode": "individual",
  "onboarded": false,
  "session_count": 0,
  "last_active": null,

  "values": [],
  "flourishing_vision": null,

  "trigger_patterns": {
    "confirmed": [],
    "suspected": [],
    "time_patterns": []
  },

  "fundamental_needs_profile": {
    "subsistence": null,
    "protection": null,
    "affection": null,
    "understanding": null,
    "participation": null,
    "leisure": null,
    "creation": null,
    "identity": null,
    "freedom": null
  },

  "pause_settings": {
    "default_duration_hours": 72,
    "active_pauses": []
  },

  "skill_usage_counts": {},

  "communication_preferences": {
    "response_length": "moderate",
    "question_style": "one_at_a_time",
    "check_in_frequency": "as_needed",
    "flourish_last_area": null
  }
}
```

## Schema Notes

| Field | Values | How Set |
|-------|--------|---------|
| `values` | User's own phrases from welcome Q1 | welcome skill |
| `flourishing_vision` | User's verbatim Q1 answer | welcome skill |
| `trigger_patterns.confirmed` | stress / boredom / loneliness / social_comparison / fatigue / habit / other | examine + pattern skills |
| `trigger_patterns.time_patterns` | e.g. sunday_evenings, after_work | pattern skill |
| `fundamental_needs_profile` | Notes from needs-map sessions | needs-map skill |
| `check_in_frequency` | weekly / as_needed / never | user preference |
| `flourish_last_area` | body / connection / creation / meaning / rest | auto-rotated by flourish skill |
