# Customize: Dream

A paste-in prompt that adapts this consolidation skill to *your* knowledge system.

Works in **Claude Code**, **Claude.ai Projects**, or **OpenAI Codex**, all three read the same
`SKILL.md` format. Open the assistant, paste the block below, and answer its questions.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The prompt

```
You are helping me adapt an operating-discipline skill to my knowledge system.

Read the attached SKILL.md (gtm-dream). It is a consolidation pass that prunes
stale, contradicted, or duplicated items from a knowledge base. It has one hard
rule: de-link (strip the markup around dead links) but never de-line (delete
the entire entry).

Your job is NOT to rewrite the rule. It is to make the consolidation process
match MY system and MY tolerance for automation, and to tell me honestly where
my system needs human judgment that this skill cannot provide.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What does stale mean in your system? (Examples: no updates in 30 days, 
   marked as "draft" after 60 days, no date field so staleness is unmeasurable.
   Be specific about what signal tells you something is old.)

2. Do your items carry an expiry date or a "valid until" field? If yes, what 
   is the exact field name? If no, say so.

3. How would you want to handle stale items? (Examples: archive them, move to 
   a separate "historical" folder, mark with a warning, ask for confirmation
   before using them. What is the right action for your workflow?)

4. What would it cost you to merge two items that turned out to be about 
   different topics? (Examples: confusing, data loss, merge back? Or not much?)

5. The skill has a hard rule: de-link (strip dead links) but never de-line 
   (delete the entry). Does that rule work for you, or do you have a different
   comfort level? (Example: you might want to delete entire entries if they 
   are only one sentence and the link is dead.)

6. Have you ever discovered that two items in your KB were saying different 
   things about the same topic? What tipped you off? What would be a concrete
   way to catch that automatically?

7. When you run consolidation, how much can you automate without asking first?
   (Examples: "nothing, ask me before every change," "fix markup-only stuff 
   automatically," "delete anything marked as obsolete." What is your tolerance?)

Then produce:

A. The exact age thresholds for "stale" and "critical" in your system.

B. A revised workflow for handling stale items (archive / move / mark / ask).

C. The list of metadata fields (date fields, status fields, link formats) 
   the skill needs to read your items correctly.

D. A description of what "stale" looks like across MY KB. (Not generic stale,
   but: files older than X with Y metadata, or modified before Z. The exact
   pattern that catches stale in my system.)

E. THE HONEST PART: what you would NOT automate. (Examples: "never auto-delete
   items without asking," "we don't track dates so staleness is unmeasurable,"
   "we don't have duplicates because we merge immediately." Say what the skill
   cannot do in your system, and why.)

Start with question 1.
```

---

## What you should expect to happen

Question 3 and question 7 are the key ones. Most operators can describe their
data but stall on defining their own comfort level with automation.

That stall is important. **The skill's job is to flag problems. Your job is to
decide what to do.** If you find yourself hesitant about automation on something
that feels like it should be automatic, that hesitation is data. It often means
the category is more subtle than it looks.

---

## Minimum profile fields this skill reads

Add these to your operation's context file once, and every skill that uses this one
inherits them:

```markdown
## Knowledge Base Consolidation

- **Stale threshold:** [days of inactivity before an item is flagged]
- **Critical age:** [days at which an item absolutely must be decided on]
- **Expiry field name:** [field name if used, or "not used"]
- **Stale handling:** [archive / move / mark / ask]
- **Automation tolerance:** [nothing / markup-only / conservative / aggressive]
- **Metadata:** [exact field names: created, updated, status, links, etc.]
```

---

## The de-link rule: when to adapt it

The core rule, de-link but never de-line, is built for systems where knowledge
items are larger than a single sentence. If your system uses atomic single-line
items, you may want to skip the de-link rule or adapt it.

Ask yourself: **what is the smallest valuable thing you store?** If it is a single
sentence, de-linking leaves you with nothing. If it is a paragraph or longer,
de-linking preserves the context.

Adapt the rule to your system's granularity.
