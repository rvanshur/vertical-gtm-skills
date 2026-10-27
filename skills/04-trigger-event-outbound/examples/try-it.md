# Try It: Trigger Event Outbound On Corrow Ridge Cemetery (Invented Example)

Every name, date and number in this file is invented for the PlotIQ example. Nothing here is a real company.

## Ask Your Assistant
"Run Trigger Event Outbound on Corrow Ridge Cemetery using skills/04-trigger-event-outbound/examples/try-it.md and the PlotIQ profile at profiles/examples/plotiq-example.md. Treat today as 2026-10-19."

## The Records

Run date: 2026-10-19 (illustrative)
User role: BDR (Nadia Brandt)

The Event
- Event: Harborline Funeral Partners acquired Corrow Ridge Cemetery. Harborline is a 14-site regional consolidator, per its deal notice [Public: deal notice, 2026-07-01] (illustrative)
- Event date: 2026-07-01, from the state licensing database
- Source: State licensing database, ownership change
- Deal notice: Harborline's deal notice publishes the integration review date, 2027-02-16 [Public: deal notice, 2026-07-01] (illustrative)

The Account
- Account: Corrow Ridge Cemetery
- Footprint: One site, 14,000 plots [CRM] (illustrative), paper plat maps [CRM] (illustrative)
- Site budget: The general manager keeps the site budget until the integration review in Q1 2027 [CRM]
- Status: TARGET. No open deal and no owner [CRM]
- Acquirer's CFO or controller: [Unknown], not named in the CRM
- Harborline's ownership type: [Unknown], not stated in the licensing record or the deal notice
- Harborline's system for its sites: [Unknown]

## What You Should Get

- Trigger type: Acquisition / M&A (profile trigger: consolidator buys the site, profile: Qualification Criteria). Event tag: [Public: state licensing database].
- Urgency window: 2026-08-30 to 2026-10-29. Days remaining: 10. Share remaining: 10 of 60 window days (17%). Trigger status: STALE, so the sequence runs.
- Sequence: two personas, three emails each, six emails in total: the acquirer's CFO or controller, whose name is [Unknown], and the site GM, whose name is [Unknown].
- Email 1 on 2026-10-20 (Day 1), subject "Corrow Ridge after the Harborline close". Email 2 on 2026-10-23 (Day 4). Email 3 on 2026-10-27 (Day 8).
- Proof point: none. The proof point for this trigger (profile: Trigger Catalog) is Illustrative, so no figure goes into any email.
- Disqualifier check: Harborline's ownership type and its system are [Unknown]. Email 1 and Email 2 neither state nor ask about either one, so both go out on their days without waiting. No email asks about the system, so the check is due 2026-10-26, the business day before the last send day, 2026-10-27.
- Deadline in Email 1: the integration review date, 2027-02-16, from the deal notice, because the trigger is STALE. The body of Email 1 names it.
- Next action: Nadia Brandt finds the acquirer's CFO or controller and the site GM by 2026-10-20, the send day of Email 1.
- Later steps: send Email 1 on 2026-10-20 (Day 1) after reading the draft. Run the Harborline ownership and system check by 2026-10-26, before Email 3 on 2026-10-27.
