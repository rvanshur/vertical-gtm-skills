# Try It: Trigger Event Outbound On Corrow Ridge Cemetery (Invented Example)

Every name, date and number in this file is invented for the PlotIQ example. Nothing here is a real company.

## Ask Your Assistant
"Run Trigger Event Outbound on Corrow Ridge Cemetery using skills/04-trigger-event-outbound/examples/try-it.md and the PlotIQ profile at profiles/examples/plotiq-example.md. Treat today as 2026-10-19."

## The Records

Run date: 2026-10-19 (illustrative)
User role: BDR (Nadia Brandt)

The Event
- Event: Harborline Funeral Partners acquired Corrow Ridge Cemetery. Harborline is a 14-site regional consolidator [Public: deal notice, 2026-07-01] (illustrative)
- Event date: 2026-07-01 [Public: state licensing database]
- Source: State licensing database, ownership change
- Deal notice: Harborline's deal notice publishes the integration review date, 2027-02-16 [Public: deal notice, 2026-07-01] (illustrative)
- Trigger window: 60 to 120 days after the event date (profile Buying Triggers: consolidator buys the site)

The Account
- Account: Corrow Ridge Cemetery
- Footprint: One site, 14,000 plots [CRM] (illustrative), paper plat maps [CRM] (illustrative)
- Site budget: The general manager keeps the site budget until the integration review in Q1 2027 [CRM]
- Status: TARGET. No open deal and no owner [CRM]
- Acquirer's CFO or controller: [Unknown], not named in the CRM
- Harborline's ownership type: [Unknown], not stated in the licensing record or the deal notice
- Harborline's system for its sites: [Unknown]

## What You Should Get

- Trigger type: Acquisition / M&A (profile trigger: consolidator buys the site). Event tag: [Public: state licensing database].
- Urgency window: 2026-08-30 to 2026-10-29. Days remaining: 10. Share remaining: 10 of 60 window days (17%). Trigger status: STALE, so the sequence runs.
- Sequence: two personas, three emails each: the acquirer's CFO or controller, whose name is [Unknown], and the site GM. The example page shows the CFO's three. The GM's follow the same rules and are left off the page.
- Email 1 (2026-10-20): subject "Corrow Ridge after the Harborline close". Email 2 (2026-10-23 to 2026-10-24) and Email 3 (2026-10-27 to 2026-10-29) follow.
- Proof point: none. The profile's proof point for this trigger is Illustrative, so no figure goes into any email.
- Disqualifier check: Harborline's ownership type and its system are [Unknown]. The check is due by 2026-10-22. Email 1 asks nothing that depends on it and may go first. Email 2 waits for the check.
- Next action: Nadia Brandt finds the acquirer's CFO or controller by 2026-10-20 (Day 1, the earlier date the sequence timing sets for this step, since Email 1 cannot go before the name is found), then sends Email 1 after reading the draft.
