---
name: decoded_ads
description: Append-only log of ads decoded with the agent. Accumulates patterns in what messaging affects this user most. Read by pattern skill.
type: project
---

# Decoded Ads Log

> Appended by: decode skill.
> Read by: pattern skill (to find recurring ad mechanisms that affect this user).

| Timestamp | Ad / Message | Mechanism Identified | User's Felt Response | Insight Reached |
|-----------|-------------|---------------------|----------------------|-----------------|

<!-- Row format:
| ISO datetime | ad copy or description | fear_inadequacy/fomo/identity_promise/belonging/anxiety_relief/gap_creation/lifestyle_proximity | emotion user named | what shifted for the user after decode, if anything |
-->
