# Customize: Trigger Event Outbound

A paste-in interview that writes your Trigger Catalog, the profile section this skill reads. It asks
one question at a time, asks you to name the events that actually opened deals for you, and records
only the windows and citations you can defend. It does not write the skill for you.

Works in Claude Code, in Codex, and in ChatGPT as a custom GPT.

> For customizing the whole suite at once, see [`docs/customization.md`](../../docs/customization.md)
> and [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The Prompt

```
You are helping me adapt a GTM methodology skill to my company's go-to-market motion.

Read the attached SKILL.md (gtm-trigger-event-outbound). It classifies a dated business event, checks the event against its window, and drafts a short sequence only while the window is open.

Your job is NOT to rewrite the skill. It is to make it fire on my accounts, my personas and my vertical, and to tell me plainly where you cannot answer.

Ask me these questions, ONE AT A TIME, and wait for each answer:

1. List the trigger events that have actually opened deals for us in the last year, not the ones that should in theory. For each one: what happened, how we heard about it, and how fast we moved.

2. For each event type, what is the honest window? An acquisition might stay warm for 90 days and a records finding for 10. Give the window in days from the event date, based on our own deals.

3. What rule or deadline does each event create, and where is it written? Name the regulation, filing or contract date and its source. If there is no deadline, say so.

4. Who acts on each event? Which persona has to respond, and which persona only hears about it?

5. For each event type, which proof point do we hold with the status Verified or Benchmark, and what is its source? If we hold none, say so.

6. Which events are landmines in our vertical, such as deaths, lawsuits, layoffs or disasters, where outreach reads as ambulance-chasing? These go on the taboo list.

Then produce, in this order:

A. THE HONEST PART: the questions above I could not answer concretely, and what I would need to gather to answer them. Do not paper over these. An answer you guessed at is a gap, and the gap is the finding.

B. Every window I gave you without a source. Mark each one UNSOURCED and keep it out of any sequence.

C. A section headed exactly "## Trigger Catalog", in this shape: a table with the columns Trigger, Rule or deadline it creates (citation), Proof point that fits, Credible first line, then two bullets, Monitoring sources and Taboo events. Fill it with my answers. It must be ready to paste.

Start with question 1.
```

---

## What You Should Expect to Happen

**Question 2 stalls** when trigger-driven wins were never tagged in the CRM, so nobody can say which
events produce pipeline and which only produce activity. **Question 6 is skipped** more often than it
stalls, and one ambulance-chasing email costs more goodwill in a tight vertical than a quarter of
good ones earn.

Both stalls point at the same missing piece, a **context layer**. The skill is a procedure, and a
procedure needs to know who you sell to, what has worked and what has already gone wrong. That is
what `profiles/client-profile.md` is for. Build it once and every skill in the suite inherits it.

---

## Minimum Profile Fields This Skill Reads

Add this section to `profiles/client-profile.md`. The fields match the Trigger Catalog shape in the
client profile template exactly. The skill also reads Industry Context, the Buying Triggers table and
Proof Points, which other interviews and sections write.

```markdown
## Trigger Catalog
| Trigger | Rule or deadline it creates (citation) | Proof point that fits | Credible first line |
|---|---|---|---|
- **Monitoring sources:** [source, event types it surfaces, lag]
- **Taboo events:** [what we never trigger outreach on]
```

---

## If You Want to Stretch a Window

Windows shrink. They do not stretch. When a sequence underperforms, the instinct is to widen the
window and send anyway. The event is the permission to write. An expired event is a cold email
wearing a costume.
