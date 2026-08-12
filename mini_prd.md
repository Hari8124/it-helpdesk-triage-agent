# Mini-PRD: IT Helpdesk Triage Agent

## Problem

Employees submit IT tickets as free text to a shared queue. A Tier-1 specialist reads each one, decides its category, checks whether it matches a documented fix, and either replies with resolution steps or routes it to the right specialist. For a meaningful share of tickets, the correct first response is already sitting in the knowledge base — but the queue doesn't distinguish these routine tickets from genuinely complex ones until a human has already spent time reading and triaging them.

The triage step is the bottleneck: manual, inconsistent between specialists, and it delays first response for every ticket equally, whether the ticket needs judgment or a routine documented fix.

## Target user

**Primary:** IT helpdesk operations — accountable for queue health, first-response time, and specialist workload. This agent is a filter in front of their queue, not a replacement for it.

**Secondary:** the employee submitting the ticket, who gets a faster first response on routine issues and isn't misled into a canned fix on issues that actually need a person.

## Proposed v1 flow

1. Classify the incoming ticket into Hardware, Software, Access & Permissions, Network, or Other.
2. Generate a short search query from the ticket.
3. Retrieve up to two relevant articles from the 8-article knowledge base using category-scoped keyword matching.
4. Decide whether the retrieved article genuinely addresses the ticket and whether any escalation rule overrides a canned response.
5. Draft either troubleshooting steps or a human-escalation acknowledgment.

## Success metric

**Primary:** percentage of tickets where the agent's routing decision — canned response vs. escalate — matches the correct action on the evaluation set.

**Guardrail — not traded away for a better headline number:** 0% of safety, security, or privileged-access tickets incorrectly resolved with a canned response. These must always escalate; a single miss is categorically worse than several unnecessary escalations elsewhere.

**Secondary:** category classification accuracy — tracked to identify systematic confusion, but treated as diagnostic rather than the primary product target.

## Non-goals (v1 scope)

- No multi-turn conversation with the employee — single-shot first response only
- No auto-closing tickets or writing back to a real ticketing system
- No handling of non-English tickets
- No production ticketing-system integration
- No production-scale retrieval infrastructure — the KB contains only eight synthetic articles
- No fine-tuning — first test whether a prompted multi-stage workflow is sufficient before reaching for anything heavier

## Evaluation

The project uses a 24-ticket synthetic evaluation set spanning clean matches, policy-override escalation cases, genuinely ambiguous cases, security triggers, `Other`, and no-KB-match cases.

The intended evaluation method is open-ended error analysis first, followed by a rubric derived from observed failures, one targeted fix, and a re-run on the same set to produce a real before/after comparison.
