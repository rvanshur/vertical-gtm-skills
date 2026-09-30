# Changelog

What changed in this repo, newest first. Each skill also keeps its own Changelog section at the
bottom of its `SKILL.md`, with the detail.

---

## 2026-09-29: Final Pass Before Wider Release

**One case study, everywhere.** Every worked example in all 29 skills and the docs now uses the
same fictional company, Lexora (a legal-ops platform), and the same cast of accounts, people and
competitors. The cast is defined once, at the bottom of
[`profiles/examples/legal-ops-example.md`](profiles/examples/legal-ops-example.md), so you can
follow one deal (Corvane Industrial) from qualification to handoff.

**New docs**
- [`docs/how-it-fits.md`](docs/how-it-fits.md): how the profile, the 14 sales skills and the 15
  operating skills connect, what to set up first, which operating skill to use when, and what
  each skill reads from the profile.
- This changelog.

**Operating skills (O1 to O15)**
- Every operating skill now reads the profile section its `CUSTOMIZE.md` interview writes.
  Before this, the interviews told you to add a section the skill never loaded.
- **O5 Second Opinion 1.1.0** now works when the assistant running it is the builder's own
  vendor: it builds a review packet for a different vendor (paste into another vendor's chat, a
  second vendor's CLI, or an API call) and triages the findings that come back.
- **O11 to O13:** customization interviews expanded to match the others ("what to expect",
  profile sections, "if you are stuck"). O12's had a broken code block.
- **O12 to O15:** the Context sections name the profile sections they read, and say that
  validated findings go back into the profile, which is how strategy reaches the sales skills.
- **O15:** The Mom Test credited to Rob Fitzpatrick. Examples moved to the Lexora case study.

**Sales skills (01 to 14)**
- Worked examples rewritten around the Lexora case study (version 1.2.0 each).
- **14 Sales-to-CS Handoff:** profile section names now match the template (Core Pain Points,
  Product Modules), and the third date of the handoff plan is renamed "Full Adoption Date"
  (it was "Full Service Date", an internal term that meant nothing outside one company).

**Profile**
- The template gains a **Product Modules** section (Sales-to-CS Handoff reads it) and a note on
  the optional operating-layer sections.
- The Lexora example gains Product Modules, an adjacent competitor (LedgerLine Audit, an
  outsourced bill review service) and the Example Cast.

**Docs corrected**
- README and `CLAUDE.md` / `AGENTS.md` describe all 29 skills. The agent instructions route to
  every operating skill, not just O1.
- The customization guide opens with which profile sections feed which skills, and points to
  headings that exist. The skill reference's scoring section now matches the skills: Deal Pulse
  risk bands are 85 / 46 / 0, MEDDPICC is a weighted 0-100 score (not an unweighted /40), and the
  Call Coaching bands are the skill's own.
- Codex and ChatGPT setups are labelled as documented but not yet walked through end to end.
- The starter kit's folder layouts put the profile where the skills look for it.
- Example metrics that came from a real company were replaced with the Lexora profile's own.

---

## 2026-09-29: Operator's Toolkit Operating Skills

O2 to O15 published alongside the Operator's Toolkit series.

## 2026-09-02: Front Door

Root `CLAUDE.md` / `AGENTS.md`, the ChatGPT GPT guide, and a `CUSTOMIZE.md` for all 14 sales
skills.

## 2026-08-25: The Operating Layer Begins

`operating/` added, starting with O1 Verify.

## 2026-07-06: Version 1.1.0 of the Sales Skills

Moved every sales skill from a per-skill profile block to one shared `profiles/client-profile.md`,
and gave every skill the five-part anatomy (Role, Input Contract, Output Contract, Methodology,
Context).
