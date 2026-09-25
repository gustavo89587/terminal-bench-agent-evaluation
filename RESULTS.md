# Experiment Results

## Task

`session-window-debug`

## Oracle Baseline

- Trials: 1
- Exceptions: 0
- Reward: 1.0
- Classification: Positive control

## NOP Baseline

- Trials: 1
- Exceptions: 0
- Reward: 0.0
- Classification: Negative control

## Gemini CLI Attempt

- Model configured: `gemini-2.5-flash`
- Task execution reached: No
- Failure: Authentication / upstream eligibility
- Included in model evaluation: No

## OpenHands Attempt

- Intended backend: Local Ollama
- Intended model: `qwen2.5:3b`
- Task execution reached: No
- Failure: Agent adapter installation
- Included in model evaluation: No

## Interpretation

The Oracle and NOP controls demonstrate that the benchmark pipeline can
produce both successful and unsuccessful verifier outcomes.

The Gemini CLI and OpenHands attempts demonstrate why infrastructure and
agent-integration failures must be separated from model-performance results.

No comparative model-performance conclusion is made from those attempts.
