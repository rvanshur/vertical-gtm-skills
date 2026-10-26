# Customize: Research-Driven Outbound

A paste-in interview that adapts this skill to your own go-to-market motion. It asks what your
industry actually publishes, which numbers your product moves and which sources exist for your
private accounts. It then writes the one profile section this skill reads, so the next run starts
from your facts and not from defaults.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The Prompt

```
You are helping me adapt a GTM methodology skill to my company's go-to-market motion.

Read the attached SKILL.md (gtm-research-outbound). It builds a sourced point of view and outbound
package from a public filing, an owner letter or an earnings call, with an ICP verdict, a signal
map, a sourced wedge and persona sequences.

Your job is NOT to rewrite it. It is to make it fire on my accounts, my personas and my vertical,
and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Which public facts about the accounts in my vertical actually predict a deal? Think of filings,
   owner letters, licensing changes, job postings, expansion news. Name the ones you have seen come
   before a real opportunity.

2. My wedge: what number does my product move, and what is the honest range I can defend (not the
   best case)? Which proof point stands behind it, and is that proof point Verified, a Benchmark or
   Illustrative?

3. Tell me about one target where research genuinely changed the message I sent. What did I find,
   and where did I find it?

4. Many of my targets are private. Which sources exist for private companies in MY vertical (state
   licensing records, permits, trade association lists, franchise disclosures, local press)? For
   each one, how current is it, and how long does it lag?

5. Who reads the point of view brief: the rep alone, or does part of it go in front of the
   prospect? That decides how polished the brief needs to be.

Then produce, in this order:

A. THE HONEST PART: the questions above I could not answer concretely, and what I would need to
   gather to answer them. Do not paper over these. An answer I guessed at is a gap, and the gap is
   the finding.

B. A short note on which answers were thin, and which of them a rep could not use yet.

C. The "## Industry Context" section, filled with the exact answers I gave you, ready to paste into
   profiles/client-profile.md. Name no individual. Every sourced fact carries its source and year.
   Leave a line as [Unknown] when I could not source it.

Start with question 1.
```

---

## What You Should Expect To Happen

**Question 2 Stalls** most often, and it is the expensive one. A wedge number with no proof point
behind it turns the whole package into confident fiction, and a proof point marked Illustrative
cannot appear in an email at all. **Question 4 stalls** when the team has only ever researched public
companies, and the private-company sources for the vertical were never mapped.

Both kinds of stall point at the same missing thing: a context layer. The skill is a procedure. A
procedure needs to know who you sell to, what has worked and what has already gone wrong. That is
what `profiles/client-profile.md` is for. Build it once and every skill in the suite inherits it.

---

## Minimum Profile Fields This Skill Reads

Add this section to `profiles/client-profile.md`, using the shape in the template's Sales-Layer
Sections block:

```markdown
## Industry Context
- **Sourced facts:** [fact, source, year] one per line. An unsourced fact is dropped, not kept
- **The number we move:** [metric, defensible range, the proof behind it]
- **Vertical financial signals:** [signal, where it appears, what it predicts]
- **Private-company sources:** [source, what it reliably tells you, lag]
```

The same section is also read by Trigger Event Outbound (04) and Closed-Loss Reactivation (05), so
a fact you add here reaches all three skills on their next run.

---

## About The Emails

The number of emails is set by your profile, not by this skill. Each persona in your Buyer Personas
table gets one sequence, and each sequence has four emails. If your motion runs on three personas,
the package has twelve emails, and that is the right number. Volume that outruns your proof points
reads as spray to the buyer, so write fewer sequences that are specific before you write more that
are generic.
