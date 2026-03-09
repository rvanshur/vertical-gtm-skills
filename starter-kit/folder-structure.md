# Recommended Folder Structure

How to organize the skills in your project for maximum usability.

---

## Basic Setup (Individual User)

```
your-project/
├── CLAUDE.md                    # Identity file (use identity-template.md)
├── client-profile.md            # Your completed Client Profile
└── skills/
    ├── 01-account-qualification/
    │   └── SKILL.md
    ├── 06-meeting-prep/
    │   └── SKILL.md
    ├── 08-deal-pulse/
    │   └── SKILL.md
    └── [only the skills you use]
```

## Team Setup (Shared Repo)

```
team-gtm-system/
├── CLAUDE.md                    # Team identity file
├── profiles/
│   └── client-profile.md       # Shared Client Profile
├── skills/                      # All 14 skills
│   ├── 01-account-qualification/
│   ├── 02-account-snapshot/
│   ├── ...
│   └── 14-sales-handoff/
├── output/                      # Saved skill outputs
│   ├── deal-scores/            # Deal Pulse reports
│   ├── call-coaching/          # Coaching reports
│   └── outbound/               # Generated sequences
└── docs/
    └── weekly-ops-checklist.md
```

## Consultant Setup (Multi-Client)

```
gtm-consulting/
├── CLAUDE.md                    # Consultant identity file
├── skills/                      # All 14 skills (methodology stays the same)
├── clients/
│   ├── client-a/
│   │   ├── client-profile.md   # Client A's profile
│   │   └── output/             # Client A's outputs
│   ├── client-b/
│   │   ├── client-profile.md   # Client B's profile
│   │   └── output/
│   └── client-c/
│       ├── client-profile.md
│       └── output/
└── templates/
    └── client-profile-template.md
```

**Key insight:** The skills directory never changes between clients. Only the Client Profile swaps. This is what makes the system portable across verticals.
