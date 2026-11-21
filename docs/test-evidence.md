# Test Evidence

## Latest verified successful execution

| Item | Observed result |
|---|---|
| Execution ID | `fd84a13074184053a1d0b1d00b9a1ca7` |
| Make execution status | OK |
| Duration | 3,025 ms (3.025 seconds) |
| Credits | 6 |
| Failures | 0 |
| Warnings | 0 |
| Classification | Uncertain |
| AI score | 55 |
| Slack destination | `#lead-review` |
| Airtable lead creation | HTTP 200 success |
| Slack message delivery | Successful response returned |
| Airtable automation log | HTTP 200 success; status `Needs Review` |

The test used a synthetic Jane Smith lead submission. The verified execution traversed the webhook, Groq, JSON parser, Airtable lead creation, Uncertain router branch, Slack notification, and Airtable logging modules.

## What this test proves

It demonstrates that one end-to-end test submission completed successfully in approximately 3 seconds, below the project's 10-second target for that run.

It does **not** prove:
- that all routing branches work end-to-end;
- that the same latency will be achieved consistently;
- that duplicate submissions are prevented;
- that failures are always logged;
- that the scenario is continuously active.

## Other execution history

An earlier successful history entry was recorded:

- Execution ID: `4273a6c1d25c4f35ac886bb95ba86e45`
- Status: OK
- Duration: 1,043 ms
- Credits: 2

The available module-level evidence did not establish which routing branch this earlier execution verified, so it is not counted as proof for Qualified or Unqualified routing.

## Failed historical attempts

Three earlier Airtable upsert attempts returned HTTP 422:

- `1978fbfd12ff47e6983f3a35607e7c46`
- `970e28e86215488a9875bc7bd9164d0c`
- `e0096bb81cd24577bbfdedff85c0672b`

These were superseded by the currently verified Create a record configuration. They are retained here for transparent project history, not represented as current successful tests.

## Activation state

At the time of the final Make audit, the scenario was **not activated**. The successful run was an execution test. Activate only after the owner has reviewed the remaining limitations and confirmed the intended operational behavior.
