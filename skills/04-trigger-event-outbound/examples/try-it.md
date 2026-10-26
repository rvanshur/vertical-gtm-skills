# Try It: Trigger Event Outbound On Corrow Ridge Cemetery (Invented Example)

Every name, date and number in this file is invented for the PlotIQ example. Nothing here is a real company.

## Ask Your Assistant
"Run Trigger Event Outbound on Corrow Ridge Cemetery using skills/04-trigger-event-outbound/examples/try-it.md"

## The Records

Run date: 2026-10-19 (illustrative)
User role: BDR (Nadia Brandt)

The Event
- Event: Harborline Funeral Partners acquired Corrow Ridge Cemetery. Harborline is a 14-site regional consolidator (illustrative)
- Event date: 2026-07-01 [Public: state licensing database]
- Source: State licensing database, ownership change
- Trigger window: 60 to 120 days after the event date (profile Buying Triggers: consolidator buys the site)

The Account
- Account: Corrow Ridge Cemetery
- Footprint: One site, 14,000 plots (illustrative), paper plat maps
- Site budget: The general manager keeps the site budget until the integration review in Q1 2027 [CRM]
- Status: TARGET. No open deal and no owner [CRM]
- Acquirer's CFO or controller: [Unknown], not named in the CRM
- Harborline's system for its sites: [Unknown]

## What You Should Get

- Trigger type: Acquisition / M&A (profile trigger: consolidator buys the site). Event tag: [Public: state licensing database].
- Urgency window: 2026-08-30 to 2026-10-29. Days remaining: 10. Share remaining: 10 of 60 window days (17%). Trigger status: STALE, so the sequence runs.
- Sequence: three emails to the acquirer's CFO or controller, whose name is [Unknown]. The site GM's three emails are left out of this example.
- Email 1 (2026-10-20): subject "Corrow Ridge after the Harborline close". Email 2 (2026-10-23 to 2026-10-24) and Email 3 (2026-10-27 to 2026-10-29) follow.
- Proof point: none. The profile's proof point for this trigger is Illustrative, so no figure goes into any email.
- Next action: Nadia Brandt finds the acquirer's CFO or controller by 2026-10-20, then sends Email 1 after reading the draft.
