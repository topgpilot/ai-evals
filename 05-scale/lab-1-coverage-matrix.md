# Lab 1, Ascend Analytics Coverage Matrix

**Product:** AI Report Summaries. External, used by clients. Writes executive summaries of research reports, which are sent straight to clients.

**What runs today:** an LLM judge compares each summary with its source report before every release. Response time is logged, but no target has been set.

## Coverage row

| Product | Hallucination Rate | Fairness | Latency | UX Trust | Robustness |
|---|---|---|---|---|---|
| AI Report Summaries | ✅ | ❌ | ⚠️ | ❌ | ❌ |

- **Hallucination Rate ✅:** an LLM judge compares each summary with its source report before every release.
- **Fairness ❌:** nothing tests whether summaries are equally good across different clients, regions or languages.
- **Latency ⚠️:** response time is logged, but there is no target, so no one can tell a pass from a fail.
- **UX Trust ❌:** the judge checks facts against the source, not tone, so nothing checks how the summaries sound to clients.
- **Robustness ❌:** nothing tests summaries of messy, incomplete or unusual reports.

## Method + Ground Truth (two ✅/⚠️ cells)

### Hallucination Rate ✅
- **Method:** before every release, an LLM judge reads each summary next to its source report and checks every figure, name and claim. It returns 1 (pass) if all of them are in the source, or 0 (fail) with one line of reasoning naming the unsupported claim. Hallucination Rate = failed summaries ÷ summaries judged.
- **Ground truth:** the source research report that the summary was written from. A claim that is not in the report counts as a hallucination, even if it might be true elsewhere.

### Latency ⚠️
- **Method:** the time from request to finished summary is already logged for every summary. Each release, we calculate the P95 (and P99) from those logs and compare it with a target.
- **Ground truth:** the logged response times. The missing piece is the pass/fail bar: no target has been set, which is why this cell is ⚠️ and not ✅. The QA team will set one, starting from the P95 ≤ 5 seconds promise in our Module 1 strategy canvas.

## Strategic acceptance

**Accepted gap:** Fairness ❌

> **Why we can accept it for now:** We accept this gap because the solution is targeted at the European market only, where most of our paying customers are, and the summaries are written in English only. A fix would therefore cost more than the risk.
>
> **What would change our mind, and when we'll look again:** We'll look again when non-English-speaking clients pass 25% of our clients, or when clients ask for summaries in other languages.

## Critical mitigation

- **Critical gap:** Robustness ❌
- **Why critical:** If it failed on messy or incomplete reports, a broken summary sent to a paying client would damage client trust and put the contract renewal at risk. Once the weekly audit is in place, the internal QA team would notice first.
- **Mitigation plan:** Add a new eval gate (a test set of messy and incomplete reports that every release must pass) and an LLM judge that scores a weekly sample of live summaries. Owner: QA team, by 30 November 2026.
