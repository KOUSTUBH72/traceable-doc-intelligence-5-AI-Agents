# Document Intelligence Agent

A small app where 5 AI agents work together to answer questions about LLM production and security. Every step is traced with LangSmith, so you can see exactly what each agent did.

## What it does

You ask a question. The agents work in order:

1. Planner: makes the question clearer
2. Document Reader: searches my local guide for answers
3. Web Enricher: searches the web live (Google Serper)
4. Synthesizer: combines both sources (Groq)
5. Report Writer: writes the final report (Gemini)

## Built with

- LangGraph: connects the agents
- LangSmith: tracing and observability
- Streamlit: the app screen
- Groq and Gemini: the language models
- Serper: web search

## How to run it

1. Install the packages:
   uv pip install -r requirements.txt

2. Copy `.env.example` to `.env` and add your own keys:
   GROQ_API_KEY=
   GEMINI_API_KEY=
   SERPER_API_KEY=
   LANGSMITH_API_KEY=
   LANGSMITH_TRACING=true
   LANGSMITH_ENDPOINT=https://api.smith.langchain.com

3. Start the app:
   streamlit run app.py

4. Optional: open LangGraph Studio
   langgraph dev

## Seeing the traces

Open https://smith.langchain.com and select your project. Each question shows up as one trace, with a step for every agent, tool call and model answer.

## Security notes

- Keep API keys in `.env` only. Never commit this file.
- LangSmith traces store prompts and answers in plain text. Hide inputs and outputs, or mask personal data, before using real data.
- Text from documents and web pages is untrusted. It can contain hidden instructions, so treat it as data, not commands.
- Tracing records what happened. It does not stop attacks.

## Project layout

- agent/: the 5 agents and the graph
- app.py: the Streamlit app
- graph_entry.py and langgraph.json: setup for LangGraph Studio
- data/: the local guide the Document Reader searches

## What I learned

Building agents is the easy part. Seeing what they do, step by step, is what makes them safe to trust.