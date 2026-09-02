# Customize: Stakeholder Mapping

A paste-in prompt that adapts this skill to *your* go-to-market motion.

Works in **Claude Code**, **OpenAI Codex**, **Claude.ai / ChatGPT Projects**, or a **custom GPT**
(attach `SKILL.md` as knowledge and paste the block below) -- they all read the same `SKILL.md`
format. Open the assistant, paste the block, and answer its questions.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The prompt

```
You are helping me adapt a GTM methodology skill to my company's go-to-market motion.

Read the attached SKILL.md (gtm-stakeholder-mapping). It builds the buying-committee map: 7-role classification, org hierarchy with ghost nodes, a weighted multi-threading score, and an engagement plan.

Your job is NOT to rewrite it. It is to make it fire on my accounts, my personas, and my
vertical, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Translate the seven buying roles into YOUR vertical's titles. Who is the economic buyer
   in a 200-person specialty contractor, a regional healthcare group, a franchise operator --
   whatever your accounts look like?

2. Ghost nodes: tell me about a deal that died because of someone who never appeared in
   the CRM. Who were they, and what would have surfaced them earlier?

3. What does multi-threading actually look like in your wins vs losses -- how many
   contacts, which roles covered? Even a rough count from your last five wins beats the
   default weights.

4. What political patterns repeat in your vertical -- IT vs operations, corporate vs
   branch, owner vs general manager? Name the standing tensions.

5. Which engagement moves are available and acceptable in your motion -- exec sponsor
   calls, site visits, event invites, peer references? The map is only useful if the moves
   exist.

Then produce:

A. A revised "Quick Reference" written in terms of MY accounts, personas, and vertical,
   not generic ones.
B. A revised "Examples" section built from the real answers I gave you, recognizable to my
   team but naming no individual.
C. The fields this skill now needs from profiles/client-profile.md, with the exact values
   I gave you, ready to paste in.
D. THE HONEST PART: the questions above I could not answer concretely, and what I would
   need to gather to answer them. Do not paper over these. An answer I guessed at is a
   gap, and the gap is the finding.

Start with question 1.
```

---

## What you should expect to happen

**Question 3 stalls** when contact roles were never recorded, so threading history cannot be
reconstructed. **Question 2 is answered instantly** -- everyone has the ghost-node story --
and then stalls on "what would have surfaced them," which is the part that changes behavior.

Both kinds of stall point at the same missing thing: a **context layer**. The skill is a
procedure. A procedure needs to know who you sell to, what has worked, and what has already
gone wrong. That is what `profiles/client-profile.md` is for -- build it once and every skill
in the suite inherits it.

---

## Minimum profile fields this skill reads

Add these to `profiles/client-profile.md` once:

```markdown
## Buying Committee
- **Role-title map:** [buying role -> titles in our vertical]
- **Ghost patterns:** [where hidden stakeholders live in our accounts]
- **Threading benchmark:** [contacts and roles in wins vs losses]
- **Standing tensions:** [the political patterns to check every deal for]
- **Available plays:** [engagement moves we can actually run]
```

---

## Map what is true, not what is complete

An UNKNOWN in a role slot is information; a guessed name is contamination. The skill's value
is showing you where the map is empty while there is still time to fill it.
