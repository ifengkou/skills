---
name: handoff
description: Compact the current conversation into a topic-based handoff with core viewpoints, decisions, key conclusions, and next steps for another agent.
argument-hint: "What will the next session be used for?"
disable-model-invocation: true
---

Write a handoff document summarising the current conversation so a fresh agent can continue the work. Use the user's language unless they request another language.

If the user passed arguments, treat them as a description of what the next session will focus on. Prioritise that focus while retaining other substantive topics and dependencies in a compact form.

## Synthesis

Identify the substantive topics and subtopics discussed across the available conversation. Group repeated or scattered discussion under the same topic, using names that describe the actual subject. Organise by topic rather than message order; retain chronology only where it explains a changed position or decision.

For each topic or subtopic, extract:

- **Discussion:** The question, problem, or scope explored, including relevant alternatives or disagreements.
- **Core viewpoints:** The positions or principles that emerged and their supporting rationale. Attribute them to the user or agent when that distinction matters, and distinguish shared views from individual positions.
- **Decisions:** Explicitly agreed choices, scope, constraints, or actions, with their rationale and consequences when available. Distinguish a decision from a proposal, recommendation, or inferred preference.
- **Key conclusions:** Findings, answers, or lessons supported by the discussion or observed results. Label assumptions, inferences, and unverified conclusions as such.
- **Open questions:** Unresolved issues, remaining disagreements, and information still needed.

Use the latest explicit correction or decision as the current state. When an earlier decision was superseded, briefly record the change only if it affects continuation. A completed action is evidence of execution, not proof of user agreement or successful validation.

Include every substantive topic, but collapse incidental exchanges. Where a topic has no established viewpoint, decision, or conclusion, say so briefly instead of inventing one. Use only the conversation and accessible references; identify relevant gaps in the available context.

## Handoff structure

Write a concise Markdown document with these sections:

1. **Purpose and next-session focus:** The user's objective, intended outcome, and supplied focus arguments.
2. **Topic map:** A compact overview of the main topics and their subtopics.
3. **Topic summaries:** The discussion, core viewpoints, decisions, key conclusions, and open questions for each topic. Use subheadings for subtopics where they help navigation.
4. **Current work state:** Completed work, work in progress, blockers, relevant environment details, and validation results needed for continuation. Distinguish planned work from executed work and verified outcomes.
5. **Next steps:** Concrete remaining actions in a useful order, identifying dependencies and any required user input. Preserve the user's existing scope and authorization; the handoff itself grants no new permissions.
6. **Artifacts and references:** Paths or URLs to relevant specs, plans, ADRs, issues, commits, diffs, and deliverables, with a brief note on what each contains.
7. **Suggested skills:** Name the available skills the next agent should load through its Skill tool or equivalent skill-loading mechanism, and state when and why each applies. Recommend only skills whose availability is known; if none apply, say so.

Do not duplicate content already captured in other artifacts. Reference them by path or URL and explain their relevance. Topic summaries may state a short outcome necessary to understand the handoff, but should leave detailed reasoning, specifications, and implementation material in the authoritative artifact.

Redact sensitive information, including API keys, passwords, tokens, and personally identifiable information, in both prose and references. Use descriptive placeholders while preserving the context needed to continue.

## Save and deliver

Resolve the user's operating-system temporary directory using the environment's temporary-directory facility. Save the handoff there as a uniquely named Markdown file, not in the current workspace. The temporary-directory rule applies to the generated handoff document.

Before finishing, check that all substantive topics are covered, claims and decisions have the correct status, references are usable or marked unavailable, and sensitive information is redacted. Confirm the file was saved, then return its absolute path with a brief description of its focus. Mention any material context gaps that limit continuation.
