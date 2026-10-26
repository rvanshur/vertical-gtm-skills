# Customize: Stakeholder Mapping

A paste-in interview that adapts this skill to your market. It asks how your buying committees are built, which non-buyers slow your deals, and which hidden stakeholders keep appearing, then writes the Buying Committee section of your client profile.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The Prompt

```
You are helping me adapt a sales methodology skill to my company's buying committees.

Read the attached SKILL.md (gtm-stakeholder-mapping). It maps the buying committee for one account: it classifies each contact by buying role, places the non-buyers who still shape the deal, marks each missing decision-maker as an UNKNOWN ghost node, scores multi-threading, and writes an engagement plan.

Your job is NOT to rewrite it. It is to make it fire on my accounts, my personas and my market, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Translate the buying roles into MY market's titles. Who is the economic buyer in a single-site independent operator, a combination operator, a family-owned multi-site group, or whatever my accounts look like?

2. Non-buyers: which people who never sign still slow or stop our deals (technical reviewer, systems administrator, general counsel, operations head, procurement, or others in my market)? For each, what do they usually ask for, and how do they usually behave? Mark every answer as my hypothesis until a call confirmed it.

3. Ghost nodes: tell me about a deal that stalled because of someone who never appeared in the CRM. Who was it, and what would have surfaced them earlier?

4. Threading: in my wins and losses, how many named contacts were engaged, and which roles did they cover? Even a rough count from my last five wins beats the default.

5. Standing tensions: which political patterns repeat in my accounts (IT against operations, corporate against the site, owner against general manager)? Name the ones to check on every deal.

6. Available plays: which engagement moves can my team actually run (an executive call brokered by the champion, a site visit, an event invitation, a peer reference)? The map is only useful if the moves exist.

Then produce:

A. A revised "Quick Reference" written in terms of MY accounts and titles, not generic ones.
B. A revised "Examples" section built from my real answers, recognizable to my team, naming no individual.
C. The Buying Committee section for my client profile, using the exact field names below, with the values I gave you. Ready to paste.
D. THE HONEST PART: the questions above I could not answer concretely, and what I would need to gather to answer them. Do not paper over these. An answer I guessed at is a gap, and the gap is the finding.

Start with question 1.
```

---

## What You Should Expect To Happen

Question 4 stalls when contact roles were never recorded, because threading history cannot be rebuilt from notes that do not say who was in the room. Question 3 is answered at once, since everyone has a ghost-node story, and then stalls on what would have surfaced that person earlier. That second stall is the part that changes behavior.

Both stalls point at the same missing thing: a context layer. The skill is a procedure. A procedure needs to know who you sell to, which people never sign but still decide, what has worked, and what has already gone wrong. That is what `profiles/client-profile.md` is for. Build it once, and every skill in the suite inherits it.

---

## Minimum Profile Fields This Skill Reads

Add this section to `profiles/client-profile.md` once. Each field is read by a step in the skill:

```markdown
## Buying Committee
- **Role-title map:** [buying role, and the titles that fill it in our market]
- **Non-buyer rows:** [each non-buyer who slows or stops our deals, why they matter here, and their usual stance as a hypothesis]
- **Ghost patterns:** [where hidden stakeholders live in our accounts, by account type]
- **Threading benchmark:** [named contacts and roles in our wins versus our losses, with the count]
- **Standing tensions:** [the political patterns to check on every deal]
- **Available plays:** [engagement moves our team can actually run]
```

---

## Map What Is True, Not What Is Complete

An UNKNOWN in a role slot is information. A guessed name is contamination. The skill's value is showing where the map is still empty while there is time to fill it.
