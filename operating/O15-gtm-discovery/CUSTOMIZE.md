# Customize: Discovery

A paste-in prompt that adapts this skill to your team's go-to-market motion.

Works in **Claude Code**, **Claude.ai Projects**, or **OpenAI Codex**. All three read the same `SKILL.md` format. Open the assistant, paste the block below, and answer its questions one at a time.

> This is a per-skill companion. For customizing the whole suite at once, see the profile template at `profiles/client-profile-template.md`.

---

## The prompt

```
You are helping me adapt a discovery skill to my company's go-to-market motion.

Read the attached SKILL.md (gtm-discovery, version 2.1.0). It diagnoses which archetype
my business is, grades every belief about our customer by evidence (assumed, heard, seen,
confirmed), plans the cheapest evidence for the bets that matter most, and writes the
result to our knowledge base for Positioning, Launch and Engine to read.

Your job is NOT to rewrite the skill. It is to make the diagnosis fit my market, point
the first evidence pass at the records we actually have, and tell me honestly where you
cannot answer for us.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Describe a typical customer in one sentence: who signs, who else is in the room,
   and what they were doing before they bought us.

2. What does our median closed deal look like? Give me the sales cycle (in weeks or months)
   and the contract value we actually collect today, for your last 10 to 20 closed deals if
   you have them. If you do not have them, say so, and I will mark those answers as assumed.

3. Do our customers move money or transactions through our product? If yes, roughly how
   much per month per customer?

4. Do two distinct user types have to transact with each other on our platform, such as
   buyers and sellers, or contractors and subcontractors? Or are the users all on one side?

5. Which records do we already keep? (CRM stages and fields, contract signers, referral
   source, usage or activation data, loss reasons, call recordings or notes.)

6. Which claim about our customer do we use most often in pitches, and which one would hurt
   us most if it were wrong?

Then produce:

A. Our starting archetype guess, based only on my answers so far, with the question that
   would most likely change it. Name which archetype leads if we are a hybrid.

B. The first evidence pass: for each record in question 5, the exact count I should pull
   and the n I should expect to report beside each rate. If a count is not in those
   records, say so and leave it out. Do not estimate it.

C. Our three load-bearing assumptions, ranked, and the cheapest evidence that would move
   each one. Write each as a question about past behavior, never an opinion.

D. THE HONEST PART: a short list of the questions above I could not answer concretely, and
   which of our claims therefore stay assumed. If the answers to question 2 are missing,
   the diagnosis is a guess, and that is the finding. Say so.

Start with question 1.
```

---

## What you should expect to happen

Questions 1, 3 and 4 usually land quickly. Question 2 is where teams stall, because the median of recent deals is rarely written down. If it is missing, the skill marks every cycle and value claim as `assumed`, and that is the correct result.

Question 6 is the most useful one. The claim a team uses most often is usually the one it has graded least.

If section D is long, the gap is in the records, not in the skill. A diagnosis needs at least the closed-deal history and a signer or stakeholder field. Without those, the output will be a candidate with low confidence, and the first task becomes building the record, not running more interviews.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once. The skill reads the existing Company, ICP Definitions, Buyer Personas, Core Pain Points and Competitive Landscape sections, and writes back to them. It also reads this section:

```markdown
## Discovery

- **Knowledge base path:** [folder where Discovery nodes are written, or "none yet"]
- **Starting archetype guess:** [the archetype you believe you are, and why; leave blank if unsure]
- **Deal history source:** [where closed deals live: CRM report name, export file, or other]
- **Stakeholder field:** [the CRM field or contract field that records who was in the room]
- **Re-grade windows:** [default 90 days for confirmed, 30 days for heard and seen; change only with a reason]
- **Interview channel:** [who may contact customers for past-behavior conversations, and through what route]
```

---

## Troubleshooting

| Problem | Cause | Response |
|---------|-------|----------|
| The skill says every claim is `assumed` | No closed-deal history was provided, or the records were not readable | Provide 10 to 20 closed deals, or name the CRM report to pull. Without them, the output is honest but thin. |
| The archetype comes back as a hybrid with low confidence | The cycle and value answers point to different bands | This is a real contradiction, not an error. Run the ten-deal test per segment, as the skill suggests, before choosing a leading archetype. |
| The ten-deal test fails on the segment you are trying to win | The test was run across the whole company, mixing segments | Run the test separately for each segment with at least 10 closed deals. A test on mixed segments can fail for a reason that has nothing to do with the segment you are targeting. |
| A rate appears without an n | The rate came from a manual summary, not a count | Ask for the count. Rates without n are returned to the team, per the skill's first working rule. |
| The starting segment does not change even though one segment looks better | The gap is under the stated threshold | This is the intended behavior. The skill reports "no difference found" at the threshold it names. Change the threshold only if you can say why. |
| Positioning refuses to run on the output | Positioning found `assumed` claims in the open bets | Grade the claims it needs, or accept that the statement will be scoped to what is confirmed. Do not delete the open bets to make the hand-off pass. |
| The output is too long to read | The brief was written beyond two pages | Ask for the two-page brief only. The nodes hold the detail, and the brief links to them. |
