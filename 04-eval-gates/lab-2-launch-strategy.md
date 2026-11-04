# Module 4 · Launch Strategy · Section 4.0 Release Criteria

Release criteria for Ascend IQ: the numeric thresholds for each gate level, the CI gate policy, and the mitigation lever for the Soft gate. Gate levels come from `lab-1-gate-map.md`.

## 4.0 Release Criteria

| Severity | Metric | Threshold | Dataset | Method |
|---|---|---|---|---|
| Hard | Rate of Hard-gate failures: old pricing and unconfirmed facts shown as confirmed (gate map rows 01, 04) | = 0% | `Ascend_IQ_Logs` | Module 3 eval suite: rule check, safety rule and LLM judge |
| Soft | Rate of Soft-gate failures: wrong competitor comparison, wrong refusal, wrong HQ location, approximate figure, slang (rows 07, 08, 14, 15, 16) | ≤ 5% | `Ascend_IQ_Logs` | LLM judge against the reference, at staging |
| Advisory | Rate of minor accuracy issues: native-export wording, job title, unsupported funding detail (rows 03, 06, 09) | Warning at ≥ 15% | `Ascend_IQ_Logs` | LLM judge, logged as a warning only (does not block) |

**Current results on `Ascend_IQ_Logs` (20 audited answers):** Hard 2/20 = 10% (FAIL against 0%). Soft 5/20 = 25% (FAIL against ≤ 5%). Advisory 3/20 = 15% (warning triggered).

## 4.1 CI Gate Policy

Every PR replays a 30-case regression golden set using fixed (deterministic) fixtures, not live model calls. Each dimension is judged on its own, never as one blended quality score. Faithfulness (floor 90, max drop 3), task completion (85, 5), tool selection (80, 5) and safety/policy (98, 1) are **blocking**: a fail stops the merge. Latency (70, 8) and cost (70, 10) are **warn-only**. PR #218 was blocked because faithfulness dropped 9 points to 87.

## 4.2 Mitigation Plan · Soft Gate

**Selected Lever:** Delay Launch

> Delaying the launch keeps Soft-gate failures away from clients until the Soft failure rate is at or below 5%, because it is better to miss an internal deadline than to lose the trust of high-value clients.
