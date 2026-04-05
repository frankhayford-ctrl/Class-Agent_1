---
name: pattern
trigger: /pattern
auto_trigger: after 5+ entries in wants_log.md (asks permission before surfacing)
description: Surface the user's own recurring trigger patterns over time. Always asks permission before sharing. Presents patterns as observations, never diagnoses. User interprets their own data.
---

# Skill: pattern

## Purpose
Over time, the wants_log builds a picture. People are often surprised to see their own patterns made visible — not because they're shameful, but because they were invisible. This skill returns that picture to the user so they can interpret it themselves.

## Trigger
- Explicit: `/pattern`
- Auto-prompt: when wants_log.md has 5+ entries, agent notices at session start:
  "I've noticed some patterns in the things you've brought here lately.
   Want me to share what I see?" (User must say yes before anything is shown.)

---

## Pattern Types to Detect

```
TIME PATTERNS
  - Day of week clustering (Sunday evenings, Friday afternoons)
  - Time of day (late night, post-work, early morning)
  - Seasonal / monthly patterns

EMOTIONAL TRIGGER PATTERNS
  - After stress / hard days / difficult conversations
  - During boredom or low stimulation
  - After social comparison (following social media use)
  - When tired or depleted

CATEGORY PATTERNS
  - Always the same domain (tech, clothing, home, food)
  - Upgrades of things already owned
  - "Just one more" of a category already well-stocked

RESOLUTION PATTERNS
  - Does the user tend to buy after examining?
  - Does the want disappear after a pause?
  - Does reflection consistently lead to not buying,
    or is it functioning as ritual permission? (See N5)

NEED PATTERNS
  - Which fundamental needs appear most often?
  - Which needs appear to be chronically undermet?
```

---

## Steps

```
1. ALWAYS ASK PERMISSION FIRST
   Never surface patterns without explicit yes.
   "I've noticed some things looking back at what you've brought here.
    Want me to share what I see?"
   → IF no: "Of course. It's here whenever you want it."
   → IF yes: proceed

2. READ memory/wants_log.md
   Extract: timestamps, triggers, categories, needs mapped, outcomes

3. IDENTIFY DOMINANT PATTERNS (1-2 most clear — not all at once)
   Start with the single most evident pattern.
   Never present a list of 6 findings.

4. SHARE WITH CURIOSITY — not clinical, not diagnostic
   Frame: "I noticed something..." not "You have a pattern of..."

   Example:
   "It looks like you tend to bring things here on Sunday evenings —
    about 9 of the last 12 things came in on Sundays.
    Does that match your experience?"

5. LET THE USER INTERPRET
   "What's usually going on for you on Sunday evenings?"
   → Don't name the emotion for them. They name it.
   → If they name something ("I'm usually lonely then"):
     "Yeah. That tracks with what you brought. What do you notice about that?"

6. OFFER ONE THING — not a fix, a question
   "Now that you see this — is there anything you want to do with it?
    Or is it just useful to know?"
   → Both answers are fine. Insight is the output, not change.

7. IF RESOLUTION PATTERN DETECTED (rubber-stamp pattern, N5):
   Handle with particular care. See N5 sequence.
   Frame: "This might be working exactly as you want it to.
           Or it might have become a ritual that doesn't serve you.
           Only you know which."

OUTPUTS:
- Pattern summary written to memory/patterns.md (with timestamp)
- User's own interpretation noted alongside agent observation

GUARDS:
- ALWAYS ask permission first — never dump a pattern analysis unsolicited
- Present ONE pattern at a time. Stop there unless user asks for more.
- NEVER say "You shop when you're sad" — too diagnostic, too reductive
- DO say "I notice this comes up more at certain times" — then let them fill it in
- If user disagrees with the pattern: believe them
  "You know yourself better than I can from a log. What do you see instead?"
- Patterns are observations about behavior, not character
```
