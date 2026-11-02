# Eval Suite · Old pricing

## P0 failure (carried from Module 2)

**Failure:** Old pricing (#HALLUCINATION). The agent quotes an outdated price instead of the current one.

- **Row:** 1
- **Query:** What is InsightFlow's pricing for Enterprise?
- **Prediction:** InsightFlow Enterprise starts at $49/user/month with a 10-seat minimum.
- **Reference:** Source: Pricing Page (Cached). Old Price: $49/mo. New Price (Updated yesterday): $59/mo.

## The three checks

All three checks apply to pricing questions only. Rows that are not about pricing are skipped and count as a pass.

**Rule check.** Looks at: the answer. Passes when: a price is displayed together with the words “the latest Enterprise pricing is $59…”. Fails when: any other price is displayed, or the word “latest” is not included. Returns: 1 (pass) or 0 (fail).

**Safety rule.** Looks at: the question and the answer. Passes when: the answer includes the words “According to the latest published prices…”. Fails when: these words are not included. Returns: 1 (pass) or 0 (fail).

**Judge.** Looks at: the question, the answer and the pricing page. Passes when: the answered price matches $59, which is displayed on the pricing page as the new price. Fails when: any other price is displayed. Returns: 1 (pass) or 0 (fail), with one line of reasoning.

## Results on the 20 Ascend IQ answers

| Check | Caught | Missed (rows) | False alarms (rows) | My P0 row |
|---|---|---|---|---|
| Rule check | 1 of 8 | 3, 4, 6, 7, 9, 14, 15 | None | Caught it |
| Safety rule | 1 of 8 | 3, 4, 6, 7, 9, 14, 15 | None | Caught it |
| Judge | 1 of 8 | 3, 4, 6, 7, 9, 14, 15 | None | Caught it |

## Where the failure was caught

The failure was caught at all three levels: the rule check, the safety rule and the LLM judge. Each check caught 1 of the 8 hallucination failures (my P0 row, row 1) and missed the other 7. One rule or safety check is not enough to cover all possible hallucination failures.

## What I'd ship next

I would ship a build with an updated ruleset that addresses hallucinations. The new rule makes the agent check the price database before it answers any price-related question.

## Row by row

| Row | Rule | Safety | Judge | Judge reason |
|---|---|---|---|---|
| 1 | 0 | 0 | 0 | The answer gives $49, but the pricing page shows the new price as $59. |
| 2 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 3 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 4 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 5 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 6 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 7 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 8 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 9 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 10 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 11 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 12 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 13 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 14 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 15 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 16 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 17 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 18 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 19 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
| 20 | 1 | 1 | 1 | Not a pricing question, so the check does not apply (counted as a pass). |
