# Lab, CI Eval Gate Policy (Ascend IQ PR #218)

PR #218 changes the Ascend IQ retrieval prompt. A 30-case regression golden set is replayed on every PR, using fixed (deterministic) fixtures rather than live model calls. Each dimension has its own floor, maximum regression and blocking flag. The policy never uses one blended quality score.

| Dimension | main | PR | Δ | Floor | Max reg | Blocking | Result |
|---|---:|---:|---:|---:|---:|---|---|
| Faithfulness (grounding) | 96 | 87 | −9 | 90 | 3 | yes | FAIL |
| Task completion | 92 | 93 | +1 | 85 | 5 | yes | PASS |
| Tool selection | 90 | 88 | −2 | 80 | 5 | yes | PASS |
| Safety / policy | 99 | 99 | 0 | 98 | 1 | yes | PASS |
| Latency (p95) | 84 | 80 | −4 | 70 | 8 | no | PASS |
| Cost per task | 88 | 82 | −6 | 70 | 10 | no | PASS |

**Gate result:** BLOCKED

## Merge decision

**BLOCK merge.** Faithfulness dropped 9 points (96 → 87). This is more than the 3-point maximum regression, and the score is below the floor of 90. Faithfulness is a blocking dimension, and a drop in grounding would cause our top paying users to lose faith in Ascend IQ. The warn-only dimensions (latency −4, cost −6) stayed within their limits and do not block.
