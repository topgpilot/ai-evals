# AI Evaluation Strategy Canvas

## 1. Product Strategy, The Context

**Who it's for:** VP-level strategists and product leaders at Fortune 500 companies who pay upward of $50,000 a year for verified market intelligence.

**What they use it for:** Asking plain-language questions, like "Compare the pricing models of Stripe and Adyen," and getting answers in seconds instead of digging through the platform.

**What's at stake:** Engagement is dropping, Q4 retention is at risk, and the CPO wants Ascend IQ live for the top 50 enterprise accounts next month. One poor answer to the wrong client can do lasting damage to the relationship.

## 2. Measurements, The Execution

**User promise.** For all executive clients, Ascend IQ promises a verifiable, clear and brief response in about 5 seconds, without manual data mining, so that Ascend Analytics can meet its Q4 milestone on retention rate.

**Top 3 trust metrics:**
- **Latency**, Response speed (P95 / P99). 95% of answers (P95) must come back within 5 seconds, so that Ascend IQ stays faster than manual search and delivers immediate business value.
- **Hallucination Rate**, % of outputs that are confidently false or fabricated. VP-level clients invest $50K+ in verified data, and a single fabricated statistic can jeopardize the entire contract.
- **Robustness**, Coherence on messy, adversarial, or out-of-scope inputs. VPs often ask complex questions that cover several aspects at once, sometimes with typos, and they still expect a correct, verifiable and clear answer. If Ascend IQ fails on these inputs, VPs will lose trust in its ability to give a robust answer.

**Why these three:** Latency keeps Ascend IQ faster than manual search, Hallucination Rate protects the trust that the contracts depend on, and Robustness keeps answers correct and clear even when a question is complex or messy.

## 3. Strategic Trade-Offs, The Cost

### Trade-off 1 · Hallucination Rate ↔ Latency

We prioritize Hallucination Rate over Latency because VP-level clients rely on trusted and accurate data for strategic decisions. Any loss of trust from an inaccurate answer can jeopardize a contract worth $100,000, while a slower but more accurate response will build trust.

### Trade-off 2 · Robustness ↔ Latency

We prioritize Robustness over Latency because VP-level users are busy and make important decisions. When their question is complex or messy, the answer must still be presented in a clear, logical and unambiguous way, even if this takes longer.
