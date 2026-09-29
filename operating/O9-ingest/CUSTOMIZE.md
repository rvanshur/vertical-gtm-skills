# Customize: Ingest

A paste-in prompt that adapts this skill to *your* knowledge system.

Works in **Claude Code**, **Claude.ai Projects**, or **OpenAI Codex**, all three read the same
`SKILL.md` format. Open the assistant, paste the block below, and answer its questions.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The prompt

```
You are helping me adapt an ingest skill to my knowledge system.

Read the attached SKILL.md (gtm-ingest). It extracts concepts from raw content
and structures them into knowledge items with compiled truth + timeline, metadata,
and connections to related items.

Your job is NOT to rewrite the structure. It is to make the skill ingest in a way
that fits MY content and MY system, and to tell me honestly where my system differs
from the assumptions.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What sources do you ingest most often? (Examples: call transcripts, meeting notes,
   documents, research summaries, Slack threads, emails. Be specific.)

2. What format are your sources in? (Examples: plain text, markdown, PDFs, Notion pages,
   recorded calls to transcribe. Are they already structured, or do you start with noise?)

3. When you read a source, how do you decide what to keep and what to skip? (Examples:
   decisions get captured, speculation gets skipped. Pain points get captured, pleasantries 
   don't. What is your extraction heuristic?)

4. What do you call your knowledge items, and where do you store them? (Examples: notes, 
   documents, records, artifacts. A file system, a database, a wiki, a Notion workspace?)

5. Do your items currently have any structure (sections, metadata, timestamps)? If yes,
   describe it. If no, and you are starting from scratch, that is valid. Say so.

6. How do your items currently link to each other? (Examples: [[wiki-links]], markdown
   links, a database, manually maintained indexes. Or do they not link at all yet?)

7. The skill has a special rule: one person gets one record, with a timeline of every
   interaction. Do you use person entities, or something else? (Examples: contact records,
   customer profiles, team member pages. Or no person tracking at all?)

8. What has it cost you when knowledge was NOT captured and structured? Specific example:
   a time you needed an answer and it was gone because nobody captured it before.

Then produce:

A. The exact frontmatter and section structure for YOUR items. (Not generic, but the
   exact format I should use going forward.)

B. The extraction heuristic for YOUR most common content type. (When you ingest a call
   transcript / meeting notes / document, what specifically do you keep?)

C. The mapping: which types of source content → which types of knowledge items.

D. THE HONEST PART: what parts of the skill do NOT apply to you, and why. (Examples:
   "we don't have person tracking," "our items are atomic single sentences," "we use 
   full-text search, not links." Say what is different.)

Start with question 1.
```

---

## What you should expect to happen

Question 3 and question 8 are where the real work happens. Most operators know what
sources they have (Q1-2) and can describe their system (Q4-7), but stall on stating
their extraction heuristic explicitly.

That stall is important. **The heuristic is what makes ingest work.** Without one,
every decision becomes a judgment call, and consistency evaporates. If you find
yourself hesitating on "what counts as important enough to capture," that hesitation
is the heuristic trying to be born. Write it down.

---

## Minimum profile fields this skill reads

Add these to your operation's context file once, and every skill that uses this one
inherits them:

```markdown
## Knowledge Ingestion

- **Item storage location:** [path or database where items live]
- **Item format:** [markdown / YAML / JSON / other, the exact structure]
- **Metadata fields:** [exact names: created, updated, status, tags, source, etc.]
- **Taxonomy:** [domain values, type values, status values, what is blessed]
- **Link format:** [how items reference each other]
- **Common sources:** [call transcripts, meeting notes, documents, what arrives most]
- **Extraction heuristic:** [what counts as important enough to capture]
```

---

## The compiled-truth/timeline split: when to adapt it

The structure assumes items are larger than a single sentence and worth updating
over time. If your system works differently (atomic single-line items, or items
that are never revised), adapt the structure.

Ask yourself: **will this item be rewritten as my understanding evolves?** If yes,
the compiled-truth/timeline split matters. If no, simplify the structure.

The timeline (append-only dated entries) is most valuable for items about people,
decisions, evolving opinions, and patterns. It is less valuable for static facts
(a company's founding date does not need a timeline).

Adapt to your mix of static vs. evolving knowledge.
