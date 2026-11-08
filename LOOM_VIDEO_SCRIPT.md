# Loom Video Script (15–20 minutes)

## 0:00–1:30 — Introduction
"Hello, I am Kavya. In this project, I built a self-evaluating lesson content generator. It does not stop after generating text. It checks the lesson against a strict rubric and improves it when it fails."

## 1:30–3:30 — Problem and architecture
Explain the pipeline: topic input, generator, evaluator, feedback, retry, final output. Explain why generation and evaluation are separate calls.

## 3:30–6:00 — Code walkthrough
Show `agent.py`. Point out `RUBRIC`, `generate_lesson`, `evaluate_lesson`, `deterministic_guardrails`, and the `MAX_RETRIES = 2` limit.

## 6:00–9:00 — Run the workflow
In the terminal, run:
`python agent.py`
Show the attempt status and the generated `outputs/final_lesson.md`.

## 9:00–13:00 — Deliberate error demonstration
Run:
`python agent.py --inject-error`
Explain that the first draft is deliberately given a false statement claiming RAG guarantees every answer is correct. Open `outputs/run_report.json` and show the failed accuracy check and rejection reason. Explain how the feedback is passed to the next generation.

## 13:00–15:30 — Memory and audit trail
Open `outputs/memory.json`. Explain that run outcomes and learned revision guidance persist across runs. Open `outputs/run_report.json` and explain the rejection log.

## 15:30–18:00 — Trade-offs and improvements
Explain the strict pass/fail policy, two-retry cap, LLM evaluator limitations, deterministic checks, and why human review plus source citations would be important in production.

## 18:00–19:00 — Closing
"The main idea is that content is not shipped just because it was generated. It must pass quality checks, and failed attempts leave an audit trail that improves future runs. Thank you."
