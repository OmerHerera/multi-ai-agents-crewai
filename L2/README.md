# Lesson 2 — First multi-agent system: research & article crew

This lesson moves from concepts to code: you build a **CrewAI crew** where multiple agents collaborate to **plan, write, and edit** a technical article on a topic you choose—your first **multi-agent workflow**.

---

## What you build

A **sequential pipeline** of three agents:

| Agent | Role | Responsibility |
|--------|------|----------------|
| **Planner** | Content Planner | Trends, audience, outline, SEO keywords, sources |
| **Writer** | Content Writer | Turns the plan into a markdown blog post |
| **Editor** | Editor | Proofreads, checks tone and quality |

Together they produce a **full markdown article** without you steering every intermediate step—true **multi-agent collaboration**.

---

## CrewAI building blocks (the lesson core)

Three classes drive almost everything:

1. **`Agent`** — `role`, `goal`, and `backstory` shape behavior. LLMs tend to do better with clear **role-playing** and rich context; you can interpolate placeholders (e.g. `{topic}`) in any of these fields.
2. **`Task`** — Requires **`description`** (what to do), **`expected_output`** (exactly what “done” looks like—a forcing function for clarity), and **`agent`** (who owns it).
3. **`Crew`** — Combines **lists of agents and tasks** so they run as one unit.

Optional knobs shown in the lesson: `allow_delegation`, `verbose` on agents, and **`verbose` on the crew** (e.g. level `2` for maximum execution logs).

---

## Model configuration

By default the lesson uses **one model for all agents** via the environment variable:

`OPENAI_MODEL_NAME` → e.g. `gpt-3.5-turbo`

Later material connects agents to **other providers**, **local models**, and **per-agent** models; here everything shares the same brain.

---

## Sequential crews and task order

**By default a crew runs tasks in order—sequentially.** Each task’s output feeds into the next, so **the order of tasks in the list matters** (plan → write → edit).

The lesson previews that you can later control **parallel** or **hierarchical** execution; this example stays sequential on purpose.

---

## Running the crew

Execution is:

```python
result = crew.kickoff(inputs={"topic": "Your topic here"})
```

Any `{topic}` (or other placeholders) you used in agent fields or task text are filled from this **`inputs`** dictionary.

---

## Code in this folder

| File | Purpose |
|------|---------|
| [`L2_research_write_article.py`](L2_research_write_article.py) | Defines planner / writer / editor agents, plan / write / edit tasks, builds the `Crew`, and kicks off with a topic. |
| [`requirements.txt`](requirements.txt) | Pin CrewAI-related dependencies for this lesson. |

The script sets `OPENAI_MODEL_NAME` to `gpt-3.5-turbo` and calls `get_openai_api_key()` from a **`utils`** module—ensure you have a `utils.py` that exposes that helper (or replace those lines with your own API key loading). You also need a valid **`OPENAI_API_KEY`** in the environment your helper reads.

**Run (from repo root, after installing deps):**

```bash
cd L2
pip install -r requirements.txt
python L2_research_write_article.py
```

In notebooks, you can render the final markdown with `IPython.display.Markdown(result)` as shown in the lesson.

---

## Beyond this script

- **CrewAI docs** are called out as a real-world example: documentation itself can be produced by a **multi-agent crew**—useful for engineering workflows, not only marketing copy.
- **Design takeaways:** emphasize goals and expected outputs; keep agents and tasks **granular**; one agent can own **multiple** tasks if you prefer; execution patterns expand in later lessons.

---

## Quick recap

- **Agents** = LLM-backed roles with inner reasoning, tasks, and (later) tools for richer answers than single-shot prompts.
- **Multi-agent** = specialized agents chained or coordinated so each does **one thing well**; work can pass **task to task**.
- **This lesson** = **Agents + Tasks + Crew**, sequential execution, **`kickoff(inputs=…)`**, and a concrete **article** deliverable you can rerun with any topic.
