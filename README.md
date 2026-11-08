
# Self-Evaluating Lesson Content Generator

An offline Python prototype that generates a beginner-friendly lesson about **Introduction to RAG**, evaluates it using deterministic pass/fail checks, records rejected attempts, and saves the final lesson and evaluation report.

The workflow demonstrates a bounded generate → evaluate → retry → ship process without requiring an API key or an external LLM.

## 1. Architecture

```text
             Topic
               |
               v
       Lesson Generator
        (Offline Template)
               |
               v
       Rule-Based Evaluator
               |
          PASS / FAIL
           /       \
         PASS      FAIL
          |          |
          v          v
     Save Lesson   Rejection Log
     and Report         |
                        v
                 Retry (max 2)
                        |
                        v
                Save Run Memory
```

## 2. Design Choices

- **Separate generation and evaluation:** The generator and evaluator are separate functions.
- **Hard pass/fail checks:** Every required evaluation check must pass.
- **Deterministic evaluation:** Rule-based checks detect the deliberate false claim and verify lesson structure and coverage.
- **Bounded retries:** The workflow allows a maximum of two retries after the initial attempt.
- **Persistent memory:** `outputs/memory.json` stores run history and failure guidance.
- **Audit trail:** `outputs/run_report.json` records evaluation results and rejected attempts.

## 3. Evaluation Rubric

The evaluator checks eight dimensions:

1. Accuracy and grounded explanation
2. Beginner-friendly language
3. Step-by-step example
4. Explanation of technical terms
5. Coverage of key concepts
6. Logical teaching flow
7. Minimum lesson structure
8. Reliability limitations

A lesson is marked `PASS` only when all eight checks pass.

## 4. Requirements and Setup

- Python 3.10 or later
- No external API key required
- No external Python packages required for the current offline version

Open the project directory in the terminal and run:

```bash
python --version
```

## 5. Run the Project

Normal run:

```bash
python agent.py
```

Run with a custom topic:

```bash
python agent.py --topic "Introduction to RAG"
```

Run the deliberate-error demonstration:

```bash
python agent.py --inject-error
```

The demo inserts a deliberately false claim into the first lesson. The evaluator should reject the first attempt because the claim incorrectly says that RAG guarantees every answer is correct.

The workflow then runs another attempt and evaluates the clean lesson.

## 6. Outputs

The program creates the following files inside `outputs/`:

- `final_lesson.md` — generated beginner lesson.
- `run_report.json` — evaluation results, rejected attempts, and final status.
- `memory.json` — persistent run history and stored failure guidance.

## 7. Current Implementation Limitations

This is an offline prototype, not a complete LLM-powered agent.

- The lesson generator currently uses a fixed template rather than an LLM.
- The evaluator uses deterministic rules and does not perform semantic LLM evaluation.
- Failure guidance is stored in memory but is not yet used to intelligently modify the generated lesson.
- The retry demonstration regenerates the clean template after the deliberate error is injected.
- Keyword-based checks cannot prove factual correctness.

### Future Improvements

- Integrate an LLM for lesson generation.
- Add an independent LLM-based evaluator.
- Use evaluator feedback to revise lesson content dynamically.
- Apply persistent learning guidance during future generations.
- Add unit tests for retry limits, evaluation checks, and memory persistence.
- Add source-grounding and human review for production use.

## 8. Demo Results

Example output from the offline deliberate-error run:

```text
Attempt 1: FAIL
Attempt 2: PASS

Final status: SHIPPED
Attempts used: 2
```

The first attempt is rejected because the evaluator detects the false accuracy claim. The second attempt passes all eight deterministic checks.

## 9. Repository Structure

```text
rag_content_agent/
├── agent.py
├── README.md
├── requirements.txt
├── .env.example
├── .gitignore
└── outputs/
    ├── final_lesson.md
    ├── run_report.json
    ├── memory.json
    └── .gitkeep
```

## 10. Conclusion

This prototype demonstrates a simple quality-control workflow for beginner learning content. It shows how deterministic checks, rejection logging, bounded retries, and persistent run history can be combined in a Python application.

The current implementation is intentionally offline. LLM-based generation, semantic evaluation, and feedback-driven improvement are planned extensions.