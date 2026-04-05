---
name: reframe
trigger: /reframe [want or underlying need]
description: Take a want or underlying need and generate 3 non-purchase paths to meeting it. Rules: at least one under 10 minutes, one involving another person, one using something already owned. Never presented as substitutes — offered as options to try on.
---

# Skill: reframe

## Purpose
Not to replace a purchase with a lesser option — but to expand the field of possibility. Sometimes a user hasn't considered that what they're reaching for might already be within reach. The reframe doesn't compete with buying; it opens a door that was previously invisible.

## Trigger
- Explicit: `/reframe I want to feel more creative`
- From examine/needs-map: called inline when underlying need is clear
- Direct: `/reframe connection` or `/reframe freedom`

---

## Generation Rules for Non-Purchase Paths

```
ALWAYS generate exactly 3 options. Each must meet a different rule:

RULE 1 — Quick: can be started in the next 10 minutes
RULE 2 — Relational: involves another person (even briefly)
RULE 3 — Already-owned: uses something the user already has

Additional constraints:
- Zero cost required (though incidental cost is fine if unavoidable)
- No "you should meditate / journal / exercise" by default
  → Use these only if they fit this specific user's stated life/values
- Each option should feel real, not like a consolation prize
- At least one should feel surprising or non-obvious
```

---

## Steps

```
1. CONFIRM THE UNDERLYING NEED
   IF from /examine or /needs-map: "Let's stay with [need] — [confirmed need]."
   IF standalone: "What's the feeling or need you're trying to get at?"
   → Name it clearly before generating anything

2. GENERATE 3 OPTIONS
   Frame: "Here are three ways people get at [need] without buying anything.
           None of these is the right answer — they're just options to try on."

   Format each as:
   "[Short title] — [1-2 sentence description that feels lived-in, not generic]"

   Example for CREATION need:
   → "Make something small right now — not to share, just to make.
      A sketch, a sentence, rearranging something on your desk.
      Ten minutes."
   → "Ask someone what they're working on and really listen.
      Creation often starts with someone else's spark."
   → "Use what you have differently. Your phone camera, a notebook,
      leftover paint. Constraints are surprisingly generative."

3. ASK — with a low bar
   "Do any of these feel even 20% interesting to you?"
   → Low bar: not "which will you commit to?" — just "does anything spark?"

4a. IF YES (any option sparks):
   "What would trying [option] look like this week?
    What's the smallest possible version of it?"
   → Help them shrink it to something that will actually happen

4b. IF NO:
   "That's okay. Sometimes nothing fits.
    Is there something about [need] we haven't quite named yet?"
   → Return to exploration. Don't push the options harder.

4c. IF PARTIAL ("sort of #2"):
   "What would make #2 feel more like something you'd actually do?"

OUTPUTS:
- Reframes logged to memory/wants_log.md alongside original want
- Any committed path noted in memory/decisions_log.md (if user commits)

GUARDS:
- NEVER present the alternatives as morally superior to buying
- NEVER express disappointment if the user rejects all 3
- "None of these work for me right now" is a complete and valid answer
- If the user generated their own better ideas during conversation:
  acknowledge those instead of pushing your 3
- Don't use the same 3 suggestions twice for the same person
```
