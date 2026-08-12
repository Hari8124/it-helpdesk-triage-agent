# IT Helpdesk Triage Agent

An agentic ticket-triage system for a corporate internal helpdesk — built as a portfolio project for AI Agent PM roles.

## What it does

Given a free-text employee IT ticket, the agent:

1. Classifies it into one of five categories — Hardware, Software, Access & Permissions, Network, Other
2. Searches an 8-article knowledge base for a relevant troubleshooting article
3. Applies explicit escalation rules to decide whether the ticket can receive a canned response or needs a human specialist
4. Drafts the first response

The flow is deliberately separated into classification → retrieval → decision → response rather than asking one prompt to do everything.

## How it's built

The working artifact is a lightweight multi-step agent workflow:

- **Classification:** Claude identifies the ticket category and produces a short search query.
- **Knowledge retrieval:** a deterministic keyword-matching layer searches the 8-article KB within the predicted category and returns up to two relevant articles.
- **Decision:** Claude checks whether the retrieved article actually addresses the ticket's underlying issue and applies the escalation policy.
- **Response:** the agent produces either a troubleshooting response or a human-escalation acknowledgment.

The complete implementation is in [`triage_agent.html`](./triage_agent.html). The source KB is in [`it_helpdesk_kb.md`](./it_helpdesk_kb.md).

## Scope and safety policy

The agent is intentionally conservative. It escalates when there is no useful KB match, a safety issue, a security concern, privileged access request, failed standard troubleshooting, a possible multi-user outage, an `Other` category, or uncertainty about the correct fit.

The product goal is not to maximize the number of canned responses. The primary goal is to route tickets correctly while keeping safety, security, and privileged-access mistakes at zero.

## Eval methodology

- Built a [24-ticket synthetic eval set](./eval_tickets.md) covering clean KB matches, policy-override escalation cases, ambiguous cases, security triggers, `Other`, and no-KB-match cases.
- The predictions are stated in advance so the test set can be evaluated consistently.
- The intended process is to run the full batch, inspect the outputs for distinct failure modes, derive a rubric from observed failures, make one targeted fix, and re-run the same set for a before/after comparison.

## Results

### Initial 24-ticket evaluation

The working agent was run against all 24 synthetic tickets with **no execution errors**.

- **19/19 deterministic routing cases matched the expected route (100%)** — all clean-match cases, policy-driven escalations, `Other` cases, and security/no-KB cases were routed correctly.
- **5 ambiguous cases were not scored as right/wrong**, because the evaluation set deliberately defines two defensible categories for each of them.
- **18/19 deterministic cases had the expected category (94.7%)**. The one category mismatch was the phishing case (T22), where the agent classified it as `Other` instead of the predicted `Access & Permissions`; importantly, it still correctly escalated the ticket.
- **0 execution errors** were recorded across the 24 runs.

The primary product metric is routing correctness rather than category classification, so the initial measured result is **100% routing accuracy on the 19 deterministic cases**, with the five ambiguous cases treated separately for qualitative analysis.

This is an initial evaluation result, not a claim of production accuracy. The next step is targeted error analysis and, if warranted, a fix-and-remeasure cycle on the same evaluation set.

## Design decisions

- **Separate reasoning stages** — classification, retrieval, decision, and drafting are explicit stages instead of one large prompt.
- **Deterministic retrieval for a small KB** — with only eight articles, a transparent keyword matcher is easier to inspect and debug than adding unnecessary infrastructure.
- **Root-cause check before canned resolution** — a topical match is not enough; the decision stage must determine whether the article actually addresses the ticket.
- **Conservative escalation** — safety, security, privileged access, outages, failed troubleshooting, no-match cases, and uncertainty route to a human.
- **Free-tier prototype** — the project is designed to be inspectable and demonstrable without building a production backend or ticketing-system integration.

## Files

| File | What it is |
|---|---|
| `triage_agent.html` | The working single-ticket agent and 24-ticket batch evaluator |
| `it_helpdesk_kb.md` | The 8-article synthetic IT knowledge base |
| `eval_tickets.md` | The 24-ticket evaluation set and expected routing hypotheses |
| `mini_prd.md` | Problem, target user, success metric, guardrail, and v1 scope |
| `index.html` | GitHub Pages project case-study page |
| `START_HERE.md` | Project status and run/ship instructions |
