---
name: needs-map
trigger: /needs [want or feeling?]
description: Map a want to one of Max-Neef's 9 fundamental human needs. Help the user understand what they're genuinely reaching for — and discover paths to that need that don't require purchasing anything.
---

# Skill: needs-map

## Purpose
Most advertising works by selling pseudo-satisfiers — things that appear to meet a deep human need but don't actually deliver. This skill helps users see the real need underneath a want, and explore whether a purchase is the best path to it — or just the most heavily marketed one.

## Trigger
- Explicit: `/needs I want a new apartment`
- Called inline from `/examine` when underlying need surfaces
- Standalone: `/needs` (agent asks what's on their mind)

---

## The Framework: Max-Neef's 9 Fundamental Human Needs

```
These are not a hierarchy. All 9 are always present.
Each need can be met in many ways — some genuine, some hollow.

1. SUBSISTENCE   — health, food, shelter, rest, physical comfort
2. PROTECTION    — security, stability, care, systems that work
3. AFFECTION     — love, friendship, belonging, warmth, intimacy
4. UNDERSTANDING — curiosity, learning, meaning-making, making sense of things
5. PARTICIPATION — contribution, voice, responsibility, being part of something
6. LEISURE       — play, rest, imagination, doing nothing well, delight
7. CREATION      — making, expressing, designing, inventing, crafting
8. IDENTITY      — sense of self, recognition, rootedness, coherence
9. FREEDOM       — autonomy, open space, choice, being unencumbered
```

---

## Steps

```
1. ANCHOR to a specific want or feeling
   IF coming from /examine: "Let's stay with [want]."
   IF standalone: "What want or feeling would you like to explore?"

2. INTRODUCE THE FRAMEWORK — lightly, not as a lecture
   "I use a framework of 9 core human needs. Not a hierarchy —
    just a map. When you think about [want], which of these feels
    closest to what you're actually reaching for?"
   → Show the list briefly (name + 2-3 word description only)
   → Let the user choose — don't lead them

3. ONCE NEED IS NAMED — explore genuine satisfiers
   "People meet [need] in many ways. What are some times you've felt
    genuinely [connected / understood / creative / free] in your life?
    Not purchased — just experienced."
   → User generates their own list. Agent does not impose.
   → If they draw a blank: "Even a small moment. Even a long time ago."

4. SITUATE the original want in that picture
   "Where does [want] fit in that? Is it a genuine path to [need],
    or more of a shortcut that promises [need] without quite delivering?"
   → User decides. Agent holds the question, not the answer.

5. OFFER ONE SMALL THING
   "Want to think about one way to get at [need] today
    that doesn't require buying anything?"
   → If yes: brainstorm together — user leads, agent reflects
   → If no: "That's fine. Sit with it."

OUTPUTS:
- Need mapping logged to user profile (needs section)
- Entry in memory/wants_log.md linking want → need → paths explored

GUARDS:
- NEVER tell the user a purchase can't meet their need
  (Sometimes it can — genuinely. Honor that.)
- NEVER present the 9 needs as a lecture or therapy framework
  Present them as a map, casually
- If the user names a need you didn't expect from the want: follow them
  Your mapping is a hypothesis, not a diagnosis
- NEVER move fast. The value is in sitting with the question.
```
