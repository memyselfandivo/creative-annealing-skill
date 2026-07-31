---
name: creative-annealing
description: Runs a structured, simulated-annealing-style ideation process — wide divergent exploration (including ideas that deliberately work against the stated goal) followed by staged elimination rounds down to exactly 3 final ideas, each round's survivors justified. Trigger ALWAYS when the user says "creative-annealing", with or without further detail (topic, starting count). Partial or missing info (topic only, count only, or just the bare trigger word) still triggers this skill — resolve missing pieces via the intake questions below. Do NOT trigger for generic creativity/brainstorming requests that don't use this specific trigger term.
---

# Creative Annealing

A multi-round ideation process modeled on simulated annealing: generate ideas at "high temperature" (wide, unfiltered, including ideas that run counter to the goal), then "cool" through elimination rounds that transform rather than just filter, converging on exactly 3 ideas. Every surviving idea carries a reason; nothing is discarded without a visible trail the user can revisit later.

## 1. Trigger handling

On seeing "creative-annealing":

- **Full form** (trigger + topic + starting count all present): skip intake questions, go straight to Step 2 (clarification).
- **Bare trigger** (topic and/or count missing): ask only for what's missing, one question at a time:
  1. "What idea or problem is this about?"
  2. "How many ideas should the exploration round start with?" — if asked for a recommendation, suggest **7** (below that there's no real intermediate elimination round before the mandatory final round of 3, so 7 keeps the staged process meaningful).

## 2. Clarification

Before exploring, briefly clarify only what's genuinely unclear:
- The concrete problem/topic
- Relevant constraints, target audience, context of use

Also determine (silently — not necessarily by asking the user):
- **Goal direction**: the obvious, conventional direction a solution would take
- **Opposite direction**: its plausible opposite

Not every goal has a clean opposite — for abstract goals it may feel somewhat constructed. Pick a reasonable one and move on rather than searching for a perfect fit.

## 3. Exploration round (high temperature)

Generate exactly N ideas (N = starting count). No evaluation, no filtering, no self-censoring — weak, extreme, or impractical-looking ideas belong here too.

Spread the N ideas across three directions relative to the goal (~25/50/25, approximate — doesn't need to divide evenly):

- **Counter-direction (~25%)**: ideas that explicitly work AGAINST the goal or pursue its opposite. Example — goal "attract more young customers": ideas that explicitly serve an older audience, or actively avoid attracting new customers.
- **Creative-lateral (~50%)**: broadly creative ideas off the direct path — neither clearly toward the goal nor clearly against it. Vary this bucket internally too: some can push to an extreme within the goal's own domain, others can come from an entirely different domain. No need to label the split — just make the ideas themselves genuinely different from each other.
- **Goal-direction (~25%)**: the conventional creative ideas a normal brainstorm would produce anyway.

This distribution IS the point of the exploration round. A round where nearly every idea sits in the goal-direction bucket (just increasingly polished variations of the same thing) has missed the method's core idea.

For EVERY idea, give:
- **Idea**: short, concrete
- **Direction**: one of the three (Counter-direction / Creative-lateral / Goal-direction)
- **Approach**: one sentence naming the underlying strategy (e.g. "reversing user expectations", "combining two unrelated industries", "radical simplification", "analogy from nature") — this is the anchor the user can later reference for a discarded idea.

## 4. Round plan

Compute the full round plan once, right after exploration, and show it (e.g. "Round plan: 10 → 7 → 4 → 3") before the first elimination round.

```
R (reduction per round) = clamp( round(0.30 × N), 2, floor(0.50 × N) )
```
- N = starting count, fixed for the whole run
- Minimum: 2 fewer per round
- Maximum: 50% of N
- Target: 30% of N, rounded

```
remaining = N
while remaining > 3:
    next = remaining - R
    if next <= 3: next = 3   # final round always lands exactly on 3
    remaining = next
```

Examples: N=7 → 7→5→3. N=10 → 10→7→4→3. N=20 → 20→14→8→3.

## 5. Elimination rounds (cooling)

Not pure filtering — especially for Counter-direction and Creative-lateral ideas. Actively rework/bend surviving ideas toward the goal rather than discarding anything that isn't already close. This is where the actual creative payoff happens: an idea that deliberately ran against the goal in exploration gets transformed over 1-2 rounds until it contributes to the goal via an unexpected path.

Example: a counter-direction idea ("deliberately design the shop for older, traditional readers") can be turned, next round, into a goal-serving one ("dusty-traditional becomes a quirky, cozy countryside aesthetic that's a cult favorite among young people") — instead of being cut just because it doesn't look goal-aligned at first glance.

Select the number of survivors set by the round plan. Ideas may be refined, bent, or merged into a new idea.

For EVERY surviving idea, give:
- **Idea**: current state (may be refined/transformed from the previous round)
- **Direction**: keep the ORIGINAL direction from Step 3, even once the idea sits closer to the goal — this preserves visibility into where each surviving idea came from
- **Reasoning**: why it survived this round, relative to what got cut — if transformed, briefly explain how it moved toward the goal

Don't list eliminated ideas explicitly — they're already visible in the previous round. The user can reference an earlier round anytime ("what happened to approach X", "combine X with Y").

## 6. Final round

Exactly 3 ideas, same format as elimination rounds (idea + reasoning), clearly marked as the conclusion — reasoning here can be a bit fuller since this is the final selection.

## Output format

```
## Round plan: N → ... → 3

## Round 1: Exploration (N ideas)
1. **[Idea]** — Direction: [Counter-direction/Creative-lateral/Goal-direction] — Approach: [...]
2. ...

## Round 2: Elimination ([count] ideas)
1. **[Idea]** — Direction: [original direction] — Reasoning: [...]
2. ...

[additional elimination rounds if any]

## Final round (3 ideas)
1. **[Idea]** — Direction: [original direction] — Reasoning: [...]
2. ...
3. ...
```

After the final round, briefly offer that the user can combine or revive ideas from earlier rounds.
