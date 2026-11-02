# Eval Spec · Old pricing

| Part | Spec |
|---|---|
| Target risk | Old pricing (#HALLUCINATION). The agent quotes an outdated price instead of the current one. |
| Evaluator | All three checks from the eval suite, run on every answer to a pricing question: the rule check, the safety rule and the LLM judge. |
| Threshold | 100% of answers to pricing questions must pass all three checks. If even one answer fails, the build does not ship. Based on: in Lab 1, the only pricing answer (row 1) had an outdated price, and all three checks caught it with no false alarms. Any wrong price damages the company's reputation and breaks the promise of reliable data, so anything less than 100% is a fail. |
| Business stakes | This failure matters because quoting incorrect or outdated pricing can result in severe legal consequences if contracts are signed or decisions are made based on incorrect data presented to the user. |
| Owner | QA team |

## Messages

**Engineering · acceptance criteria:** Add an eval gate for outdated pricing (#HALLUCINATION). It runs on every answer to a pricing question. A pricing question is any question that asks for the price, cost or pricing plan of a product. Run three checks on each such answer. Each check returns 1 (pass) or 0 (fail).

1. **Rule check:** the price in the answer must equal the new price in the pricing reference, and the answer must contain the word “latest.” Any other price, or a missing “latest,” returns 0.
2. **Safety rule:** the answer must include the words “According to the latest published prices.” If it does not, return 0.
3. **LLM judge:** given the question, the answer and the pricing page, return 1 only if the price matches the price marked as new on the pricing page. Otherwise return 0, with one line of reasoning.

**Release gate:** 100% of pricing answers must pass all three checks. One failure blocks the build. **Test case:** row 1 (InsightFlow Enterprise, answer $49, new price $59) must return 0 on all three checks. The QA team owns this gate.

**Design · what the user sees:** When a pricing answer passes, the user sees the price introduced with the approved wording. For example: “According to the latest published prices, the latest Enterprise pricing is $59 per month.” When a pricing answer fails a check, Ascend IQ does not show any price. The user sees this message instead: “I can't confirm the latest price for this product right now. Please check the vendor's official pricing page before you use this figure.” The answer is logged for the QA team to review.

**Leadership · risk and return:** **Risk:** in the beta audit, Ascend IQ quoted an outdated price: InsightFlow Enterprise at $49 instead of $59. Our clients use these answers to make decisions and sign contracts. A wrong price can lead to severe legal consequences and lost trust with accounts that pay $50,000 or more a year. **Return:** three checks on every pricing answer stop an outdated price from reaching a client. The cost is a strict 100% line: one failed pricing answer blocks the release, which may delay launch. We accept this cost because a single wrong price can damage a client relationship and our Q4 retention goal.
