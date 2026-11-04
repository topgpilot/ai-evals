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

### _Risk name 1_
- **Method:** _how you evaluate it_
- **Ground truth:** _what you grade against_

### _Risk name 2_
- **Method:** _how you evaluate it_
- **Ground truth:** _what you grade against_

## Strategic acceptance

**Accepted gap:** Fairness ❌

> **Why we can accept it for now:** We accept this gap because the solution is targeted at the European market only, where most of our paying customers are, and the summaries are written in English only. A fix would therefore cost more than the risk.
>
> **What would change our mind, and when we'll look again:** We'll look again when non-English-speaking clients pass 25% of our clients, or when clients ask for summaries in other languages.

## Critical mitigation

- **Critical gap:** _the ❌ you cannot accept_
- **Why critical:** _…_
- **Mitigation plan:** _concrete plan with a date/owner — not "we'll add it later"._
