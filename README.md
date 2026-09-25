# Terminal-Bench Agent Evaluation

A small hands-on experiment with Terminal-Bench and Harbor focused on
AI agent evaluation, verifier-based scoring, and failure classification.

## Objective

The goal was to build and validate an evaluation workflow for terminal-based
AI agents and distinguish actual agent performance from failures in the
surrounding evaluation infrastructure.

## Environment

- Terminal-Bench
- Harbor 0.23.0
- Docker
- Ubuntu/Linux
- Task: `session-window-debug`

The task involves debugging a session-window processor handling event-time
semantics, late events, session merging, and watermark progression.

## Method

I used two controls to validate the evaluation pipeline.

### Positive control — Oracle

The Oracle agent was used to verify that the task and verifier were capable
of producing a successful result.

Result:

| Agent | Trial | Exceptions | Reward |
|------|------:|-----------:|-------:|
| Oracle | 1 | 0 | 1.0 |

This established the positive baseline.

### Negative control — NOP

A NOP agent was then executed through the same benchmark pipeline.

Result:

| Agent | Trial | Exceptions | Reward |
|------|------:|-----------:|-------:|
| NOP | 1 | 0 | 0.0 |

The trial completed normally and produced the expected negative baseline.

## Agent Integration Experiments

I also attempted to evaluate real LLM-based agents.

### Gemini CLI

The Gemini CLI adapter was successfully installed and Harbor accepted the
configured model.

Execution did not reach meaningful task interaction because authentication
was rejected by the upstream service with an eligibility error.

Classification:

`Agent integration / authentication failure`

This result was excluded from model-performance conclusions.

### OpenHands

An OpenHands trial was also attempted using a local Ollama endpoint.

The agent did not reach task execution because the Harbor adapter installation
failed while attempting to load the installed OpenHands package.

Classification:

`Agent adapter / environment setup failure`

This result was also excluded from model-performance conclusions.

## Failure Classification

One of the most useful outcomes of the experiment was separating benchmark
results from infrastructure failures.

I used the following conceptual classification:

    Environment setup
          ↓
    Agent setup
          ↓
    Authentication / model connection
          ↓
    Agent execution
          ↓
    Verifier execution
          ↓
    Reward

A failure before agent execution should not be interpreted as evidence that
the model failed the task.

Likewise, a reward of `0.0` only becomes meaningful for agent-performance
analysis when the agent actually had an opportunity to interact with the
task environment.

## Results

| Execution | Status | Reward | Interpretation |
|---|---|---:|---|
| Oracle | Completed | 1.0 | Positive control |
| NOP | Completed | 0.0 | Negative control |
| Gemini CLI | Integration failure | N/A | Excluded |
| OpenHands | Adapter setup failure | N/A | Excluded |

## Key Takeaway

**A benchmark failure is not necessarily an agent failure.**

Agent evaluation requires separating failures in infrastructure,
authentication, adapters, execution, and verification before interpreting
benchmark scores.

This distinction becomes especially important when evaluating autonomous
agents because the evaluation harness itself introduces multiple failure
boundaries that can otherwise contaminate conclusions about model behavior.

## What I Practiced

- Terminal-Bench task execution
- Harbor evaluation workflows
- Oracle baseline validation
- Negative-control experiments
- Verifier-based scoring
- Docker-based agent environments
- Agent integration troubleshooting
- Failure classification
- Reproducible AI-agent evaluation methodology

## Scope

This experiment validates the evaluation workflow and methodology.

It does **not** claim comparative performance results for Gemini, OpenHands,
or their underlying models because those integrations did not reach
meaningful task execution.
