# Customize: Wrap-up

A paste-in prompt that adapts this session-close skill to *your* workflow.

Works in **Claude Code**, **Claude.ai Projects**, or **OpenAI Codex**, all three read the same
`SKILL.md` format. Open the assistant, paste the block below, and answer its questions.

> This is a per-skill companion. For customizing the whole suite at once, see
> [`docs/customization.md`](../../docs/customization.md) and
> [`profiles/client-profile-template.md`](../../profiles/client-profile-template.md).

---

## The prompt

```
You are helping me adapt a session-close skill to my workflow.

Read the attached SKILL.md (gtm-wrap-up). It closes a working session with a
written handoff: what happened, where we stopped, and one next action stated
with enough precision that someone could resume the work cold.

Your job is NOT to rewrite the handoff format. It is to make the skill work
for MY type of work and MY project structure, and to tell me honestly what
work patterns I have that the skill cannot capture.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What types of work do you do in a typical session? (Examples: writing code,
   content creation, research, analysis, configuration. Be concrete.)

2. At the end of a session, what is the state you care most about? (Examples:
   uncommitted git changes, file-level status, running service state, database
   changes, browser state. What actually matters for the next person to know?)

3. How many projects do you usually touch in one session? (One typically, or do
   you context-switch across several? This determines artifact structure.)

4. When you write "next action", what format is it usually in? (Examples: a git
   command, a file path, a person's name, a ticket number. What is the actual
   form it takes for you?)

5. The skill has a "next action" gate with four tests. Does that gate work for
   your work? Are there types of next actions you have that would fail the tests?
   (Example: "sometimes next action is a decision, not a command.")

6. What does "resumable cold" mean for your work? (Examples: I could hand the
   file to someone else and they could continue. I could come back tomorrow
   and know exactly where to start. Or something else?)

7. When you ended your last working session, what did you NOT write down that
   you wished you had the next day?

Then produce:

A. The exact format for storing continuation artifacts in your system. (The path,
   the frontmatter fields you need, the body sections that matter.)

B. For each type of work you do, what the "state" section should capture. (Not
   generic, but: when you are writing code, what matters. When you are writing
   content, what matters.)

C. A worked example of a next action from YOUR real work, with annotation showing
   how it passes (or fails) the four tests.

D. THE HONEST PART: what work you do that this skill cannot cover. (Examples:
   "I work in a UI builder, there is no 'next action', just current state". "My work is asynchronous, continuation means 'wait for external input' not
   'continue yourself.'" Say what is different.)

Start with question 1.
```

---

## What you should expect to happen

Question 2 and question 7 are where the real personalization happens. Most people
know their projects (Q1, Q3-4) and can describe their tools (Q5-6), but struggle
with question 2 (what state matters) because the answer is highly specific to
their work.

That specificity is valuable. **The state section is what the next session actually
uses.** If it is too vague, the handoff fails. If it is too detailed, you will not
write it twice.

---

## Minimum profile fields this skill reads

Add these to your operation's context file once, and every skill that uses this one
inherits them:

```markdown
## Session Handoff

- **Artifact storage:** [where continuation notes are saved]
- **Artifact format:** [markdown / YAML / JSON, the structure]
- **Project structure:** [single project, multi-project, unclear]
- **State precision:** [what details matter for resumption in your work]
- **Next action format:** [how you typically express "what comes next"]
- **Definition of done:** [for a work session to be "done", what has to happen]
```

---

## The four-test gate: when to adapt it

The four tests (imperative / named object / single step / resumable cold) are built
for work that is sequential and resumable (code, writing, analysis). If your work
is different, adapt the tests.

Ask yourself: **is my next action something the next session can DO, or something
they need to KNOW about?** If it is "wait for feedback from X," the imperative test
fails. If it is "the build is currently red for reason Y," that is state, not action.

Adapt the tests to your work type.
