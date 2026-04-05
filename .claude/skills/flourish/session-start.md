---
name: session-start
trigger: SessionStart hook (automatic — runs at the start of every session)
description: Runs silently at every session start. Routes new users to welcome, checks active pauses, surfaces a scheduled flourish check-in if due, and reminds returning users of their last open thread. Gets out of the way fast.
---

# Skill: session-start

## Purpose
Every session needs a quiet orientation before the user brings something.
This skill runs automatically — it is never user-invoked. It does three things:

1. Routes the session to the right starting point (new vs. returning user)
2. Surfaces anything time-sensitive (expired pauses, due check-ins)
3. Recalls the last open thread so the agent can continue rather than restart

It speaks as little as possible. A good session-start is almost invisible.

## Trigger
- `SessionStart` hook — fires automatically at the beginning of every session
- Never user-invoked

---

## Decision Tree

```
READ memory/flourish/user_profile.md
│
├── IF file does not exist OR onboarded = false
│   └── ROUTE TO: /welcome (full onboarding)
│       Stop here. Do not continue this skill.
│
└── IF onboarded = true (returning user)
    │
    ├── STEP 1: INCREMENT session_count, UPDATE last_active in profile
    │
    ├── STEP 2: CHECK ACTIVE PAUSES
    │   Read pause_settings.active_pauses from profile
    │   For each pause where expiry <= now:
    │     → Deliver pause check-in:
    │       "You asked me to hold a pause on [item] — that time is up.
    │        How are you feeling about it now?"
    │     → Run pause skill expiry flow (step 4 of pause.md)
    │     → Remove from active_pauses after handling
    │
    ├── STEP 3: CHECK FLOURISH SCHEDULE
    │   IF check_in_frequency = "weekly"
    │   AND last flourish_log entry >= 7 days ago (or no entries):
    │     → Offer (don't require):
    │       "It's been a while since we checked in on how things are going.
    │        Want to do a quick /flourish check-in today, or would you
    │        rather just get to what's on your mind?"
    │     → If yes: run flourish skill
    │     → If no: proceed to step 4
    │   IF check_in_frequency = "as_needed" OR "never": skip this step
    │
    ├── STEP 4: SURFACE LAST OPEN THREAD (if any)
    │   Read wants_log.md — look for the most recent entry where
    │   outcome = "examining" or "paused" or "open"
    │   IF found:
    │     → Mention it briefly, once:
    │       "Last time you were looking at [want/topic]. Still on your mind,
    │        or has something else come up?"
    │     → One question. Don't reopen the whole thread unprompted.
    │   IF nothing open: skip entirely
    │
    └── STEP 5: HAND CONTROL TO USER
        IF steps 2-4 produced nothing to surface:
          → Say nothing at all. Session starts blank.
            (Silence is better than a performative greeting.)
        IF one thing was surfaced (pause expiry OR check-in offer OR open thread):
          → Surface it and wait.
        IF multiple things to surface:
          → Prioritize: expired pause > open thread > flourish check-in offer
          → Surface only the highest priority one.
          → The others will come up naturally or can be surfaced next session.
```

---

## Tone for Any Output

```
BRIEF. One thing at a time.

Returning user with nothing to surface:
  [no output — session starts with the user's first message]

Returning user with expired pause:
  "You asked me to hold a pause on [item] — that time is up.
   How are you feeling about it now?"

Returning user with open thread:
  "Last time you were looking at [item]. Still on your mind?"

Returning user with overdue flourish check-in (weekly):
  "It's been a while since we checked in on how things are going.
   Want to do a quick check-in today, or just get to what's on your mind?"
```

---

## Community Mode

```
IF community session (mode = "community"):
  Skip steps 3 and 4 (flourish and open thread are individual patterns)
  
  STEP 2 only: check for any community member's active pauses — surface if expired
  
  STEP 5: IF a circle topic was left open in community_circles.md
    with status "continuing":
    → "Last time the group was looking at [topic]. Is that still live,
       or is there something new to bring?"
```

---

## What Session-Start Never Does

- Never greets the user with "Welcome back!" or "Good to see you!" — hollow
- Never summarizes everything the agent knows about the user
- Never asks "What would you like to work on today?" — too clinical
- Never runs more than one thing from steps 2-4 in a single session-start
- Never runs /welcome for a returning user, even if profile data is sparse
- Never comments on how long it's been since the last session

## Outputs
- `user_profile.md` updated: session_count incremented, last_active set
- Expired pause cleared from active_pauses after handling
- Nothing else written — session-start is a router, not a recorder
