# Known Limitations and Improvement Backlog

The final Make AI acceptance audit rated the workflow **READY WITH ACCEPTED LIMITATIONS** for an internship MVP. The items below remain open.

## Known limitations

1. **Unverified routing branches** — Qualified and Unqualified Slack routes are configured but not proven by the final recorded end-to-end test.
2. **No deduplication** — Airtable Create a record can create duplicate leads if the same submission is sent more than once.
3. **Incomplete validation** — current checks require lead name, company, and a basic email shape. Company size, budget, and lead source are not comprehensively validated.
4. **Incomplete failure logging** — dedicated error handlers do not consistently write failed events to Airtable for Airtable or Slack errors.
5. **No processing duration value** — Processing Time (ms) is mapped as null in the audited log modules.
6. **Partial retry coverage** — Groq retry handling is configured (three retries at 15-minute intervals) and Make incomplete executions are enabled, but equivalent dedicated handling is not established for all downstream modules.
7. **Scenario not active** — final audit recorded the Make scenario as not activated.

## Recommended next improvements

Prioritize in this order:

- Test Qualified and Unqualified outcomes with synthetic payloads and retain execution evidence.
- Add deterministic deduplication using a stable event ID or normalized email plus an appropriate time/business rule; use an Airtable-supported lookup/create-or-update pattern and verify it under repeat submissions.
- Add explicit validation for required fields and acceptable data formats; log rejected submissions without exposing sensitive data.
- Add error handlers for Airtable and Slack, recording failure status and a safe diagnostic message.
- Measure elapsed time with a supported Make mechanism and populate Processing Time (ms).
- Review retry intervals and ensure retries cannot create duplicate side effects.
- Activate the scenario only after the owner has confirmed all routes, alert destinations, and failure behavior.

## Data integrity and responsible AI

- Keep source-submitted facts distinct from AI-generated interpretations.
- Never fill missing budget or company details with guesses.
- Route insufficient evidence to human review.
- Do not treat an AI confidence/priority score as proof of a lead's ability or intent to buy.
- Avoid putting unnecessary personal information in Slack messages or logs.
