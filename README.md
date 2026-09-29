# instruct.ai — Milestone 2 Prototype

**Project:** CourseGuide AI  
**Course:** CEN 4930 — AI Agent Studio, Fall 2026  
**Institution:** Florida Gulf Coast University (FGCU)

A real, running prototype of an instructor-configurable AI learning agent. The agent helps students reason through course-specific assignments without simply producing graded answers. It applies agent fundamentals, prompt engineering, tool integration, and MCP from Chapters 1–3.

## Problem

College students in reasoning-intensive courses increasingly have access to immediate general-purpose AI assistance, but that assistance is not automatically aligned with an instructor's course context, permitted help level, or expected reasoning process.

## What this agent does

- Takes a `course_id` and a student question.
- Uses an MCP tool to classify the help request (concept, hint, setup check, analogy).
- Uses an MCP tool to look up the instructor-defined course policy.
- Generates a guided, course-aligned response that respects the policy's boundaries.

## MCP tools integrated

- `lookup_course_policy(course_id)` — returns allowed help levels, forbidden help levels, tone, and style rules.
- `classify_help_request(question)` — classifies the student's request into a help type.
- `list_available_courses()` — lists configured course policies.

## Setup

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
```

Edit `.env` with your BYOM or NRP credentials.

## Run the agent

```bash
python -m src.m2_agent --course physics_101 --question "What is velocity?"
```

Or use the helper script:

```bash
bash scripts/run_m2.sh
```

## Run tests

```bash
bash scripts/run_tests.sh
```

The tests check five example prompts and verify that each response contains expected keywords.

## Known limitations

1. The agent does not yet inspect images or handwritten work.
2. Policy matching is exact; partial course names fall back to a generic policy.
3. Help classification is keyword-based; nuanced prompts may be mislabeled.
4. The MCP server launches over stdio; if `python` is not on PATH, the connection fails.
