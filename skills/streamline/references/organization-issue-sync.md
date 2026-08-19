# Organization issue-sync example

A small team wanted every organization issue added to a shared GitHub Project,
with a Discord alert when synchronization failed. An initial 458-line plan
wrapped that convenience tool in several subsystems. The right-sized plan used
the requirements and recovery paths to reduce each area:

| Area | Initial machinery | Right-sized design |
| --- | --- | --- |
| Project insertion | A processing queue, dead-letter queue, D1 delivery ledger, and checkpoints | A verified webhook handler that calls the GitHub Project API directly |
| Missed events | Fifteen-minute probes, a health endpoint, and an external monitor | One bounded daily reconciliation for backfill and missed deliveries |
| Failure alerts | A separate alert queue, delivery auditing, and six-hour reminders | A direct Discord REST call through an existing bot, plus one KV key for alert deduplication |
| Rollout | Five phases and a large failure matrix | Focused tests and five acceptance criteria |

The rewrite reduced the plan to 137 lines. It removed D1, queues, dead-letter
handling, health endpoints, checkpoint machinery, external monitors, and
rollout ceremony. It retained webhook verification, secret handling,
restricted Discord mentions, bounded reconciliation, and acceptance criteria.

The removed machinery remains eligible when evidence supports it. A queue and
dead-letter queue become useful after measured downstream failures exceed the
daily reconciliation window. A durable ledger becomes useful when an audit or
replay requirement exceeds GitHub's retained history. Independent monitoring
becomes useful when an explicit availability target requires total-outage
detection.

The public design transition is recorded in
[standardagents/issues#3](https://github.com/standardagents/issues/issues/3#issuecomment-5344275186).
