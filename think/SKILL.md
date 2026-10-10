---
name: think
description: "Assess feasibility, choose an architecture, and produce an executable handoff grounded in project evidence. Excludes routine edits and debugging."
disable-model-invocation: true
---

# Think

Strengthen engineering decisions through evidence, feasibility checks, minimal design, and executable handoffs. Scale depth to uncertainty and impact. A feasibility question can end with a supported judgment; an implementation plan must settle the decisions needed to build it.

## Establish the evidence

Read relevant project guidance (`AGENTS.md`, `CLAUDE.md`, `CONTEXT.md`) and prior decisions such as `docs/adr`. Inspect the affected code and actual configuration. Check whether an existing feature already meets the need and whether a criticized behavior is intentional; reassess that choice against current goals.

When a request presupposes a solution, use first principles to recover the underlying goal and constraints, then check whether that solution is necessary.

Use relevant memory to recover preferences and prior reasoning, then verify factual claims against current evidence. Memory does not grant authorization. Surface conflicts between requirements, project rules, and observed behavior; ask only for consequential choices that evidence cannot resolve.

Check current official capabilities and supported patterns before proposing custom machinery. When unfamiliar mechanisms or repeated failures create uncertainty, study a relevant mature implementation and identify what transfers to this project.

## Assess feasibility

Separate the judgments that matter to the request:

| Dimension | Establish |
|---|---|
| Technical | Required capabilities exist; interfaces, permissions, compatibility, and performance constraints permit the approach. |
| Delivery | The current codebase, skills, time, and resources can support implementation, integration, migration, testing, and maintenance. |
| Value | The expected benefit warrants the cost compared with existing behavior or a smaller change. |
| Commercial, when relevant | Demand, distribution, willingness to pay, delivery/support costs, and readiness to charge support the business goal. |

Distinguish verified facts, assumptions, and unresolved questions. State the most fragile assumption, the evidence behind it, and what changes if it fails. Use adversarial review to seek a counterexample that could invalidate it; report evidence or a verification method, rather than treating a hypothetical risk as a finding. Technical possibility alone does not establish deliverability or value.

For a decisive unknown, use the smallest check permitted by the task. If it requires a prototype, unavailable access, or additional authorization, specify the experiment and pass/fail criterion; keep the recommendation conditional until resolved. A validation proposal is a valid outcome, but must be labeled separately from a ready-to-build plan.

For multiple requests, apply these judgments per item, then account for dependencies, impact, effort, and uncertainty when recommending priority.

## Recommend the smallest workable approach

Recommend one direction with rationale, effort, risk, and existing code it builds on. Apply Occam's razor: among approaches meeting the acceptance criteria, prefer fewer assumptions and lower operational and maintenance complexity; justify additions by a concrete benefit. Mention an alternative only when its tradeoff could change the decision. State what evidence would change the recommendation.

- Prefer existing defaults, interfaces, and dependencies. Explain the need and ongoing cost of new services, runtimes, configuration, or user setup.
- Tie retries, fallbacks, and defensive layers to named failure modes. Reconsider the approach when workaround machinery outweighs the feature.
- Where relevant, examine dependency outages, expected growth, data consistency, and migration or rollback failure. Resolve weaknesses or disclose their consequences.
- Use a diagram when ownership or data flow needs clarification. Investigate cycles and unclear boundaries.

## Make the handoff executable

For an implementation plan, include the applicable details:

- Goal, acceptance criteria, constraints, scope, and exclusions.
- Chosen approach, key tradeoffs, and file or module targets.
- Public API, schema, command, configuration, and dependency changes.
- Implementation order; each phase leaves a usable, independently mergeable result.
- Verification commands and observable checks for normal, error, and boundary behavior; reference source artifacts for visual acceptance.
- Required tools, access, accounts, and release or migration steps, including failure handling and rollback.

Verify prerequisites with read-only checks where possible and mark unverified access explicitly. Resolve blocking design questions before declaring the plan executable. Defer nonblocking details only with a reason and owner; keep implementation steps concrete enough for another engineer to execute without choosing the architecture again.

End at the deliverable requested. Planning does not authorize implementation; honor implementation authorization already given without adding another approval round.
