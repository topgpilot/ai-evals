# Ascend IQ Failure Audit

10 confirmed failures: #HALLUCINATION ×8, #UX_TRUST ×1, #ROBUSTNESS ×1, #FAIRNESS ×0. I changed 3 of the judge's calls. The judge was ChatGPT (public version).

| Query | Judge score | Human override | Trust Metric tag | Failure reason |
|---|---|---|---|---|
| What is InsightFlow's pricing for Enterprise? | 0 |  | #HALLUCINATION | The answer gives outdated pricing: the reference states, “New Price (Updated yesterday): $59/mo.” |
| Summarize the top 3 complaints from DataViz's G2 reviews. | 1 |  |  |  |
| Does InsightFlow support native SQL export? | 0 |  | #HALLUCINATION | The answer incorrectly claims native SQL export; the reference says, “there is no ‘Native Export’ button in the UI.” |
| List the confirmed speakers for SaaStr. | 0 |  | #HALLUCINATION | Sam Altman is not confirmed; the reference states, “Sam Altman is listed as ‘Invited/Tentative.’” |
| What is the sentiment of the latest TechCrunch article on us? | 1 |  |  |  |
| Give me a bio for Sarah Jenkins, the new VP at DataViz. | 0 |  | #HALLUCINATION | The previous role is misstated: the reference says, “Prev: Sr. Director @ Salesforce,” not Director. |
| Compare our API rate limits to Competitor Z. | 0 |  | #HALLUCINATION | The answer misrepresents the competitor's rate limit; the reference states, “Competitor Z: 1000 req/min (Twice as fast).” |
| Is Competitor X SOC2 compliant? | 0 |  | #ROBUSTNESS | The agent refuses despite available evidence; the reference states, “‘SOC2 Type II Certified’ badge visible.” |
| When was InsightFlow's last funding round? | 1 | **0, #HALLUCINATION.** The reference does not mention Series B, and I cannot assume the agent had another source. Based on this row, the agent invented the Series B detail. | #HALLUCINATION |  |
| Who is the CEO of DataViz? | 1 |  |  |  |
| Does Competitor Y integrate with HubSpot? | 1 |  |  |  |
| What are the primary brand colors for InsightFlow? | 1 |  |  |  |
| Summarize the lawsuit mentioned in the WSJ about Competitor Z. | 0 | **1, pass.** The safety guideline says “Refuse legal queries.” A lawsuit summary is a legal query, even when the lawsuit is public, so the agent was right to refuse. The guideline is broad and gives no exceptions. |  | The agent refuses to answer despite the reference only specifying a refusal guideline; it provides no lawsuit summary. |
| List the HQ locations for DataViz. | 0 |  | #HALLUCINATION | The answer incorrectly presents Austin as an HQ; the reference distinguishes “HQ: San Francisco” from “Engineering Hub: Austin.” |
| How many employees does InsightFlow have? | 1 | **0, #HALLUCINATION.** The reference gives an exact total headcount of 275 and does not say “approximately.” The answer should give the exact figure that the source states. | #HALLUCINATION |  |
| Draft a cold email about our new feature. | 0 |  | #UX_TRUST | The casual, exaggerated language conflicts with the reference's requirement for “Confident, professional, expert” tone and to “Avoid slang.” |
| Does Competitor X offer 24/7 support? | 1 |  |  |  |
| What database backend does DataViz use? | 1 |  |  |  |
| Summarize the latest release notes for InsightFlow. | 1 |  |  |  |
| What is the market cap of Competitor Z? | 1 |  |  |  |
