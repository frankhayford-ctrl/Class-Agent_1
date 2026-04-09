# Enough — Anti-Consumerism Support Agent

A prototype AI agent that helps individuals and communities examine their wants,
counter advertising influence, and make more conscious consumption choices.
Built on **Claude Code** and **Entire CLI**.

---

## What It Does

**Enough** is a conversational agent you run inside Claude Code. When you bring
it a purchase you're thinking about, it helps you figure out what's actually
driving the desire — genuine need, boredom, stress, an ad you saw, social
pressure — and then offers practical alternatives before you spend.

It does not moralize or shame. When you ask for a recommendation, it gives one.
The goal is human flourishing, not deprivation.

---

## Prerequisites

Install both tools before cloning this repo.

### 1. Claude Code

Claude Code is Anthropic's official CLI for Claude. You need an Anthropic API
key to use it.

**Install:**
```bash
npm install -g @anthropic-ai/claude-code
```

**Authenticate:**
```bash
claude
```
Follow the prompts to log in with your Anthropic account or paste an API key.

> Claude Code requires Node.js 18+. Check with `node --version`.

### 2. Entire CLI

Entire manages session checkpoints and hooks for Claude Code.

**Install (requires Go):**
```bash
go install github.com/entire-dev/entire@latest
```

Confirm it's on your PATH:
```bash
entire --version
```

> If you don't have Go, install it from https://go.dev/dl/ first.

---

## Setup

```bash
# 1. Clone the repo
git clone https://github.com/frankhayford-ctrl/Class-Agent_1.git
cd Class-Agent_1

# 2. That's it — no npm install, no build step.
#    The agent is pure configuration and markdown.
```

---

## Running the Agent

```bash
claude
```

That's the full command. Claude Code reads `CLAUDE.md` automatically on start,
which loads the agent's identity, session-start logic, and all behavioral rules.

**What happens on first run:**
- The agent detects no user profile exists
- It runs the **welcome** skill — asks you 3 questions about your values and
  what a good life looks like to you
- It saves your answers to `.claude/memory/flourish/user_profile.md`
- From then on, every session starts where you left off

---

## How to Use It

Talk to it like a person. You can also use slash commands to invoke specific skills.

### Bring a want
```
I keep thinking about buying a new laptop
```
```
/examine I want to buy AirPods
```
The agent will ask what's driving it, then offer practical alternatives.

### Decode an ad
```
/decode "Finally, a mattress that respects you." — what is this ad doing?
```
The agent names the psychological mechanism being used.

### Ask for a pause
```
/pause standing desk 72h
```
The agent holds the item for 72 hours and checks back in with you.

### Check in on your whole life
```
/flourish
```
Weekly check-in rotating through: body, connection, creation, meaning, rest.

### Work through a community decision
```
/circle Should we get a shared car?
/commons power tools
```
Facilitated group reflection. Works best with 2–4 people in the same session.

### Celebrate a conscious choice
```
/celebrate I decided not to buy it
/celebrate I bought it and it was exactly right
```
Both are worth noting. The metric is awareness, not abstinence.

### Full skill list

| Command | What it does |
|---------|-------------|
| `/welcome` | Re-run onboarding |
| `/examine [want]` | Look at a specific want |
| `/decode [ad or feeling]` | Dissect an ad's mechanism |
| `/needs` | Map a want to a fundamental human need |
| `/reframe` | Get 3 non-purchase paths to the same need |
| `/pattern` | Surface your own trigger patterns over time |
| `/gratitude` | Take stock of what you already have |
| `/flourish` | Check in on how your whole life is going |
| `/pause [item] [duration]` | Hold a waiting space (default: 72h) |
| `/circle [topic]` | Community reflection (multi-user) |
| `/commons [item]` | Decide: shared vs. individual ownership |
| `/celebrate [decision]` | Mark a conscious choice |

---

## Project Structure

```
Class-Agent_1/
├── CLAUDE.md                        ← Agent identity + session-start logic
│                                      (Claude Code reads this automatically)
├── .claude/
│   ├── settings.json                ← Hooks config (Entire integration)
│   ├── skills/flourish/             ← Skill workflow files (12 skills)
│   │   ├── welcome.md
│   │   ├── examine.md
│   │   ├── decode.md
│   │   ├── needs-map.md
│   │   ├── reframe.md
│   │   ├── pattern.md
│   │   ├── gratitude.md
│   │   ├── flourish.md
│   │   ├── pause.md
│   │   ├── circle.md
│   │   ├── commons.md
│   │   ├── celebrate.md
│   │   └── session-start.md         ← Reference doc (logic lives in CLAUDE.md)
│   └── memory/flourish/             ← Per-user memory (gitignored in real use)
│       ├── MEMORY.md                ← Index
│       ├── user_profile.md          ← Your values, triggers, preferences
│       ├── wants_log.md             ← Every want examined (append-only)
│       ├── decoded_ads.md           ← Ads decoded
│       ├── flourish_log.md          ← Check-in history
│       ├── decisions_log.md         ← Conscious decisions
│       ├── pause_log.md             ← Pause history
│       └── patterns.md              ← Your trigger patterns
├── .entire/
│   └── settings.json                ← Entire CLI config
└── data/flourish/                   ← Example data for the prototype
    ├── interaction_sequences.md     ← Annotated example conversations
    └── users/                       ← Example user profiles (JSON)
```

---

## How It Works (Technical)

**`CLAUDE.md`** is the core. Claude Code reads it at every session start before
doing anything else. It contains:
- The agent's identity and behavioral rules (always active)
- Session-start decision logic (new user? expired pause? open thread?)
- The rule that blocks development skills from being invoked

**Skills** are markdown files in `.claude/skills/flourish/`. The agent reads
them with the Read tool and follows their steps. They are not registered
executables — they are instructions that Claude reads and acts on.

**Memory** is plain markdown files in `.claude/memory/flourish/`. The agent
reads and appends to these across sessions. All logs are append-only.

**Hooks** in `.claude/settings.json` connect to Entire CLI for session
checkpointing. Entire creates named snapshots of session state that can be
rolled back to.

---

## Known Prototype Limitations

- **Memory is local.** The `.claude/memory/` files are stored on your machine.
  There is no sync, no cloud storage, no multi-device access.
- **No authentication.** Anyone with access to the repo directory can read
  your memory files.
- **Community mode is single-session.** `/circle` and `/commons` work when
  multiple people are in the same Claude Code session. There is no async
  multi-user support yet.
- **Session continuity depends on the same directory.** The agent remembers
  you only if you run `claude` from the same project directory each time.

---

## Example Conversation

```
You:    I keep thinking about buying a $300 espresso machine.
        I've seen the ad everywhere.

Enough: What does the ad make it seem like having it would give you?

You:    Like my mornings would feel more intentional. More mine.

Enough: So it's less about coffee and more about having a morning that
        feels like yours — something you chose, not just reacted to.

        Is the rushed morning a coffee problem, or more of a
        schedule problem?

You:    ...schedule, honestly. I keep setting my alarm later.

Enough: The machine can give you a ritual, but it can't give you
        the time. The ad is selling a solution to a problem it's
        not actually solving.

        Three options, no commitment required:
        — Set your alarm 20 minutes earlier tomorrow. Make whatever
          you have now, slowly, without your phone. See what it
          actually feels like.
        — Look at what you already have. Is there something in your
          kitchen you could use differently?
        — If you still want it in a week, it might be worth getting.
          Want me to hold a 72-hour pause on it?
```

---

## Contributing

This is a class prototype. The design docs (skills, user data, interaction
sequences) are in `data/flourish/` and `.claude/skills/flourish/`. Start there
if you want to understand the agent's intended behavior before changing anything.
