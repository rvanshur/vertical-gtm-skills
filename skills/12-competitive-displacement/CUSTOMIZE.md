# Customize: Competitive Displacement

This interview adapts the Competitive Displacement skill to your market. It asks five questions, one at a time, about the incumbents you displace, the failures you can prove, and how you learn contract timing. It then writes your Displacement section for the client profile, ready to paste.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The Prompt

```
You are helping me adapt a go-to-market skill to my company's motion.

Read the attached SKILL.md (gtm-competitive-displacement). It writes outbound sequences that displace a known incumbent. Its sequences are built on the incumbent's failure patterns, a displacement template per incumbent type, and proof points that are allowed to be cited.

Your job is NOT to rewrite the skill. It is to make it fire on my accounts, my personas and my market, and to tell me honestly where I cannot answer you.

Ask me these, ONE AT A TIME, and wait for each answer:

1. Whose installed base are you targeting, and why now? Name the event that makes this timely: a price increase, an end of life notice, an acquisition, a support collapse. Displacement outbound with no "why now" is just a claim that you are better.

2. Which of the incumbent's failure patterns can you PROVE? A failure counts only if a customer you won away described it in their own words. List only those, with the customer's words.

3. Your two or three won-away stories, with numbers: what was failing, what changed after the switch, and how long the migration took.

4. Switching cost, honestly: what does leaving this incumbent really involve? Data, retraining, integrations, contract exit. The sequence must survive the prospect asking.

5. Renewal timing: when do their contracts come up, and how do you find out? Public procurement records, asking on calls, industry chatter?

Then produce:

A. A revised "Quick Reference" written in terms of MY accounts, personas and market, not generic ones.

B. A revised "Examples" section built from the real answers I gave you, recognizable to my team but naming no individual.

C. The Displacement section for profiles/client-profile.md, with the exact values I gave you, in the field names below, ready to paste:
   - Incumbent template rows (one row per incumbent type, with Positioning, Wedge, three discovery questions, and the primary and secondary persona row numbers)
   - Difficulty tests (for each active incumbent, whether the three tests are met, with the evidence tag on each contract fact)
   - Proof points against incumbents (the Displaced vendor and Status for each proof point, read from the Proof Points table)
   - Renewal timing (the renewal month for each incumbent and how we learned it, tagged)
   - Won-away failure patterns (each pattern with the won-away customer's words and its tag)

D. THE HONEST PART: the questions above I could not answer concretely, and what I would need to gather to answer them. Do not paper over these. An answer I guessed at is a gap, and the gap is the finding.

Start with question 1.
```

---

## What You Should Expect To Happen

**Question 2 Stalls** when the failure patterns come from your own sales floor instead of from won-away customers. That gap is dangerous, because the incumbent's customers know their real failures better than you do. **Question 4 stalls** when nobody has written down an honest migration. "Seamless" is not a migration plan.

Both stalls point at the same missing thing, a context layer. The skill is a procedure, and a procedure needs to know who you sell to, what has worked, and what has already gone wrong. That is what `profiles/client-profile.md` is for. Build it once, and every skill in the suite inherits it.

---

## Minimum Profile Fields This Skill Reads

Add this section to `profiles/client-profile.md` once:

```markdown
## Displacement
- **Incumbent template rows:** one row per incumbent type, with Positioning (tagged), Wedge, three discovery questions, and the primary and secondary persona row numbers from Buyer Personas
- **Difficulty tests:** for each active incumbent, whether the no-term, 180-day renewal and exit-fee tests are met, each contract fact with its tag
- **Proof points against incumbents:** the Displaced vendor and Status for each proof point, read from the Proof Points table, where the customer rows stay
- **Renewal timing:** each incumbent's renewal month and how we learned it, tagged
- **Won-away failure patterns:** each pattern with the won-away customer's words and its tag
```

---

## The One Rule

Never send a failure-pattern claim you cannot trace to a won-away customer. The people receiving these emails live inside the incumbent's product. One wrong claim identifies you as a vendor who guesses.
