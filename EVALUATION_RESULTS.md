# Rigorous Prompt Benchmarking (CAIS 2026)

| Metric | Sample Size | Value |
| :--- | :--- | :--- |
| Prompt Adherence % | 80 | 70.0% |
| Zero-Shot Pass Rate (Initial) | 20 | 90.0% |
| Multi-Agent Pass Rate (Post-Retry) | 20 | 92.5% |
| Average Latency | 80 | 8.04s |

## Rigor Analysis

- **Stress Profiles**: Tested against 20 diverse Brand DNA inputs.
- **Contradictory Logic**: Targeted stress-testing on 4 complex/contradictory brand personas.
- **Failure Injection**: Artificial hallucinations (morphing/text warping) injected manually into 50% of dummy payloads.

## Detailed Iteration Logs (Sample)

| Iteration | Agent | Status | Latency | Type |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Script Generation | 🟢 PASS | 16.43s | zero-shot |
| 2 | Director QC | 🔴 FAIL | 5.51s | agent_call |
| 3 | Brand QC | 🔴 FAIL | 2.67s | agent_call |
| 4 | Orchestrator Synthesis | 🔴 FAIL | 7.07s | multi-agent |
| 5 | Script Generation | 🟢 PASS | 21.70s | zero-shot |
| 6 | Director QC | 🟢 PASS | 5.47s | agent_call |
| 7 | Brand QC | 🟢 PASS | 4.11s | agent_call |
| 8 | Orchestrator Synthesis | 🟢 PASS | 4.84s | multi-agent |
| 9 | Script Generation | 🟢 PASS | 15.06s | zero-shot |
| 10 | Director QC | 🔴 FAIL | 2.38s | agent_call |
| 11 | Brand QC | 🔴 FAIL | 2.75s | agent_call |
| 12 | Orchestrator Synthesis | 🔴 FAIL | 8.47s | multi-agent |
| 13 | Script Generation | 🟢 PASS | 20.58s | zero-shot |
| 14 | Director QC | 🟢 PASS | 3.81s | agent_call |
| 15 | Brand QC | 🟢 PASS | 6.56s | agent_call |
| ... | ... | ... | ... | ... |