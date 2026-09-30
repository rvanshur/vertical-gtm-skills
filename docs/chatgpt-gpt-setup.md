# Build Your GPT: Running This Suite in ChatGPT

You do not need Claude Code to use these skills. Every skill is a plain markdown file
(`SKILL.md`), and ChatGPT's custom GPT builder can run one as the brain of a GPT: the skill
becomes the GPT's playbook, and your client profile becomes its knowledge of your business.

> **Status:** this guide is written from ChatGPT's published GPT builder and has not yet been
> walked through end to end on every skill. If something here does not match what you see,
> the loader block and the two-file pattern are the parts that matter.

The system is the same on every platform:

```
Step 1: Build your context layer      profiles/client-profile.md (one file, done once)
Step 2: Give the assistant a skill    SKILL.md (the methodology, the contracts, the output shape)
Step 3: Make it yours                 adapt the skill to your motion (see "Adapting Your Own Version" below)
```

---

## Before You Build: Complete Your Client Profile

Everything depends on this. Fill out [`profiles/client-profile-template.md`](../profiles/client-profile-template.md)
and save your completed copy as `client-profile.md`. The [Lexora example](../profiles/examples/legal-ops-example.md)
shows the density to aim for, and you can upload it as-is to try a GPT before writing your own.
A GPT with a thin profile produces generic output, because the skill cannot invent your ICP,
personas or proof points.

No file system exists inside a GPT, so the profile travels as an **uploaded knowledge file**
instead of a path reference. Same file, different delivery.

---

## Pattern A: One GPT per Skill (Recommended)

Best for the skills you run daily. A "Meeting Prep" GPT that does one thing well beats a
do-everything GPT that has to guess which playbook you meant.

1. In ChatGPT, go to **GPTs, then Create**, and use the **Configure** tab. Skip the chat-based
   builder, since you already have the instructions.
2. **Name / Description:** name it after the skill, for example `Meeting Prep for [Your Company]`.
3. **Instructions:** paste the loader block below. Keep it compact. The instructions field has a
   size limit, and the full methodology lives in the knowledge file, not here.
4. **Knowledge:** upload exactly two files:
   - the skill's `SKILL.md` (for example `skills/06-meeting-prep/SKILL.md`)
   - your completed `client-profile.md`
5. **Capabilities:** enable web browsing if the skill does research (03, 04, 12). The rest
   work without it. Code interpreter and image generation stay off.
6. **Conversation starters:** copy the skill's example inputs. Every `SKILL.md` has an Examples
   section, and all of them use the Lexora case study.
7. **Sharing: keep it "Only me" or invite-link.** Your client profile contains your ICP,
   competitive positioning and named proof points. **Never publish a GPT to the store with your
   profile attached.**

### The Loader Block (Paste Into Instructions)

```
You implement one sales methodology skill, defined in the attached SKILL.md. It is your
only playbook. Follow it exactly: its Role, Input Contract, Output Contract, Methodology,
and output format.

Rules:
1. Before any task, consult the attached client-profile.md for company data: ICP, personas,
   pain points, value props, competitors, proof points. Never invent this data. If a needed
   field is missing from the profile, say which one and ask for it.
2. Honor the Input Contract: if required inputs are missing from my request, ask for them
   before producing output. Do not guess.
3. Produce the Output Contract's artifact in full, same sections, same order, every run.
4. Where SKILL.md says to read profiles/client-profile.md, that means the attached
   client-profile.md file.
5. If I ask for something outside this skill's scope, say which skill in the suite covers it
   (SKILL.md's "Integration with Other Skills" section lists them) rather than improvising.
```

## Pattern B: One Suite GPT (All Skills, One Assistant)

Upload your `client-profile.md` plus the `SKILL.md` files you actually use. Stay well under the
knowledge-file limit: 5-8 skills is the practical sweet spot, because retrieval gets less
reliable as the pile grows. Add one routing line to the top of the loader block:

```
You implement a suite of sales methodology skills, one per attached SKILL.md. First decide
which skill my request matches (each file's frontmatter has a name and description). Say
which skill you selected, then follow that file exactly per the rules below.
```

The trade-off, stated plainly: Pattern B is more convenient and measurably mushier. Retrieval
sometimes blends two skills' instructions. For anything scored or graded (08, 09, 13), use a
dedicated Pattern A GPT.

## Also Works: a ChatGPT Project

If you have ChatGPT Projects, the same two-file pattern works with project files plus project
instructions: same loader block, no GPT publishing step. Claude.ai users can set up the same
thing as a Claude Project.

## The Operating Skills in ChatGPT

The 15 skills in `operating/` work the same way (skill file plus profile), with two caveats.
Weekly Review, Graph Health, Dream and Ingest expect a folder-based knowledge base, which a GPT
does not have, so they are best run in Claude Code. And Second Opinion is naturally a job for
ChatGPT when your work is built in Claude: paste the review packet it produces into ChatGPT, and
you have your second vendor.

---

## Adapting Your Own Version

The suite is a framework, not a fixed product. The intended path:

1. **Run it stock first** on 2-3 real accounts. You cannot judge a customization you have not
   compared to the baseline.
2. **Adapt in conversation.** Every skill, sales and operating alike, ships a `CUSTOMIZE.md`: a
   paste-in prompt that interviews you about your motion and tells you what to change in the
   skill and in your profile. [`docs/customization.md`](customization.md) covers swapping
   methodologies (SPIN to Sandler, MEDDPICC weights) and adjusting scoring.
3. **Save the result as your own SKILL.md.** Keep the five-part anatomy (Role, Input Contract,
   Output Contract, Methodology, Context), so the file stays portable across Claude Code, Codex
   and ChatGPT.
4. **Re-upload to your GPT.** Knowledge files do not live-sync. Every time you revise the skill
   or the profile, delete the old file in Configure, then Knowledge, and upload the new one.
   Stale knowledge is the most common silent failure of skill-based GPTs.

---

## Known Limits vs. the CLI Platforms

| | Claude Code / Codex | ChatGPT GPT |
|---|---|---|
| Reads profile automatically | Yes, from the path | From uploaded knowledge (re-upload on change) |
| Writes output files | Yes, to `output/` | No, so copy artifacts out of the chat |
| Chains skills in one session | Yes | One GPT per skill (Pattern A) or routed (Pattern B) |
| Runs scripts / mechanical gates | Yes | No |
| Team distribution | Shared repo | Invite-link GPT (profile stays private) |

If your team lives in ChatGPT, this gets you the full methodology. If you outgrow it (you want
file outputs, skill chaining, or gates the system enforces), that is what the CLI setup in the
[README](../README.md#quick-start-15-minutes) is for.
