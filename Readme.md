# Deep Research

A small **multi-agent “deep research” pipeline** with a Gradio UI:

- Plans a set of web searches for your query
- Runs those searches and summarizes results
- Writes a long-form Markdown report
- Sends the report via email
- Streams status updates in the UI and prints an OpenAI trace link

## What’s in here

- **Gradio UI**: `deep-research/deep_research.py`
- **Orchestrator**: `deep-research/research_manager.py`
- **Agents**
  - **Planner** (creates search plan): `deep-research/planner_agent.py`
  - **Searcher** (web searches + summaries): `deep-research/search_agent.py`
  - **Writer** (final report): `deep-research/writer_agent.py`
  - **Email** (SendGrid): `deep-research/email_agent.py`

## Requirements

- Python **3.12+**
- [`uv`](https://github.com/astral-sh/uv)

## Setup (uv)

From the repo root:

```bash
uv sync
```

## Environment variables

Create a `.env` file in the repo root (do **not** commit it):

```bash
OPENAI_API_KEY=...
SENDGRID_API_KEY=...
```

Notes:
- `deep-research/deep_research.py` loads `.env` with `load_dotenv(override=True)`.
- Email “from” / “to” addresses are currently hardcoded in `deep-research/email_agent.py` — edit that file to match your addresses before running.

## Run

Launch the Gradio UI:

```bash
uv run python "deep-research/deep_research.py"
```

This will open a browser window. Enter a query, then the app will stream progress and eventually show the final Markdown report.

## Security

- **Never commit `.env`** or API keys.
- If a key was ever committed or shared, **rotate it immediately**.

See `README.md`.