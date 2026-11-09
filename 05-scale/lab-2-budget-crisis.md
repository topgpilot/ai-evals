# Lab 2, Ascend IQ Budget Crisis

> Repo file `ai-evals/05-scale/lab-2-budget-crisis.md`. Allocate Level 1/2/3 coverage across the 5 failure modes under the **$200K/quarter cap** with **max 3 at Level 3**.

**Quarterly budget cap:** $200,000
**Total Level 3 spend:** $175,000 (3 of max 3 L3 slots used)

## Portfolio decision grid

| Failure | Trust metric | Risk | Level | Cost |
|---|---|---|---|---|
| Data Fabrication | Hallucination Rate | P0 | L3 | $85,000 |
| Context Specificity | UX Trust | P1 | L2 | $7,000 |
| Source Attribution Failure | Robustness | P1 | L3 | $65,000 |
| Data Bias | Fairness | P2 | L2 | $5,500 |
| Cost Overruns | Latency | P3 | L3 | $25,000 |
| **Total** | | | **3 × L3, 2 × L2** | **$187,500 of $200,000** |

_Reference L3 costs: Hallucination $85K · Context $70K · Attribution $65K · Bias $55K · Latency $25K. L2 ≈ 10% of L3, L1 ≈ 5% of L3._

**Running total:** $85,000 + $7,000 + $65,000 + $5,500 + $25,000 = **$187,500**. That leaves $12,500 under the cap.

**Why these three get Level 3:** they are the three trust metrics from my Module 1 strategy canvas (Hallucination Rate, Robustness, Latency). Hallucination is our P0: 8 of the 10 confirmed failures in the Module 2 audit were hallucinations. Robustness is the gap I could not accept in Lab 1. Latency is our 5-second promise to clients and costs only $25K. **The trade-off:** we could not afford L3 for both P1 items. Hallucination + Context + Attribution would cost $220,000, which is over the cap. So Context Specificity drops to L2.

## Fallback methods (non-Level 3 items)

### L2 · Context Specificity (UX Trust · P1)
- **Method:** the Soft gate from Module 4. Before release, an LLM judge at staging checks a sample of answers against the brand guideline ("Confident, professional, expert" and "Avoid slang"). The release is held if more than 5% of answers fail.
- **Why this fallback is defensible:** this is the P1 we downgraded. In the Module 2 audit, UX Trust was our least frequent failure: 1 of 20 answers (the slang cold email), which I rated P3 in my failure taxonomy. A wrong tone is embarrassing, but it does not give a VP a false figure to act on, which a hallucination does. In an incident review, we can show that every release still passes the ≤ 5% Soft gate. We will move this to L3 if the Soft gate fails two releases in a row on tone.

### L2 · Data Bias (Fairness · P2)
- **Method:** once a month, the QA team reviews a sample of answers across client regions and industries, scored with the same LLM judge. A gap between groups is logged and reviewed.
- **Why this fallback is defensible:** this is the Fairness gap I accepted in Lab 1, and the same reasoning applies: we target the European market, where most of our paying customers are, and everything is in English only. So the risk of uneven quality across languages is low today, and full L3 coverage ($55,000) would cost more than the risk. The kill criterion is the same as in Lab 1: we move to L3 when non-English-speaking clients pass 25% of our clients, or when clients ask for answers in other languages.
