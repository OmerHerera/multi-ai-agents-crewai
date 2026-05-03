# Multi-Agent AI with CrewAI

Course companion notes and examples for building **multi-agent systems** with **[CrewAI](https://www.crewai.com/)**—an open-source framework (with an optional production platform) oriented toward real-world use.

---

## Why agents (not “just chat”)?

Large language models come from many vendors (OpenAI, Hugging Face, Ollama, and others) and fundamentally **predict the next token**. Chat-style use feels like **ChatGPT**: you iterate with prompts and feedback until the output is good enough.

That loop works because **quality improves through interaction** you correct length, tone, or facts. The downside is **you become the bottleneck**: you must stay in the conversation instead of doing other work.

**Agents** aim to break that pattern: the model can **reason and revise on its own** asking and answering its own sub-questions until it reaches an answer it is satisfied with, **without you in every step**.

---

## What makes an agent “full”?

Two ideas matter:

1. **Self-directed reasoning** — The model moves beyond a single-shot reply by reflecting, refining, and optimizing before returning a final answer.
2. **Tools** — Agents connect to the outside world (APIs, posting, data retrieval, etc.). Other stacks may call these **skills** or **capabilities**; they extend what plain text generation cannot do alone.

Together, reasoning plus tools describes a capable, autonomous-style agent.

---

## Multi-agent systems

A **multi-agent system** scales that idea: **several agents collaborate**. One agent can **delegate** work to another; you still aim for **one coherent final result**.

**Benefits:**

- **Specialization** — Each agent does one job well (e.g. a researcher vs. a writer).
- **Different models per role** — e.g. one agent on Llama 3, another on GPT-4, or a fine-tuned model for a specific step—often stronger than one model trying to do everything.

---

## Why CrewAI?

Concepts here apply broadly, but examples use **CrewAI** because it:

- Maps ideas to **simple structures** that are easy to learn.
- Gives an **opinionated pattern** for wiring agents together so you spend less time on plumbing.
- Ships **ready-made tools** used throughout the lessons.
- Supports **custom tools and agents** when you need something bespoke.
- Offers an optional **platform** to move what you build toward production.

---

## Core building blocks (next steps)

Upcoming material focuses on three primitives:

- **Agents**
- **Tasks**
- **Crews**

Together they form the foundation for your **first multi-agent system**.

---

## Outcomes

By working through this material you can automate slices of personal and professional workflows with agents, combining focused roles, tools, and (when useful) multiple models—**with CrewAI as the framework used in the examples**.

---

## Repository status

This repository is set up as the home for course-related code and notes.

---

## Running the Project

### Requirements

Before running any examples, ensure you have the following installed:

- **Python 3.11 or higher** — [Download here](https://www.python.org/)
- **Ollama** — For running LLMs locally — [Download here](https://ollama.ai/)

### Setting up Ollama

1. **Install Ollama** from [ollama.ai](https://ollama.ai/)
2. **Start the Ollama server** in a terminal:

   ```bash
   ollama serve
   ```

   This starts Ollama on `http://localhost:11434` (default port)

3. **Pull a model** (in another terminal):
   ```bash
   ollama pull llama2
   ```
   You can also use other models:
   ```bash
   ollama pull mistral
   ollama pull neural-chat
   ```

### Setting up Python Environment

1. **Navigate to the project directory**:

   ```bash
   cd /path/to/multi-ai-agents-crewai
   ```

2. **Create a Python virtual environment** (recommended):

   ```bash
   python3 -m venv venv
   ```

3. **Activate the virtual environment**:
   - **macOS/Linux**:
     ```bash
     source venv/bin/activate
     ```
   - **Windows**:
     ```bash
     venv\Scripts\activate
     ```

4. **Install dependencies**:
   ```bash
   cd L2
   python3 -m pip install -r requirements.txt
   ```

### Running the Examples

#### L2 - Research & Article Writing

Navigate to the `L2` directory and run the research article example:

```bash
cd L2
python3 L2_research_write_article.py
```

This will:

- Create a **Content Planner** agent that researches the topic and creates an outline
- Create a **Content Writer** agent that writes the article based on the plan
- Create an **Editor** agent that reviews and finalizes the article
- Generate a complete blog article using your local Ollama instance

The topic can be customized by editing the `crew.kickoff()` call at the bottom of the script.

### Troubleshooting

**Issue**: `command not found: python`

- **Solution**: Use `python3` instead, or add Python to your PATH

**Issue**: `ModuleNotFoundError` when running scripts

- **Solution**: Ensure you've installed dependencies with `pip install -r requirements.txt`

**Issue**: Connection refused to `http://localhost:11434`

- **Solution**: Make sure Ollama is running (`ollama serve` in a separate terminal)

**Issue**: Model not found

### Troubleshooting

**Issue**: `command not found: python`

- **Solution**: Use `python3` instead, or add Python to your PATH

**Issue**: `ModuleNotFoundError` when running scripts

- **Solution**: Ensure you've installed dependencies with `pip install -r requirements.txt`

**Issue**: Connection refused to `http://localhost:11434`

- **Solution**: Make sure Ollama is running (`ollama serve` in a separate terminal)

**Issue**: Model not found

- **Solution**: Pull the model first with `ollama pull <model_name>`
