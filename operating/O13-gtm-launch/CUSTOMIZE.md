# Customize: GTM Launch

A paste-in prompt that adapts this skill to your launch.

Works in **Claude Code**, **Claude.ai Projects**, or **OpenAI Codex**, all three read the same
`SKILL.md` format. Open the assistant, paste the block below, and answer its questions one at a time.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The prompt

```
You are helping me adapt GTM Launch to my specific launch.

Read the attached SKILL.md (gtm-launch). It guides launch planning through GTM motion
selection, funnel projection, channel strategy, asset creation, and war room coordination.
If profiles/client-profile.md exists, read its Company, ICP Definitions, Buyer Personas, Value
Propositions, Competitive Landscape and Proof Points sections first.

Your job is NOT to rewrite the framework. It is to help me plan a launch that is executable
with my resources.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What are you launching, and to whom? (Product, feature, market entry, repositioning, and
   your target customer)

2. What are your GTM motion options, and which feels like the best fit? (Inbound, outbound,
   product-led, community-led, partner-led)

3. What is your revenue goal for the launch period, and how realistic is it? (What does
   success look like, in a number?)

4. What resources do you have? (Budget, team, time available)

5. What could go wrong, and how would you know if it did? (What are you most worried about?)

Then produce:

A. GTM motion selection with specific rationale for why this motion over others

B. Funnel projection from revenue goal through all conversion stages (conservative, base,
   optimistic scenarios)

C. Launch asset specifications (website structure, demo script, social proof inventory)

D. Channel strategy with sequencing and success metrics per channel

E. War room plan: roles, escalation paths, response templates

F. The "Launch Plan" profile section below, filled in with my answers

G. THE HONEST PART: if the revenue goal is unrealistic based on funnel math, say so and
   recommend adjusted goals. List any question above I answered with a guess.

Start with question 1.
```

---

## What you should expect to happen

Questions 1 and 2 go quickly. Question 3 is where the plan meets arithmetic: the funnel
projection works backward from the goal, and most first goals need more top-of-funnel volume
than the team can produce in the window. That gap is the most useful thing this skill tells
you, so let it show rather than quietly lowering the goal.

Question 5 stalls when a team has never written down what failure would look like on day one.
If that happens, section E (the war room plan) is where to spend the extra time.

---

## Minimum profile fields this skill reads

The skill starts from the profile sections every GTM skill already uses. Proof Points matter
most here, because launch social proof is drawn from them. Add one section of its own to
`profiles/client-profile.md`:

```markdown
## Launch Plan

- **What is launching:** [product, feature, market entry or repositioning]
- **Motion:** [inbound, outbound, product-led, community-led or partner-led, and why]
- **Revenue goal and window:** [the number, and the dates it is measured between]
- **Launch day owner:** [who runs the war room]
```

---

## If you are stuck on any question

- **Question 1 stalls:** you are launching a capability, not a product for a customer. Run GTM
  Discovery (`operating/O15-gtm-discovery`) first and come back with a named customer.
- **Question 2 stalls:** pick the motion your best current customers actually arrived through.
  The launch is not the moment to learn a new motion from scratch.
- **Question 3 stalls:** let the funnel projection set the goal. Give the skill your realistic
  traffic and conversion rates and read the revenue it produces.
- **Question 4 stalls:** list what is already committed (people, budget, dates) and plan only on
  that. A launch planned on hoped-for resources slips on day one.

---

## When you are ready to execute

After launch planning is complete, you know:
- Which GTM motion to use and why
- How much traffic you need at each stage
- What assets need to be ready before launch day
- Which channels to activate and in what order
- What success looks like for each role on launch day

When you have that, launch becomes a matter of execution, not hoping. The plan either works or
gives you clear data on why it did not. Both are useful.

If you launch without a funnel model, you will not know how much traffic you need. If you launch
without channel prioritization, you will spread too thin. If you launch without a war room plan,
launch day will be chaos.

A boring launch with a plan beats an exciting launch without one. After launch, GTM Engine
(`operating/O12-gtm-engine`) takes over.
