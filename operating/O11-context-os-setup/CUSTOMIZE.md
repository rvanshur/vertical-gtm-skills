# Customize: Context OS Setup

A paste-in prompt that adapts this skill to your knowledge architecture.

Works in **Claude Code**, **Claude.ai Projects**, or **OpenAI Codex**, all three read the same
`SKILL.md` format. Open the assistant, paste the block below, and answer its questions one at a time.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md), and for how this skill sets up the
> knowledge base that Weekly Review, Graph Health, Dream and Ingest run on, see
> [`docs/how-it-fits.md`](../../docs/how-it-fits.md).

---

## The prompt

```
You are helping me build a knowledge base for go-to-market intelligence.

Read the attached SKILL.md (context-os-setup). It guides building a two-layer knowledge system
where atomic concepts are defined once and referenced everywhere, so facts stay synchronized
as they change. If profiles/client-profile.md exists, treat it as the first strategic document
the knowledge base should hold.

Your job is NOT to design a complex taxonomy. It is to help me capture what we know about our
market in a way that does not drift.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What do you already know about your market that you never want to lose? (Positioning,
   customer profile, competitors, regulatory, revenue metrics, whatever exists)

2. Where is it stored right now, and is it scattered or consolidated? (Notion, spreadsheets,
   documents, email, Slack; how fragmented?)

3. Who needs to read this knowledge? (Just you, the team, investors, customers?)

4. What breaks if this knowledge gets out of sync? (If positioning used old customer data,
   what happens?)

5. If you had to stop at one synthesis document, the 5% that answers 95% of questions, what
   would it be?

Then produce:

A. A directory structure (Layer 1 atomic concepts + Layer 2 strategic documents) customized to
   my market

B. A starter taxonomy (5-7 blessed tags, defined)

C. A starter ontology (how my key concepts relate)

D. A one-page documentation guide for how to add knowledge without breaking the system

E. A plan for seeding the base with my first content

F. The "Knowledge Base" profile section below, filled in, so the other knowledge skills know
   where the base lives

G. THE HONEST PART: most knowledge bases are abandoned because they are too complex or nobody
   uses them. Mine will work only if it is simple enough that anyone can use it and immediate
   enough that people will. Tell me which of my answers suggest I am overbuilding.

Start with question 1.
```

---

## What you should expect to happen

Questions 1 and 2 are easy and usually produce a long, scattered list. That is fine. Question 4
is the one that decides the design: if nobody can name what breaks when a fact goes stale, the
knowledge base has no job yet, and it will be abandoned.

Question 5 stalls more than people expect. If you cannot name the one synthesis document, start
with your client profile. It is already the document every GTM skill in this repo reads.

---

## Minimum profile fields this skill writes

This skill does not need the profile to run. It writes one small section that the other
knowledge skills (Weekly Review, Graph Health, Dream, Ingest) can read:

```markdown
## Knowledge Base

- **Location:** [the folder, e.g. knowledge_base/]
- **Taxonomy file:** [where the blessed tags are defined, e.g. knowledge_base/_system/taxonomy.yaml]
- **Synthesis document:** [the one document a new team member reads first]
- **Owner:** [who approves new tags and structural changes]
```

---

## If you are stuck on any question

- **Question 1 stalls:** open the last three decks or documents you sent a customer or investor.
  Every fact in them that you would hate to get wrong belongs in the base.
- **Question 2 stalls:** you do not know where it lives, which is the answer. Seed from the one
  place most people actually check, even if it is a single shared document.
- **Question 4 stalls:** pick one fact that changes often (pricing, a competitor's position, the
  ICP) and trace every place it appears. Each of those is a place it can go stale.
- **Question 5 stalls:** use the client profile as the synthesis document for the first month.

---

## When your knowledge base works

You will know it is working when:
- A new team member can onboard by reading one document (the synthesis)
- When facts change (customer feedback, competitive move), they get updated once and everywhere
  reflects the change
- When discovery runs next quarter, they do not re-derive what was learned last quarter
- When launch planning needs competitive data, they do not rebuild what positioning already has

That is the compounding effect. One fact defined once, referenced everywhere, updated in one place.

If you are three months in and people are still asking "do we know this" or emailing to "confirm
the pricing" or rebuilding the customer profile, the base is not working. Make it simpler. Make
it more visible. Use the synthesis layer.

A knowledge base that gets used beats a perfect knowledge base that does not.
