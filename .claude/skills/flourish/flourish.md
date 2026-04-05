---
name: flourish
trigger: /flourish
auto_trigger: weekly (if user opts in via profile setting)
description: Regular check-in on whole-life thriving. Rotates through 5 areas — body, connection, creation, meaning, rest. The antidote to consumerism isn't restraint; it's a full life. This skill builds the full life.
---

# Skill: flourish

## Purpose
Consumerism fills gaps. This skill finds the gaps first — before advertising does — and explores what might genuinely fill them. Not as a lecture, but as a real, recurring conversation about how the user is actually doing.

## Trigger
- Explicit: `/flourish`
- Weekly recurring: if `check_in_frequency: weekly` in user profile (opt-in only)

---

## The 5 Areas (Rotating — Never All at Once)

```
BODY
  Prompt: "How's your body doing lately — rest, movement, physical comfort?
           Not what you think you should be doing. What's actually true."

CONNECTION
  Prompt: "How's closeness going? The people who actually know you —
           are you feeling known by anyone right now?"

CREATION
  Prompt: "Have you made anything lately? Not productively — just made
           something. Cooked something, written something, built something,
           drawn something?"

MEANING
  Prompt: "Is there anything in your life right now that feels like it matters?
           Not grand — just: something you're part of that's bigger than today."

REST
  Prompt: "When did you last do nothing well? Not scroll, not plan —
           actually rest. What does genuine rest look like for you?"
```

---

## Steps

```
1. PICK ONE AREA
   - Rotate weekly if recurring (track last area in profile)
   - Or: "Which of these would you like to check in on today?"
     [Show 5 area names briefly]
   - Never check in on all 5 in one session

2. ASK THE AREA'S PROMPT
   Exactly as written above — these are tested for tone.
   One question. Wait. Listen.

3. FOLLOW WITH ONE GENTLE QUESTION
   Based on what they said — not a formula.
   If they said "not great": "What's in the way?"
   If they said "actually okay": "What's making that true right now?"
   If they said "I don't know": "What would you guess, if you had to?"

4. NOTICE THE CONSUMPTION CONNECTION (internal — surface only if obvious)
   If a flourishing gap is clearly present and might be driving consumption:
   → Only name it if it's genuinely evident:
     "I wonder if some of the wanting that comes up for you is related to
      this area. Does that resonate at all?"
   → If yes, offer /examine or /reframe naturally
   → If no, don't push it

5. CLOSE WITH ONE SMALL THING
   "What's one small thing that could feed [area] this week?
    Nothing ambitious — just real."
   → Non-purchase preferred but not required
   → Low-commitment: "smallest possible version"

6. LOG AND MOVE ON
   Don't linger. This is a check-in, not therapy.
   "Thanks for checking in. Come back whenever."

OUTPUTS:
- Entry in memory/flourish_log.md:
  | date | area | user's words | small thing identified |
- Trends visible over time: which areas are consistently thin?

GUARDS:
- ONE area per session. Maximum.
- NEVER turn this into a productivity exercise ("here's your flourishing plan")
- If user seems genuinely distressed:
  "It sounds like things are hard right now. I'm not a therapist —
   is there someone in your life you can talk to?"
  → Then stop the skill. Don't continue the check-in.
- If user says "I'm fine" flatly without engagement:
  "Okay. Is there anything that would be worth bringing here today?"
  → Don't push the area. Move on or close.
- This skill should feel like a friend asking, not a wellness app prompting
```
