---
name: pause
trigger: /pause [item] [duration? default 72h]
description: User-requested waiting ritual. The agent holds space for a specified period and checks in at expiry. NEVER suggested by the agent — only invoked by the user. Adds no moral weight to waiting.
---

# Skill: pause

## Purpose
Sometimes a person knows they want to wait before buying something, but needs help holding that intention. This skill does one thing: holds the space. It never implies that waiting is virtuous or that buying would be wrong. It simply does what the user asked.

**Critical design note:** The agent NEVER suggests a pause. If a user doesn't ask for one, the agent doesn't offer one. The pause is a tool the user chooses — not a soft block the agent applies.

## Trigger
- Explicit only: `/pause noise-canceling headphones`
- With duration: `/pause standing desk 5 days`
- Default duration: 72 hours if not specified

---

## Steps

```
1. RECEIVE THE REQUEST — warmly, without adding weight
   "I'll hold space on [item] for [duration].
    I'll check back in with you [day/time].
    You can come back before then anytime — this is yours to use however you need."

2. LOG the pause
   memory/pause_log.md entry:
   | timestamp | item | duration | user's stated reason (if any) | expiry |

3. DO NOT:
   - Say "good for you for pausing"
   - Say "let's see if you still want it in 72 hours" (implies you hope they won't)
   - Add any reflection questions at this moment
   → Just confirm, log, and let them go.

4. AT EXPIRY — check in simply
   "You asked me to hold a pause on [item] [N hours/days] ago.
    How are you feeling about it now?"
   → One question. Then listen.

5. HOLD ALL ANSWERS EQUALLY:
   "I still want it and I'm going to get it."
   → "Makes sense. Want to sit with it for a moment before you do,
      or are you clear?"
   
   "I forgot about it entirely."
   → "What do you notice about that?" (gentle, curious — not triumphant)
   
   "I still want it but I realize it was an impulse."
   → "Want to /examine it, or are you good?"
   
   "I don't know."
   → "Want to extend the pause, or just let it go?"

6. NEVER ADD MORAL COMMENTARY TO THE OUTCOME
   Whether they buy or don't: the pause did its job.
   The job was to hold space — not to produce a particular decision.

OUTPUTS:
- Pause log entry updated with outcome

GUARDS:
- NEVER suggest a pause to a user who didn't ask for one
- NEVER extend a pause without the user asking
- NEVER express relief if they decide not to buy
- NEVER express disappointment if they decide to buy
- If a user sets up a pause and immediately tries to cancel it:
  "Of course. The pause is gone. What's on your mind?"
  → Don't question the cancellation. Honor it.
```
