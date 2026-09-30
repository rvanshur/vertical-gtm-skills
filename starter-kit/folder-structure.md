# Recommended Folder Structure

How to lay out the skills so every one of them finds your client profile.

**The one rule:** every skill reads its data from `profiles/client-profile.md`, relative to the
repo root. Whatever layout you choose, that path has to hold your active profile, or you have to
tell Claude where the profile is (see Option B in [Getting Started](../docs/getting-started.md#step-3-run-the-skills-from-where-you-work)).

---

## Basic Setup (Individual User)

Work straight from your clone of this repo. Nothing to move.

```
vertical-gtm-skills/
├── CLAUDE.md                    # Loads automatically, routes you to the right skill
├── profiles/
│   ├── client-profile.md        # YOUR profile (gitignored, never committed)
│   ├── client-profile-template.md
│   └── examples/legal-ops-example.md
├── skills/                      # The 14 sales skills
├── operating/                   # The 15 operating skills
└── output/                      # Generated call sheets, scorecards, sequences (gitignored)
```

---

## Team Setup (Shared Repo)

Fork the repo for your team. Decide deliberately where the shared profile lives, because
`profiles/client-profile.md` is gitignored by default. Either remove that line from your fork's
`.gitignore` (if the repo is private and the whole team should share one profile), or keep the
profile in your team's document system and copy it into place.

```
team-gtm-system/                 # your fork
├── CLAUDE.md                    # Keep the repo's version, add your team's rules at the bottom
├── profiles/
│   └── client-profile.md        # The shared profile
├── skills/                      # All 14 sales skills
├── operating/                   # The operating skills your team uses
├── output/                      # Saved skill outputs
│   ├── deal-scores/             # Deal Pulse reports
│   ├── call-coaching/           # Coaching reports
│   └── outbound/                # Generated sequences
└── knowledge_base/              # Only if you run O11 Context OS Setup
```

---

## Consultant Setup (Multiple Clients)

The skills never change between clients. Only the profile does. Keep each client's profile
next to the others and copy the active one into place when you switch engagements.

```
vertical-gtm-skills/
├── profiles/
│   ├── client-profile.md        # The ACTIVE client (copied from below)
│   └── clients/
│       ├── client-a.md
│       ├── client-b.md
│       └── client-c.md
├── skills/
├── operating/
└── output/
    ├── client-a/
    ├── client-b/
    └── client-c/
```

Switching clients:
```bash
cp profiles/clients/client-b.md profiles/client-profile.md
```

Add `profiles/clients/` to `.gitignore` too, since each file holds that client's competitive data.

**Why this works:** the skills directory never changes between clients. Only the Client Profile
swaps. That is what makes the system portable across verticals.
