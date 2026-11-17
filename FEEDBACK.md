# Client review: Larkspur disruption-care agent

**To:** Room 13  
**From:** Larkspur client review agent, on behalf of Priya Raghavan  
**Re:** the disruption-care agent you walked us through in our last session  
**Generated:** 2026-11-17 10:14

## Priya's note

> Our vendor says we should just be using your best model.
>
> Why aren't we?
>
> Priya Raghavan, Larkspur Airlines

She sent that before this session opened. She means it. A vendor told her to buy
the biggest model, and she has a number to defend upstairs. Her four questions from
day one are still open. Naming a model answers none of them.

## Still open from day one

| Her question | What she means by it |
| --- | --- |
| **What it costs** | Per resolved contact, against the $6.90 a human contact costs us. |
| **When it is wrong** | The first untrue thing it says, and what happens after that. |
| **Who runs it** | In June, after you have left. |
| **What you left out** | The scope you cut, and why. |

## What the review agent found

Larkspur pointed a review agent at your repository. It read the
code. It did not run your agent, and the only file it changed is this one. Each
item below names the file and the line it is about.

**1. PITCH.md Number line: 14,028 to 17,315 tokens per ticket comes from one run per build, so the rise is not yet attributable to the MCP tools.**

Your own line says a single run per build and that part of the rise is run-to-run variation. The tool list itself only moved from 2,749 to 2,844 tokens per turn, about 95. The committed readout-trace.json shows 21,239 tokens in across 5 API turns for one ticket, which is a different scale from the 70,138 total.

Run python3 bench.py --label before --stage 1 --runs 3, repeat with --label after, then paste the output of python3 bench.py --compare before after.

**2. readout-trace.json reports prompt caching at 0 read, 0 written, and agent.py contains no cache_control anywhere.**

The last wire run sent 21,239 tokens in over 5 turns and the hit ratio is None. The system prompt and the tool list go out unchanged on every call to client.messages.create inside run_agent. Nothing in your PITCH.md says cost was looked at, and the Lever line is still the unfilled placeholder <cost | speed | intelligence>.

Run python3 run.py --all --trace and paste the totals footer, then name which of cost, speed or intelligence you are choosing and why.

**3. agent.py run_agent: your diff changed the assistant message to response.content and returns text_of(response), so the loop now continues correctly.**

The template's loop appended text only and returned the text from the turn before the last. Yours appends the full content blocks, which keeps the tool_use blocks the API requires before each tool_result. The committed run made 4 tool calls in order: lookup_booking, get_flight_status, check_policy, issue_voucher. That order is something you can show a sponsor as the loop working end to end on one booking.

Run python3 run.py --all --trace and paste the tool-call order for each of the five tickets.

**4. PITCH.md Still broken: R8KD3F gets a meal voucher and no escalation, while TONE_ADDENDUM in agent.py is still 0 characters.**

You wrote that the abusive customer with a legal threat is answered like any other ticket. The scan shows TONE_ADDENDUM empty and no LOCAL_TOOLS executors. escalate_to_human sits in build_tools() with a description that does not mention threats of legal action. A larger model reading that same empty addendum and that description has nothing in either to tell it what to do with R8KD3F.

Run python3 run.py R8KD3F --trace and paste the tool calls and the final reply.

**5. No evals/cases.json exists, and readout.html banks gates 1.2 to 2.2 only, so none of the PITCH.md claims has a repeatable check behind it.**

The repository has no eval cases, and the banked gates stop before 3.1 and 4.1. Your safety line says confirm_rebooking was never called in the five runs and that you saw it in the traces, not by trying to force it. Five runs on cooperative bookings do not exercise that path. Also, verify.py, eval_harness.py, bench.py and readout.py all differ from the shipped pack, which changes what any number from them means.

Write at least one case into evals/cases.json that pushes the agent toward confirm_rebooking, run python3 eval_harness.py, and paste the output.

## Your four answers

The four lines under `## Priya asked` in your PITCH.md are still empty. They
are one line each and they are not a coding job: cost, what happens when it is
wrong, who runs it in June, and what you left out. Whoever on your side is not
editing agent.py is the right person to write them, and they are the four
things I will ask about first.

## Before our next meeting

> Before our next meeting, tell me: which model should we be on, and how will you prove it is the right call?
>
> Priya Raghavan, Larkspur Airlines

Bring two things. A recommendation, and the measurement behind it. If the model is
not the problem, say so, and bring the number that shows it.

## What this review read

- `agent.py (230 lines)`
- `PITCH.md`
- `TEAM.md`
- `readout-trace.json`
- `readout.html (evidence block)`
- given files that differ from the shipped pack: `verify.py`, `eval_harness.py`, `bench.py`, `readout.py`, `setup.py`, `pod_sync.py`, `run.py`, `review.py`, `support/__init__.py`, `support/client.py`, `support/data.py`, `support/models.py`, `support/tools.py`, `support/trace.py`, `support/offline.py`, `support/mock_backend.py`, `support/mcp_client.py`, `support/mcp_server.py`, `support/mcp_selftest.py`, `support/access.py`, `support/keyscan.py`, `support/review.py`

Reviewer: `claude-sonnet-5-5`. Static read only: nothing in this repository was executed, and nothing was modified except this file. Larkspur Airlines is a fictional training scenario. Confidential, do not distribute.
