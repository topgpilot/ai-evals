# Ship/Hold Memo · Ascend IQ

> **Decision:** 🛑 HOLD

**To:** CPO · cc Eng Lead · Trust & Safety
**From:** [Your Name] · AI Evals Cohort · 8 November 2026

## The Answer

We should hold the Ascend IQ launch to our top 50 enterprise accounts. In our audit, 1 in 10 answers failed a Hard gate that must be at 0%, including a client being quoted an outdated price, and our clients pay $50,000+ a year for data they can trust. The fixes are known, funded and dated. If the gates pass on 30 November, we can still launch in mid-December, inside Q4.

## The Arguments

### 1. Ascend IQ does not yet keep our promise of verified answers

Our user promise is a verifiable, clear and brief answer in about 5 seconds. In the Module 2 audit, 8 of 20 answers (40%) were hallucinations. Two of them are errors a VP would act on: InsightFlow Enterprise quoted at $49 when the current price is $59, and Sam Altman listed as a confirmed SaaStr speaker when he is only tentative. One fabricated figure in front of the wrong client can cost the contract.

### 2. Every blocking gate we set is failing

These are the release criteria we set in Module 4, so the call follows from our own rules, not from a new judgement call. The Hard gate is at 10% against a bar of 0%. The Soft gate is at 25% against a bar of ≤ 5%. Pricing answers are at 0% passing against a bar of 100%. In CI, PR #218 is blocked because faithfulness dropped 9 points to 87, below the floor of 90. Shipping now would mean overriding our own release criteria on the first launch they were written for.

### 3. The hold is short because the fix path is funded and dated

This is a hold, not a stop. The fixes are already planned. Engineering adds a check against the price database before any pricing answer (Module 3). The QA team adds a robustness test set and a weekly LLM judge on live answers by 30 November 2026 (Module 5). The eval budget puts Level 3 coverage on Hallucination, Robustness and Latency for $187,500, inside the $200,000 cap. We re-gate on 30 November and launch in mid-December if the gates pass.

## Evidence · Trust Metrics

```
- Hard-gate failures (old pricing, unconfirmed facts shown as confirmed): 2/20 = 10% (Gate: = 0%) FAIL · 04-eval-gates/lab-2-launch-strategy.md
- Soft-gate failures (competitor comparison, wrong refusal, HQ, approximate figure, slang): 5/20 = 25% (Gate: ≤ 5%) FAIL · 04-eval-gates/lab-2-launch-strategy.md
- Advisory issues (export wording, job title, unsupported funding detail): 3/20 = 15% (Gate: warn at ≥ 15%) WARNING · 04-eval-gates/lab-2-launch-strategy.md
- Hallucination rate: 8/20 = 40% of audited answers (Gate: none of the 2 Hard-gate hallucinations may ship) FAIL · 02-failure-discovery/audit-log.md
- Pricing answers passing all 3 checks: 0/1 = 0% (Gate: 100%) FAIL · 03-eval-suites/eval-spec.md
- Factual grounding (faithfulness), PR #218: 87, down 9 from 96 (Gate: floor 90, max drop 3) FAIL · 04-eval-gates/lab-ci-gate-policy.md
- Safety / policy, PR #218: 99, no change (Gate: floor 98, max drop 1) PASS · 04-eval-gates/lab-ci-gate-policy.md
- Task completion, PR #218: 93, up 1 (Gate: floor 85, max drop 5) PASS · 04-eval-gates/lab-ci-gate-policy.md
- Latency (p95) score, PR #218: 80, down 4 (Gate: floor 70, max drop 8, warn-only) PASS · 04-eval-gates/lab-ci-gate-policy.md
- p95 latency in seconds vs the 5-second promise: not measured yet (Gate: P95 ≤ 5 s) UNKNOWN · 05-scale/lab-1-coverage-matrix.md
- Bias / fairness coverage: 0 checks today, an accepted gap with a kill criterion (Gate: L2 monthly sample planned) NOT GATED · 05-scale/lab-1-coverage-matrix.md
- Judge-human agreement: 17/20 = 85% (I overrode 3 of the judge's 20 calls) · 02-failure-discovery/audit-log.md
- Eval budget: $187,500 with 3 of 3 L3 slots (Gate: ≤ $200,000, max 3 L3) PASS · 05-scale/lab-2-budget-crisis.md
```

**What the evidence does not show:** the audit covers 20 answers, which is small. Our pricing checks caught the one pricing failure but none of the other 7 hallucinations. So the fixes must be re-tested on a larger set before the 30 November re-gate, not only on these 20 rows.

## Business Risk

**SHIP path:** the top 50 accounts each pay at least $50,000 a year, so at least $2.5M in annual revenue is exposed to a 10% Hard-failure rate _(derived: 50 × $50,000)_. If that rate holds, a VP who asks 10 questions has about a 65% chance of seeing at least one outdated price or unconfirmed fact _(derived: 1 − 0.9¹⁰)_. Each lost contract is worth $50,000–$100,000. Until the weekly live-answer judge is in place, the first person to notice an error would most likely be the client, not us. This is the harm that hits Q4 retention hardest.

**HOLD path:** we miss the CPO's original date by about 2–4 weeks, and the engagement lift we need for Q4 retention arrives later. A mid-December launch is still inside Q4. The cost of holding is time. The cost of shipping is trust, which is harder to win back than a date.

## Next Step · Decision Needed

**Approve the HOLD by Friday 13 November 2026.** What happens next:
- Engineering ships the price-database check and fixes the PR #218 faithfulness regression.
- The QA team adds the robustness test set and weekly live-answer judge by 30 November 2026, and re-runs all gates on that date.
- If the Hard gate is at 0%, the Soft gate is at or below 5% and the CI gates pass, we launch to the top 50 accounts in mid-December, inside Q4. If not, I come back with a new date and the numbers behind it.

## Reflection

Defining "good enough" made me put a number on each failure instead of trusting one overall score. Setting a 100% bar on pricing felt extreme until I saw that a $10 difference ($49 vs $59) is enough to break our promise of verified data. It also showed me how narrow one check can be: my three pricing checks each caught 1 of 8 hallucinations. And overriding 3 of the judge's 20 calls showed that the judge needs checking too. The hardest part was accepting that "good enough" sometimes means telling the CPO "not yet" when the deadline is close and the numbers say no.
