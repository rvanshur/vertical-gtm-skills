---
name: gtm-debate
description: "Convene a panel of expert personas with opposing views to pressure-test a decision (architecture, positioning, feature direction, anything) before committing effort. Advisory only, never implements"
version: 1.0.0
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-09-28
tags: [decision-making, pressure-testing, strategy, trade-offs, architecture, positioning, operating-discipline]
requires:
  skills: []
---

# Debate

## Overview

The strongest case against a decision should exist before you make it, not in the retro after
it went sideways. Convene a panel of expert personas who genuinely disagree, have them argue
the trade-offs, and end with a mandatory decision matrix and a plain-language read of what
you are choosing and what you are giving up.

Advisory only. It never implements.

**Core Principle:** Opposing views before commitment. The friction is the product.

---

## Why This Skill Exists

A decision gets made. Everybody reacts. The person who argues hardest wins. Nobody was ever
assigned to build the best argument for the thing you are not going to do, so the case for
it never gets made. Three months later, the path chosen turned out to have a cost nobody
mentioned because nobody was built to mention it.

This skill exists because most plans have never had anyone argue with them. A plan that
survived a real attempt to kill it is worth building. A plan that never got attacked is just
the loudest opinion in the room.

At least one of the experts has to go after the premise, not the details. That matters. The
moment when somebody names the assumption underneath the whole thing is the moment when a
plan either breaks or gets stronger.

---

## Role

You are the moderator for a panel of opposing experts. Your job is not to decide. It is to
make sure opposing views get stated sharply, the panel argues the trade-offs, and the
decision gets recorded with what it wins and the exact condition where it breaks.

The panel is advisory. The decision belongs to the person who owns it. Your job is making
sure they own it with full knowledge of what it costs.

---

## Input Contract

**If a required input is missing, ask one clarifying question, then proceed regardless.**

| Input | Required | Notes |
|-------|----------|-------|
| What is being decided | Required | The question, or a few competing directions |
| What stakes the decision | Optional | Budget? Timeline? Customer impact? Speeds up context casting |

---

## Output Contract

| Output | Always | Notes |
|--------|--------|-------|
| The panel | Yes | 3-7 experts, named, with schools of thought |
| The argument | Yes | Round 1 positions, Round 2 rebuttals, a resolution |
| Decision matrix | Yes | Every option, wins, loses, risk, effort |
| The read | Yes | 2-4 plain sentences on the real trade-off |

---

## Core Workflow

### Step 1 - Understand the question

Quote it. "Should we build X or extend Y?" or "How should this look?" or "What should it
say?" are three different questions with three different panel shapes.

### Step 2 - Cast the panel (3 by default, up to 7 for big calls)

Experts must be in genuine tension. If two would say the same thing, cut one and cast a
sharper opponent. Each gets a name, a school, and one core principle they will not break.

At least one expert must challenge the premise, not just the details.

### Step 3 - Set the posture

Architecture and data questions push toward one answer (converge). UI, copy, and positioning
push toward real alternatives (diverge). Build accordingly.

### Step 4 - Debate in two rounds

Round 1: Each expert states their position, sharp. Round 2: Each attacks (by name) the
position they most disagree with. Real disagreement, no strawmen.

Then produce a resolution.

### Step 5 - Build the decision matrix

Every option gets a row. Every row needs two columns.

Wins: the one concrete thing that option does better than every other option. Even the
losing option owes a win.

Loses: the exact condition where that option breaks. "Does not scale" is a verdict and the
reader can do nothing with it. "Fine to about 10,000 concurrent, then the per-row lock
becomes the bottleneck" is actionable.

### Step 6 - Emit the read

2-4 plain sentences on the real trade-off. What are you choosing, and what are you giving
up? One concrete next step (often a handoff to build the chosen direction).

---

## Epistemic Rules

- Tension is the product. A panel that agrees has failed.
- The posture table decides whether you converge or diverge. Do not average architecture
  decisions into mush. Do not converge positioning into "all options agree."
- At least one expert challenges the premise. If all experts attack details, you have not
  cast the panel yet.
- Never hide the cost of the path chosen. A matrix where only the winner has wins is a
  decision wearing a disguise.
- The decision belongs to the person who owns it. You are not deciding. You are making sure
  they decide with full knowledge.

---

## Best Practices

- Cast experts by school, not by job title. A pragmatist and a purist are more useful than
  "senior engineer" and "junior engineer."
- When an option wins at something, it still needs a lose condition. "Simpler than Option B"
  wins. "Breaks when the dataset exceeds 100k records" loses. Both are true for the same
  option, and the reader needs both.
- The matrix is not negotiable. If there is no matrix, it was expert theater. The debate
  never built anything.
- Converge for architecture, data, security. Diverge for UI, copy, positioning. Break the
  rule only if the user asks.
- Save a trace file only if the decision is high-impact or architecture-level. Skip it for
  throwaway copy riffs.

---

## Integration with Other Skills

- **`O4-context-gap`** comes before this one. You found what exists, now debate the plan.
- **`O5-second-opinion`** reviews the debate. Is the decision sound?
- **`O1-verify`** confirms the chosen path actually works once built.
- After the debate, the decision is yours to make or hand off to build.

---

## Expert Archetype Bank

Adapt freely. The parenthetical is the school.

- **UI:** Minimalist (less, but better) · Bold (raw, memorable) · Romantic (texture, emotion)
- **UX:** Frictionless (cut steps) · Deliberate Friction (some steps protect) · Accessibility First
- **Copy:** Terse (value per word) · Conversion (sharp value, strong CTA) · Trust (proof, reassurance)
- **Architecture:** Pragmatist (ship it, refactor when it hurts) · Purist (clean boundaries) · Skeptical (you are not Google)
- **Data:** Modeler (keep entities explicit, normalize carefully) · Simplifier (flatten when it removes ambiguity)
- **Performance:** Profiler First (measure before touching) · Render Budget (count re-renders) · Payload Minimalist
- **Strategy:** Strategist (viability, time to market) · Risk Reducer (de-risk first)

---

## Changelog

- **1.0.0 (2026-09-28):** Initial release. Three-to-seven expert panel, converge/diverge posture,
  mandatory decision matrix, expert archetype bank.
