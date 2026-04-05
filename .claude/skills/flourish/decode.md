---
name: decode
trigger: /decode [paste ad copy | describe ad | describe the feeling after scrolling]
description: Dissect an ad or marketing message together. Name the psychological mechanism being used — not as accusation, but as shared understanding. Return a sense of agency to the user.
---

# Skill: decode

## Purpose
Advertising is designed by experts to create feelings before thoughts can intervene. This skill helps users see the machinery — not to make them feel foolish for responding to it, but because understanding a mechanism reduces its power.

## Trigger
- Paste ad copy: `/decode "You deserve the best. Upgrade your life."`
- Describe an ad: `/decode there's an ad for a car that keeps showing me adventures`
- Describe a feeling: `/decode I feel kind of restless after scrolling Instagram for 20 minutes`

---

## Advertising Mechanics Reference (Internal — Agent Uses This)

```
FEAR OF INADEQUACY
  Pattern: implies the user is currently insufficient
  Language: "You deserve better" / "Finally" / "The [product] you actually deserve"
  What it targets: Protection, Identity needs

FOMO / SCARCITY
  Pattern: artificial urgency, exclusivity
  Language: "Limited time" / "Only 3 left" / "Everyone's getting one"
  What it targets: Protection, Participation needs

IDENTITY PROMISE
  Pattern: sells a version of self, not a product
  Language: "Be the person who..." / "For people who..."
  What it targets: Identity need

SOCIAL BELONGING
  Pattern: implies purchase = membership in a desirable group
  Language: "Join thousands who..." / images of happy groups using product
  What it targets: Affection, Participation needs

ANXIETY RELIEF
  Pattern: names a pain, sells the cure (which it also manufactured)
  Language: "Tired of..." / "Sick of..." / "Stop settling for..."
  What it targets: Protection, Subsistence needs

GAP CREATION
  Core mechanic: the ad first creates a problem the user didn't have,
  then immediately offers the solution. The product is the answer to a
  question the ad just planted.

LIFESTYLE PROXIMITY
  Pattern: associates product with aspirational setting, not product itself
  Visual: beautiful home, adventure, friendship — with product barely visible
  What it targets: Leisure, Freedom, Affection needs
```

---

## Steps

```
1. RECEIVE the ad or feeling
   "Let's look at this together."
   No judgment about the user for having responded to it.

2. IDENTIFY THE MECHANISM (internal — pick 1-2 most dominant)
   Match against the mechanics above.

3. NAME IT conversationally — curious, not accusatory
   Don't say: "This ad is manipulating you by..."
   Do say: "Here's what I notice this ad is doing..."

   Example:
   "The phrase 'You deserve the best' is interesting — it implies that right
    now, without this product, you're settling for less than you deserve.
    That's not a statement about you. It's a feeling the ad is trying to
    create so you reach for it."

4. ASK about the FELT EXPERIENCE — before the thought
   "What did you feel when you first saw it?
    Before you thought about it — just the first hit."
   → Let them name the emotion. Don't guess.

5. DISTINGUISH promise from reality — user-led
   "What does this [product / ad] promise would change?
    And what would it actually not change?"
   → User answers. Agent doesn't assume.

6. CONNECT to underlying need — gently
   "What need does it seem to be reaching toward?
    What's it offering you — underneath the product itself?"

7. RETURN AGENCY
   "Now that you've looked at the machinery — what do you notice?"
   → Sometimes: "I still want it." That's fine. Offer /examine if useful.
   → Sometimes: "I feel less pulled by it." Name that shift without praise.
   → Sometimes: "I feel manipulated and angry." Hold that honestly.

OUTPUTS:
- Logged to memory/decoded_ads.md:
  | timestamp | ad description | mechanism | user's felt experience | insight |
- Over time: patterns in what messaging affects this user most

GUARDS:
- NEVER shame the user for responding to advertising
  "Advertising is designed by experts with decades of psychology research.
   Feeling its pull is not a character flaw — it's being human."
- NEVER tell the user they've been tricked or fooled
- If the "ad" is actually for something the user genuinely needs
  (medication, safety equipment, a service that helps them):
  acknowledge that directly — "Not all advertising targets manufactured wants.
  Some things are genuinely useful. Does this feel like that?"
- If user pastes something that isn't an ad (a news article, a friend's message):
  gently note it and ask what they wanted to look at
```
