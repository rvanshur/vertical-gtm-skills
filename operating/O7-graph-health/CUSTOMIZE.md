# Customize: Graph Health

A paste-in prompt that adapts this skill to *your* knowledge system.

Works in **Claude Code**, **Claude.ai Projects**, or **OpenAI Codex**, all three read the same
`SKILL.md` format. Open the assistant, paste the block below, and answer its questions.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The prompt

```
You are helping me adapt an operating-discipline skill to my knowledge system.

Read the attached SKILL.md (gtm-graph-health). It measures the structure health of a
knowledge base (tag sprawl, link density, provisional item age) and produces a score
that you can track over time.

Your job is NOT to rewrite it. It is to make it measure what actually matters to MY
system, and to tell me honestly where my system differs from the default assumptions.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What do you call the files where you store knowledge? (Examples: notes, nodes, 
   documents, records, cards, whatever term your system uses)

2. What metadata does each item carry? (Examples: status, type, domain, tags, created_date,
   updated_date, links. Does it have a frontmatter block, a header comment, inline metadata?)

3. Does your system have a blessed list of tags (a taxonomy or tag guide)? If yes, where
   is it? If no, say so plainly.

4. How do items link to each other? (Examples: [[wiki-links]], markdown links, 
   YAML arrays, database foreign keys. Be specific about the format.)

5. What makes an item "provisional" or "incomplete" in your system? (Examples: a status
   field marked "emergent", a TODO in the content, a missing-data marker. What signals
   that an item is still forming?)

6. The skill checks for broken links and orphan items. In your system, what does each
   one mean? (An orphan is an item with few or no connections. Is that a problem in
   your system, or do you use a different discovery pattern? A broken link is a 
   reference to an item that doesn't exist. Would you even notice that?)

7. What has it cost you when your knowledge base structure broke? Specific example:
   a time you looked for something and could not find it, or a rule that fragments
   the search surface and nobody noticed until it was too late.

Then produce:

A. The exact paths and commands I should run every time I measure structure health.

B. A revised "Quick Reference" table where thresholds are tuned to MY system.
   (The defaults might be right, or you might need different ones.)

C. A revised metadata parsing section that reads MY item format, not generic ones.

D. THE HONEST PART: a short list of the questions above MY system does NOT fit.
   If I don't use tags, that threshold is meaningless. If I use full-text search
   instead of links, orphans are not a problem. Say it plainly.

Start with question 1.
```

---

## What you should expect to happen

Most systems get through questions 1-2. Question 7, the specific cost of breakage,
stalls more than it should, which is the whole point. **The question exists because 
most operators have not measured the cost of structure decay, only the inconvenience.**

If you cannot remember a specific incident, say so. That means either your system is
new enough to not have accumulated decay yet, or you have not had to search for old
knowledge when structure has fragmented. Both are valid. The skill is insurance.

---

## Minimum profile fields this skill reads

Add these to your operation's context file once, and every skill that uses this one
inherits them:

```markdown
## Knowledge Base Structure

- **KB location:** [path to the directory where items are stored]
- **Taxonomy file:** [path to the blessed tag list, or "none" if not used]
- **Item metadata format:** [description of how items are marked up]
- **Link format:** [how items reference each other]
- **Status values:** [the values used to mark an item as emergent/provisional]
- **Discovery pattern:** [links, full-text search, other]
```

---

## Thresholds: when to customize them

The default thresholds in the skill are based on single-operator knowledge bases and team
wikis. If your system is different, adapt them:

- **Tag sprawl:** Single-person system vs. team system may have different optimal sprawl.
  A team with multiple entry points expects higher sprawl. Adjust 20%/40% if it makes sense.
- **Orphan threshold:** If you use full-text search, orphans are not a problem. If you rely
  on link-following, lower the threshold (maybe 1 link is enough for your use case).
- **Hub threshold:** If your system expects hub items (tables of contents, index pages),
  raise or remove the threshold.
- **Age thresholds:** If your "provisional" status is meant to be permanent for certain
  items (e.g., "in progress" work), adjust or remove the aging rule.

Thresholds are recommendations, not laws. Change them.
