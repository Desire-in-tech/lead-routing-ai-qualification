# AI-Powered Lead Routing & Qualification

An AI-assisted lead intake and routing workflow built for the Datheon AI Automation & Agent Building Internship.

The automation receives lead submissions through a Make.com webhook, asks Groq to classify the lead, stores the result in Airtable, and sends a Slack notification to the appropriate review channel.

## Workflow

`Webhook → Groq qualification → JSON parsing → Airtable lead record → status router → Slack notification + automation log`

### Routing outcomes

| Classification | Destination |
|---|---|
| Qualified | Slack `#qualified-leads` |
| Uncertain | Slack `#lead-review` |
| Unqualified | Slack `#unqualified-leads` |

The AI is instructed not to invent missing company or budget details. Missing or ambiguous information should lead to an **Uncertain** classification and human review.

## Technology

- **Make.com** — workflow orchestration and webhook intake
- **Groq API** — LLM-based lead qualification (model configured in the scenario: `openai/gpt-oss-120b`)
- **Airtable** — lead records and automation logs
- **Slack** — outcome-specific notifications
- **PowerShell** — synthetic webhook test submissions

## Example webhook payload

See [`examples/lead-payload.json`](examples/lead-payload.json). Use your private Make webhook URL locally; never commit it to this repository.

## Verified test evidence

The latest documented successful end-to-end execution:

- Execution ID: `fd84a13074184053a1d0b1d00b9a1ca7`
- Result: **OK**
- Duration: **3,025 ms**
- Credits consumed: **6**
- Failures / warnings: **0 / 0**
- Verified route: **Uncertain → Slack `#lead-review`**
- Verified persistence: Airtable lead record and an automation log with status `Needs Review`

This verifies one complete run, not consistent latency across all traffic or every routing branch. See [test evidence](docs/test-evidence.md).

## Current limitations

This is an internship MVP, not a production-hardened lead management service.

- Qualified and Unqualified Slack routes are configured but were not verified by the final recorded test.
- Duplicate prevention is not implemented; repeated webhook submissions can create duplicate Airtable records.
- Processing time is not currently populated in the Automation Logs table.
- Failed-execution logging is incomplete. The current log evidence covers the successful uncertain/review path.
- Input validation is partial (required lead name, company, and basic email checks); company size, budget, and lead source are not fully validated.
- Groq retry handling and Make incomplete executions are configured, but dedicated Airtable/Slack error logging is incomplete.
- The Make scenario was **not activated** at the time of the final audit. The verified execution was a manual/test execution.

These limitations are documented deliberately so the project does not overstate its readiness.

## Documentation

- [Architecture and data flow](docs/architecture.md)
- [Test evidence and acceptance status](docs/test-evidence.md)
- [Known limitations and next improvements](docs/limitations.md)

## Security

Do not commit API keys, Make webhook URLs, OAuth tokens, Slack credentials, Airtable personal access tokens, or real customer personal data. Use synthetic test records and configure credentials in the relevant platform's secure connection settings.

## Setup overview

The workflow is configured in Make.com. To reproduce it:

1. Create the Airtable base and tables described in [architecture](docs/architecture.md).
2. Configure Groq, Airtable, and Slack connections inside Make.
3. Import or recreate the workflow using the module sequence documented above.
4. Register a Make Custom Webhook and keep its URL private.
5. Submit the example payload to the webhook and inspect the Make execution, Airtable records, and Slack destination.

The scenario blueprint is not included in this repository yet. Add a sanitized export if/when one is available; remove webhook URLs and connection identifiers first.
