# Customize: Positioning

A paste-in prompt that adapts this skill to your team's value, price and approval rules.

Works in **Claude Code**, **Claude.ai Projects**, or **OpenAI Codex**. All three read the same `SKILL.md` format. Open the assistant, paste the block below, and answer its questions one at a time.

> This is a per-skill companion. For customizing the whole suite at once, see the profile template at `profiles/client-profile-template.md`.

---

## The prompt

```
You are helping me adapt a positioning skill to my company's value, price and approval rules.

Read the attached SKILL.md (gtm-positioning, version 2.0.0). It takes the customer
picture from our discovery work, runs six questions in order, tests a positioning
statement on four points, attaches proof and a grade to every value claim, sets a price
only after the statement passes, and checks the price against three economics thresholds.
If the economics fail, it sends the position back. It never tunes the numbers.

Your job is NOT to rewrite the skill. It is to fit its thresholds and rules to my
company, point the first pass at the price and cost records we actually have, and tell
me honestly where you cannot answer for us.

Ask me these, ONE AT A TIME, and wait for each answer:

1. In one sentence, what does the buyer get more of as they pay us more? (This becomes
   the value metric candidate. Examples: sites, seats, plots, transactions, records.)

2. What is our list price, and what else do we charge? Include any setup or implementation
   fee, and say whether that fee is charged per site, per seat or per account. If we have
   no list price yet, say so, and the price will be marked modeled.

3. Who must sign above a certain amount, and what is that amount? Give the year-one figure
   and the role of the person who signs.

4. Do you accept the three economics thresholds as written (lifetime value to acquisition
   cost above 3 to 1, payback under 12 months, gross margin above 70%)? If not, name yours
   and say why.

5. Which cost records do we have? (Acquisition cost per customer, gross margin, and how long
   customers stay.) If a record is missing, say so. The gate will report "not run" for it.

6. Which customer conversations may we hold for the past-behavior price test, and through
   which route? Name who may contact buyers, and who may not.

7. How long should proof stay valid? The defaults are 30 days for heard and seen, and 90
   days for confirmed. Change them only with a reason. The pilot-only flag stays on either way.

Then produce:

A. Value metric candidates from my answer to question 1, each with the reason it matches the
   value and the reason it might be the wrong unit to bill.

B. The past-behavior price test script, using my answers to questions 3 and 6, with the
   three questions asked in past-behavior form. Never "would you pay X?"

C. The economics inputs we are missing, ranked by how much they would change the payback
   result.

D. THE HONEST PART: a short list of the questions above I could not answer concretely,
   and which parts of our statement therefore stay labelled as hypotheses. If the cost
   records are missing, the economics are "not run", and that is the finding. Say so.

Start with question 1.
```

---

## What you should expect to happen

Questions 1, 2 and 3 usually land quickly, because most teams know their list price and their approval line. Question 5 is where teams stall. Acquisition cost and retention are rarely written down, and the gate will report "not run" until they are. That is the correct result, not a gap to fill with a benchmark.

Question 2 has a common trap. The setup rule decides whether a multi-site buyer crosses the approval line that a single-site buyer stays under. At $899 a site, with one $5,000 setup per account, a two-site year one is $26,576, which is over a $25,000 line. Charged per site, the same two-site account would be $31,576. Answer the setup rule precisely, because the skill will show both totals.

If section D is long, the gap is in the records, not in the skill. A position needs at least one pilot or customer result per value claim, marked with its grade, and the economics need the cost records.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once. The skill reads the existing Company, ICP Definitions, Buyer Personas, Core Pain Points, Value Propositions, Competitive Landscape and Proof Points sections, and writes back to them. It also reads this section:

```markdown
## Positioning

- **Knowledge base path:** [folder where Positioning nodes are written, or "none yet"]
- **Owner of the positioning decision:** [the person who approves the statement and the price before any write]
- **Value metric default:** [the unit the buyer gets more of as they pay more, or leave blank]
- **Price list and setup rule:** [list price, setup fee, and whether setup is per site, per seat or per account]
- **Approval line:** [the year-one amount above which someone else must sign, and who signs. Default: $25,000]
- **Economics thresholds:** [default: lifetime value to acquisition cost above 3 to 1, payback under 12 months, gross margin above 70%]
- **Re-grade windows:** [default 90 days for confirmed, 30 days for heard and seen. Change only with a reason]
- **Price test channel:** [who may contact buyers for the past-behavior price test, and through what route]
```

---

## Troubleshooting

| Problem | Cause | Response |
|---------|-------|----------|
| The skill says every value claim is `assumed` | Proof is missing, or the only proof is illustrative | Add real pilot or customer results with their counts. Until then, the output is honest but the statement stays hypothesis-heavy |
| The economics say "not run" | Acquisition cost, gross margin or retention is missing | Supply the missing record and re-run. Do not enter a benchmark and report the result as a finding |
| The statement passes everything except Credible | The proof is pilot-only | Keep the claim with its pilot-only flag, or move it to the bets. Do not remove the flag |
| The price fails payback | The position may be aimed at a buyer with a long path to signature | Expect the skill to send the work back to who the position is for. Do not lower the price, because that makes payback longer |
| The price sits outside the archetype band | The value metric or the price was chosen for ease of billing | Flag it, then re-check the value metric against what the buyer gets more of |
| A two-site buyer crosses the approval line | The setup fee is per account, and the two-site year one is $26,576, over the line | Show both totals, confirm the setup rule in the profile, and narrow the start to one-site buyers. Do not change the price to pass |
| The output is too long to read | The brief was written past two pages | Ask for the two-page brief only. The nodes hold the detail, and the brief links to them |
