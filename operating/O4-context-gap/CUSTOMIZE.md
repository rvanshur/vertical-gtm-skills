# Customize: Context Gap

A paste-in prompt that adapts this skill to your go-to-market motion.

Works in **Claude Code**, **Claude.ai Projects**, or **OpenAI Codex**, all three read the same
`SKILL.md` format. Open the assistant, paste the block below, and answer its questions.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The prompt

```
You are helping me adapt an operating-discipline skill to my company's go-to-market motion.

Read the attached SKILL.md (gtm-context-gap). It runs a discovery search before any build,
sorts findings into six buckets, and says what the next step is given the bucket.

Your job is NOT to rewrite it. It is to make it fire on the things that actually get built
at my company, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Where does our company store existing work? (codebase folders, knowledge base, Notion,
   prior project folders, confluence, other, everything)

2. What is the most recent time we built something twice without realizing it was already
   done? (What was it, and where was the original hiding?)

3. How many requests per month do we actually get, and how many of those turn out to be
   "already done" once we look?

4. What counts as "scaffolding exists" in our setup? (A folder structure? A partial
   implementation? A template? Other?)

5. If nothing is found in the search, how do we know we actually searched? (Do we log it?
   Do we name the places we looked? Or does it just feel like we looked?)

Then produce:

A. A revised "Core Workflow" where each step is written against MY locations (folders,
   knowledge bases, tools) and MY definition of done, not generic ones.

B. A revised "Best Practices" using MY near-miss from question 2, written so it is
   recognizable to my team but names no individual.

C. A map of where things live in our setup (codebase locations, KB sections, tools, prior
   projects) so the search protocol is concrete.

D. THE HONEST PART: a short list of the questions above I could not answer concretely.
   If we do not have a consistent place where "existing work" lives, that gap is the
   finding, and it is more important to address than any single missing feature. If we
   build things but never consolidate or document them, that is the blocker this skill
   cannot fix, we have to fix that first.

Start with question 1.
```

---

## What you should expect to happen

Questions 1 and 2 usually land. Question 3 stalls when we have never counted. Question 4
stalls when "scaffolding" is vague, there is no clear distinction between "worth extending"
and "might as well rebuild." Question 5 is where most teams stall hardest. If you have no
systematic place to say "we looked there," then you have no way to prove a gap is real.

If output section D is long, that is the work. This skill assumes you have a place where
existing work lives and can be found. If you do not, the skill cannot help until you do.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once, and every skill in the suite inherits them:

```markdown
## Knowledge Locations

- **Codebase:** [primary repo location and key folders where features live]
- **Knowledge base:** [Notion, Confluence, wiki, etc. and how it is organized]
- **Prior projects:** [where old work and templates are stored]
- **Tools / integrations:** [systems where solutions may already exist]
- **Definition of "existing":** [what counts as already-done vs. scaffolding vs. true gap]
```
