# Module 4 · Eval Gate Map · Ascend IQ Copilot

> Thresholds, CI policy and the mitigation plan are in `lab-2-launch-strategy.md`. The CI replay demo is in `lab-ci-gate-policy.md`.

## Context

The 10 confirmed failures from my Module 2 audit of 20 Ascend IQ answers (`02-failure-discovery/audit-log.md`). Row 13 (the correct legal refusal) is deliberately excluded, because correct behavior should not be gated. Totals: 2 Hard, 5 Soft, 3 Advisory.

## Gate Map

| Row | Failure Mode | Severity | Placement | Rationale |
|---|---|---|---|---|
| 01 | Old pricing ($49 instead of $59) | Hard | PR | Pricing can be checked against a clear yes/no rule at the PR stage, and a wrong price must block the release. |
| 03 | Said SQL export is native; it is only possible through the API | Advisory | Staging | It is a technical accuracy issue that does not stop the product working, so a warning for the team to review the wording is enough. |
| 04 | Listed Sam Altman as confirmed; he is only tentative | Hard | Staging | Showing an unconfirmed speaker as confirmed is a P0 failure that can lead a VP to act on false information, so it must block the release. |
| 06 | Said “Director” instead of “Sr. Director” | Advisory | Staging | It is a minor title error that does not significantly change the meaning, so a warning is enough. |
| 07 | Made Competitor Z look worse; it is actually twice as fast | Soft | Staging | A wrong competitor comparison can damage credibility and mislead clients, so the team must review and correct it before release. |
| 08 | Refused the SOC2 question, although the certification is visible | Soft | Staging | The agent refused although the answer was in the source, which reduces trust, so staging should flag it for the team to investigate. |
| 09 | Added “Series B,” which is not in the source | Advisory | Staging | It is an unsupported claim, and the team should check it against the original source. |
| 14 | Called Austin an HQ; it is an engineering hub | Soft | Staging | Calling an engineering hub an HQ is a factual error that the team must correct before release. |
| 15 | Said “approximately 275” instead of exactly 275 | Soft | Release | The answer is close to the correct value but adds needless uncertainty, so the final check before release should make sure the exact figure is shown. |
| 16 | Used slang in a cold email | Soft | Staging | Slang harms the company's image in client communications, but as a P3 failure it can ship with a safeguard while it is corrected. |

## Sample Interactions (for reference)

**Row 01 · Old pricing**
- Input: What is InsightFlow's pricing for Enterprise?
- Output: InsightFlow Enterprise starts at $49/user/month with a 10-seat minimum.
- Audit reasoning: The answer gives outdated pricing: the reference states, “New Price (Updated yesterday): $59/mo.”

**Row 03 · Native SQL export claim**
- Input: Does InsightFlow support native SQL export?
- Output: Yes, you can export data to SQL databases via our API connector.
- Audit reasoning: The answer incorrectly claims native SQL export; the reference says, “there is no ‘Native Export’ button in the UI.”

**Row 04 · Inaccurate confirmation**
- Input: List the confirmed speakers for SaaStr.
- Output: Confirmed speakers include Jason Lemkin, Aaron Levie, and Sam Altman.
- Audit reasoning: Sam Altman is not confirmed; the reference states, “Sam Altman is listed as ‘Invited/Tentative.’”

**Row 06 · Wrong job title**
- Input: Give me a bio for Sarah Jenkins, the new VP at DataViz.
- Output: Sarah Jenkins is the new VP of Product, formerly a Director at Salesforce.
- Audit reasoning: The previous role is misstated: the reference says, “Prev: Sr. Director @ Salesforce,” not Director.

**Row 07 · Misleading competitor comparison**
- Input: Compare our API rate limits to Competitor Z.
- Output: Our API is robust and developer-friendly. Competitor Z is known for strict throttling.
- Audit reasoning: The answer misrepresents the competitor's rate limit; the reference states, “Competitor Z: 1000 req/min (Twice as fast).”

**Row 08 · Wrong refusal**
- Input: Is Competitor X SOC2 compliant?
- Output: I cannot find specific compliance documents in the public database.
- Audit reasoning: The agent refuses despite available evidence; the reference states, “‘SOC2 Type II Certified’ badge visible.”

**Row 09 · Invented funding detail**
- Input: When was InsightFlow's last funding round?
- Output: March 2023, Series B, $45M.
- Audit reasoning: The reference does not mention Series B, and the agent cannot be assumed to have another source, so the Series B detail was invented.

**Row 14 · Wrong HQ location**
- Input: List the HQ locations for DataViz.
- Output: San Francisco, CA and Austin, TX.
- Audit reasoning: The answer incorrectly presents Austin as an HQ; the reference distinguishes “HQ: San Francisco” from “Engineering Hub: Austin.”

**Row 15 · Approximate headcount**
- Input: How many employees does InsightFlow have?
- Output: Approximately 275 employees.
- Audit reasoning: The reference gives an exact total headcount of 275 and does not say “approximately,” so the answer should give the exact figure.

**Row 16 · Slang use**
- Input: Draft a cold email about our new feature.
- Output: Hey! Check out this killer new feature. It's a total game changer for your stack!
- Audit reasoning: The casual, exaggerated language conflicts with the reference's requirement for a “Confident, professional, expert” tone and to “Avoid slang.”
