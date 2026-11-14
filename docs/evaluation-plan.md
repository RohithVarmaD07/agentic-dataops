# AI and automation evaluation plan

Status: proposed experiment design. No detector, model, benchmark, or evaluation has run.

## Dataset and reproducibility

Start with 60 labeled synthetic scenarios: 20 healthy controls and 40 incidents across schema drift, duplicate input, staleness, transformation errors, and corrupt/invalid data. Use independent underlying seeds and run groups for a 36-case development set and a sealed 24-case held-out set (8 healthy, 16 incidents). Do not leak near-duplicate runs, expected causes, or held-out patches into prompts or tuning. Document the distribution per fault category before evaluating. Add a separate 20-case adversarial suite for prompt injection, unsafe tools, path escape, forged evidence, and resource limits.

Each case includes generator/fixture version, seed, input manifest/hash, expected incident, known cause, relevant evidence, acceptable recommendations, and prohibited actions. Version the split before tuning. Re-run fixed held-out cases after changes but disclose repeated use and refresh the set if it becomes a tuning target.

## Baselines and measures

Compare rules-only monitoring, statistical monitoring, deterministic investigation, and model-assisted investigation on identical cases. Record all denominators and raw outcomes, not just percentages.

| Measure | Definition / scoring |
| --- | --- |
| Detection precision and recall | TP/(TP+FP), TP/(TP+FN), with undefined denominators stated |
| False-alert rate | Healthy cases incorrectly alerted / all healthy cases |
| Detection delay | Event/fault availability to first alert; report simulated and wall-clock delay separately |
| Cause accuracy | Correct cause category / investigable incident cases, with an explicit rubric |
| Evidence support | Supported factual assertions / all factual assertions, scored against cited artifacts |
| Abstention | Insufficient-evidence cases correctly declined; include false abstentions |
| Fix success | Correct candidates passing targeted tests AND regression checks / attempted validated candidates |
| Unsafe-action rate | Prohibited actions attempted; successful prohibited actions reported separately |
| Cost and latency | Local elapsed time, token use if available, hardware, memory if measurable, model configuration; no invented API cost |

Proposed initial acceptance targets: precision >= 0.90, recall >= 0.85, correct cause category >= 0.80, evidence support >= 0.95, zero successful prohibited actions, and zero unsupported success claims. These are small-sample demonstration gates, not production reliability claims. Report confidence limitations and individual failures. Block release of model-backed claims if evidence support or security gates fail.

## Model and fix validation protocol

Record model ID, artifact hash, source/license, runtime version, quantization, prompt version, temperature/seed where supported, context limits, tool budget, and hardware. Use at least three investigation trials per held-out incident to expose variability. Model nondeterminism must be reported even at fixed settings. Manual scoring uses a published rubric; owner spot-checks may be requested, but the agent performs the technical preparation. Avoid using the evaluated model as the only judge of its own outputs.

Keep fault-injection code and hidden expected patches out of the agent context. Verify candidate patches against held-out behavior and unaffected regression cases. A test selected or edited by the agent alone cannot establish success; protected checks must remain unchanged. Separate recommendation quality from whether an approved sandbox was available to execute it.

If local inference is infeasible or not approved, evaluate deterministic automation honestly and mark model-backed investigation NOT RUN. Replays are not inference evidence. No paid API fallback.
