---
name: gtm-launch
description: "Launch planning and execution. GTM motion selection, channel strategy, funnel projection, launch asset blueprints, social proof collection, budget modeling, launch coordination, and day-of engagement playbooks."
version: 1.1.0
category: Operating-Discipline
author: Ryan Vanshur
license: MIT
updated: 2026-09-29
tags: [launch, GTM-motions, channel-strategy, funnel-projection, launch-execution, war-room, social-proof, launch-budget, operating-discipline]
requires:
  skills: ["gtm-discovery", "gtm-positioning"]
---

# GTM Launch

## Overview

Transforms strategy and positioning into a coordinated launch. Covers GTM motion selection, channel strategy, funnel math, launch asset creation, social proof collection, budget modeling, launch coordination, and day-of execution playbooks.

**Core Principle:** A launch is not a moment, it is a system. The teams that launch well have spent 80% of their time on preparation and 20% on execution. Reverse that and you are just hoping.

---

## Why This Skill Exists

Founders finish positioning and call it a launch. They write an email to their network. They post on Twitter. They ship the product. One day of chaos. Three weeks later, nothing happened.

The cost of that failure is not just zero revenue that week. It is zero visibility, zero signal, and the demoralization of a team that built something and watched it disappear. It is also wasted positioning work. The message was good, but nobody heard it.

This skill forces launch into a system instead of an event. You plan what channels you are using, why you are using them, and what you expect from each. You model the funnel backward from revenue goal so you know how much traffic you need. You create assets before launch day. You build a support network. You prepare response plans for common objections. You rehearse the war room.

The teams that launch well do not get lucky. They prepare. This skill codifies that preparation.

---

## Role

You are a **launch orchestrator**, not an executor. Your job is to help the user plan a launch in detail before anything ships. You create the battle plan. The team executes it.

You are not satisfied by "launch day will be exciting." You are satisfied by a plan that could run without the main founder.

---

## Input Contract

| Input | Required | Notes |
|-------|----------|-------|
| Positioning statement and messaging house | Required | From `O14-gtm-positioning` |
| GTM motions under consideration | Required | Inbound, outbound, product-led, community-led, partner-led |
| Revenue goal for the launch period | Required | What does success look like? |
| Available resources (budget, team, time) | Required | This determines what is possible |

---

## Output Contract

| Output | Always | Notes |
|--------|--------|-------|
| GTM motion selection with rationale | Yes | Why this motion, not the others |
| Funnel projection from revenue goal | Yes | How many customers, SQLs, leads, and website visitors you need |
| Launch asset specifications | Yes | Website structure, demo script, copy guidelines |
| Channel strategy | Yes | Which channels, in what sequence, with success metrics |
| Launch day playbook | Yes | War room structure, response templates, engagement targets |

---

## Context

You read the positioning statement. You understand the customer archetype. You know what problem is being solved. You do not assume launch budgets are unlimited.

Reads `profiles/client-profile.md` if it exists, as the starting evidence: Company, ICP Definitions, Buyer Personas, Value Propositions, Competitive Landscape and Proof Points.
Treat what is already there as claims to test, not facts. What this skill validates is meant
to be written back into those same sections, because the profile is what the 14 GTM skills
in `skills/` run on. That write-back is how the strategy layer reaches the daily motion. If the profile has a
`## Launch Plan` section (this skill's `CUSTOMIZE.md` writes it), read that first.

---

## Quick Reference

| Module | Output | Time | Best For |
|--------|--------|------|----------|
| **GTM Motions & Channel Selection** | Ranked motions with scored channel recommendations | 2-3 hours | Deciding which levers to pull for this launch |
| **Funnel Projection** | Backward funnel math from revenue goal through conversion stages | 1-2 hours | Understanding the volume you need at each stage |
| **Launch Asset Blueprint** | Website/landing page structure and demo script specifications | 2-4 hours | Defining what needs to be built before launch day |
| **Social Proof & Pre-Launch Content** | Social proof inventory and 5+ pre-launch content pieces | 1-2 days | Building credibility before launch |
| **GTM Budget** | Per-channel budget with ROI projections and month-by-month spend plan | 1-2 hours | Justifying spend and allocating resources |
| **Launch Coordination** | Support network roster and war room plan | 2-4 hours | Preparing the logistics of launch day |
| **Launch Day Playbook** | Event run-of-show, engagement targets, response templates | 2-3 hours | Executing flawlessly on the day |

---

## Epistemic Rules

- **No channel works without message-market fit.** You cannot scale a broken message with paid advertising. Prove organic traction first.
- **Funnel math reveals what is actually possible.** If your revenue goal requires 50,000 website visitors but you can realistically get 5,000, something has to change: your goal, your conversion assumptions, or your channels.
- **GTM motions are not channels.** Inbound is a motion (content, SEO, referral). LinkedIn and Twitter are channels within that motion. You choose the motion first, then the specific channels.
- **Social proof is ranked.** A named customer plus a metric outranks a named customer plus a quote, which outranks a logo wall. Lead with your strongest tier.
- **Preparation prevents chaos.** If the war room is rehearsed and the response templates are ready, launch day is boring. Boring is good.

---

## Core Workflow

### Step 1. Assess Launch Context

Is this a product launch, a feature launch, a market entry, or a repositioning? Each has different requirements.

Ask: What are we launching, and who are we launching to?

### Step 2. Select GTM Motion

Evaluate five fundamental motions:
- **Inbound:** Content, SEO, social, referral
- **Outbound:** Cold email, LinkedIn, calling
- **Product-Led:** Free trial, freemium, self-serve
- **Community-Led:** Community engagement, word of mouth
- **Partner-Led:** Channel partners, integrations, co-marketing

Score each on impact, resource match, time to results, and scalability. Select the top 1-2.

### Step 3. Narrow Down Channels

Within the chosen motions, select 2-3 specific channels. Do not spread too thin. Master the channels you pick.

### Step 4. Project the Funnel

Work backward from revenue goal:

Revenue Target → Deal Size → Customers Needed → Close Rate → Opportunities → SQLs → MQLs → Leads → Visitors/Outreach Volume

Build three scenarios (conservative, base, optimistic). Sensitivity analysis shows which conversion rate matters most.

### Step 5. Create Launch Assets

Define the website/landing page structure (nine-section framework: hero, social proof, problem, solution, how it works, features, pricing, FAQ, CTA).

Define the demo script (0-5 minutes, structured: hook, context, workflow, secondary value, close).

### Step 6. Collect Social Proof

Audit existing proof points. Rank by strength. Target at least 5 attributable proof points before launch.

Create 5+ pre-launch social content pieces (expertise signals, behind the scenes, problem spotlights, hot takes, social proof teases).

### Step 7. Build Launch Budget

Allocate budget by channel. Per-channel ROI calculation based on funnel projection. Budget rules: never >30% on a single unproven channel, kill channels with no signal in 30 days, reallocate from losers to winners monthly.

### Step 8. Coordinate Launch Logistics

Organize a support network (inner circle, active supporters, passive amplifiers). Create HSPC launch email templates. Plan the war room (commander, customer response, technical monitor, social monitor, comms).

### Step 9. Create Launch Day Playbook

Define success metrics for each role. Create response templates for common objections. Set engagement targets (example: social mentions answered within 15 minutes). Rehearse twice before launch.

---

## Examples

### Worked Example 1: Launch Without Positioning (Launch Failure)

**Stated motion:** "We are going to launch on Product Hunt and Twitter."

**The problem:** No channel selection rationale. No funnel math. No social proof prepared. Just hoping Product Hunt will distribute the product.

**Fix:** Map the customer first. Is Product Hunt your customer? Probably not, it is early adopters. Are you selling to early adopters? Map your GTM motion first. Choose channels that reach your actual customer. Prepare for each channel specifically.

### Worked Example 2: Funnel Math That Reveals Impossibility (Launch Success)

**Revenue goal:** $100K in month one

**Deal size:** $2K

**Customers needed:** 50

**Conversion rate (opportunity to customer):** 25% (reasonable)

**Opportunities needed:** 200

**SQL to opportunity rate:** 50% (reasonable)

**SQLs needed:** 400

**MQL to SQL:** 20% (reasonable)

**MQLs needed:** 2,000

**Visitor to MQL:** 2% (reasonable)

**Visitors needed:** 100,000

**Reality:** You can get 100,000 visitors in month one only if you already have significant reach or large budget. If you have neither, your revenue goal is wrong.

**Fix:** Set goal to $20K (10 customers), or extend timeline to quarter, or increase marketing budget.

The math is what reveals the gap. Not guessing.

### Worked Example 3: Social Proof That Converts (Launch Success)

**Weak social proof:** "Used by 1,000+ companies"

**Strong social proof:** "Caught $340K of outside-counsel overbilling in the first 90 days for Northgate Foods, a mid-market legal team" (the Lexora example profile's own proof point)

**Why it works:** The specific metric, the specific company, and the company details make it credible. A reader can see themselves in that case.

---

## Troubleshooting

| Problem | Cause | Response |
|---------|-------|----------|
| "We did not hit our launch revenue goal" | Goal was unrealistic or funnel assumptions were wrong | Use the actual data to calibrate next month. Adjust goal or levers. Funnel math applies going forward. |
| "Our GTM motion worked but the channel underperformed" | Channel selection or message-market fit issue | Kill the underperforming channel. Double down on what worked. Test different channels within the same motion. |
| "Social proof is hard to get before launch" | Proof needs to come from real customers | Launch to beta customers first. Collect proof. Then launch to broader market. Build in lead time. |
| "Launch day was chaotic even though we planned" | War room was under-resourced or response templates were vague | Next launch: rehearse twice, make targets specific numbers (not vague), assign clear ownership. Boring is better than heroic. |

---

## Best Practices

- **Launch to a beta cohort first.** Collect proof and testimonials. Refine positioning based on feedback. Then launch to the broader market with real social proof.
- **Do NOT launch on a Friday.** You will not be able to support customers over the weekend. Launch on a Tuesday or Wednesday.
- **Preparation reveals the gap.** If you discover during planning that you cannot hit your revenue goal with realistic assumptions, better now than after launch.
- **Channel sequencing matters.** Start with the channel that gives you the earliest signal. Prove message-market fit. Then scale to other channels.
- **Rehearse the war room twice.** Role-play the launch day. Discover what is missing before it matters.

---

## Integration With Other Skills

- **`O15-gtm-discovery`** and **`O14-gtm-positioning`** produce the customer, problem, and message that launch executes. Launch is downstream of these.
- **`O12-gtm-engine`** runs a post-launch retrospective to analyze what worked and what did not.

---

## Changelog

- **1.1.0 (2026-09-29):** Context section now names the client profile sections this skill reads and writes back to. Worked example now uses the Lexora case study.
- **1.0.0 (2026-09-28):** Initial release. Five GTM motions, funnel math, asset blueprinting, war room coordination, social proof collection. Adapted from Maja Voje's GTM Strategist methodology (Phases 7-9).

## Credits

Adapted from the GTM Strategist skills by Maja Voje (github.com/GTM-Strategist/gtm-strategist-skills), used under the MIT License. Copyright (c) 2026 Maja Voje / GTM Strategist. Frameworks named in this skill (April Dunford positioning, Van Westendorp and Gabor-Granger pricing research, ICE and PIE scoring) belong to their authors.
