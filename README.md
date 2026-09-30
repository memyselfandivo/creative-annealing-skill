# Creative Annealing

An AI skill that structures creative ideation as a multi-round process inspired by simulated annealing: a wide, high-temperature exploration phase first, followed by staged elimination rounds — cooling down step by step — to exactly three final ideas, with the reasoning behind every survival tracked along the way.

## Why

Most brainstorming prompts either dump a flat list of ideas or converge too quickly on the first plausible answer, usually with every idea still pointing loosely toward the same goal. The core characteristic of the original algorithm isn't "generate many ideas" — it's the temperature arc: starting hot enough to move freely, even away from a good solution, then cooling gradually so the search settles into a stable outcome instead of getting stuck on the first workable one. This skill mirrors that arc — the exploration round runs "hot" (wide, unconstrained, explicitly searching in three directions relative to the goal), and each following round cools it down, bending the off-target ideas back toward the goal along an unexpected path — while keeping a full trail of *why* each idea survived (or didn't) so nothing gets lost along the way.

## How it works

1. **Trigger** — say "creative-annealing" together with a topic and a starting idea count, or just the trigger word alone and the skill will ask for both.
2. **Clarification** — before exploring, the skill pins down what the "goal direction" is and what its plausible opposite would be, so the next step has something concrete to work from.
3. **Exploration round** — generates N ideas spread across three directions relative to the goal: roughly 25% deliberately working *against* it, 50% broadly creative ideas off the direct path (spanning both close-to-goal-but-extreme and entirely different territory), and 25% conventional ideas heading toward the goal as usual. Each idea is tagged with its direction and its underlying approach/angle. The approach tags make it possible to reconsider an idea after the finished result and to bend or extend it in a different direction. No filtering at this stage yet.
4. **Round plan** — computes how many elimination rounds are needed, based on a fixed formula (see below), and shows it upfront.
5. **Elimination rounds** — not pure filtering. Surviving ideas, especially the off-goal ones, get actively bent back toward the goal, each with a short justification for why (and how) it made it past that round.
6. **Final round** — always converges to exactly 3 ideas, each with a fuller rationale.

Not every goal has a cleanly opposite direction — for more abstract goals, the "opposite" can end up feeling somewhat constructed. That's a deliberate trade-off of this approach, not a flaw the skill tries to eliminate.

### Round-reduction formula

```
R (reduction per round) = clamp( round(0.30 × N), 2, floor(0.50 × N) )
```

- `N` = starting idea count, fixed for the whole run
- Minimum reduction: 2 ideas per round
- Maximum reduction: 50% of the starting count
- Target reduction: 30% of the starting count

The final round is a special case: it always lands on exactly 3, regardless of what the formula would otherwise produce.

A starting count of **7 is recommended as a practical minimum** — below that, the process collapses into exploration + one final round with no real intermediate elimination step, which defeats the point of a staged process.

## Installation

Download `creative-annealing.skill` (or the `SKILL.md` directly) from this repo and add it to your Claude skills.

## Usage

```
creative-annealing: how might a small local bookstore attract more customers aged 18–30? / start with 7 ideas
```

or simply:

```
creative-annealing
```

and the skill will ask for the topic and starting count.

## Output format

Each round is clearly labeled, so any idea can be referenced back later — e.g. to ask why a particular approach was eliminated, or to combine two ideas from different rounds.

---

**A note on "temperature":** the "high temperature → cooling" language throughout this skill refers to the *original* metallurgical meaning behind simulated annealing (heating and slowly cooling a metal to reach a stable structure), not to the sampling-temperature parameter used to control an LLM's output randomness. The two concepts are related only by analogy — this skill does not set or rely on any model temperature setting.
