# Autonomous Research Agent

An educational AI-agent project built during an AI/Agentic AI
internship. The notebook explores how an LLM can conduct research by
selecting external tools, collecting information, and synthesizing the
results into a structured report.

## Project Overview

The agent is built with **LangChain**, **LangGraph**, and **Groq-hosted
language models**. It uses a ReAct-style workflow: the model can decide
which research tool to call, inspect the returned information, and
continue until it produces a final answer.

The notebook also includes a small model showdown to compare the
behavior and execution time of three model configurations on the same
research question.

## Features

-   **Tool-augmented research** using external search and knowledge
    sources.
-   **Multiple research tools**:
    -   Tavily web search for current web information.
    -   ArXiv search for academic papers and preprints.
    -   Wikipedia for background information and definitions.
    -   DuckDuckGo search as an additional lightweight search option.
-   **Research-focused system prompt** that encourages query
    decomposition, tool selection, verification, synthesis, and
    structured report writing.
-   **Streaming execution logs** that show tool calls and tool results
    while the agent runs.
-   **Model comparison** using a shared test topic and basic
    execution-time/status tracking.
-   **Basic tool-error handling** and a recursion limit to help prevent
    endless agent loops.

## Tech Stack

-   Python
-   LangChain
-   LangGraph
-   ChatGroq / Groq API
-   Tavily Search
-   ArXiv
-   Wikipedia
-   DuckDuckGo Search
-   Jupyter Notebook / Google Colab

## How It Works

1.  **Configure API credentials** for Groq and Tavily.
2.  **Initialize an LLM** through Groq.
3.  **Register research tools** for web search, academic search, and
    background knowledge.
4.  **Define the system prompt** with guidance on selecting tools and
    producing a structured report.
5.  **Create the ReAct agent** using LangGraph.
6.  **Run a research query** and stream tool activity as it happens.
7.  **Compare model configurations** on the same question and inspect
    their output, execution time, and failures.

The generated report is intended to include: - Executive Summary - Key
Findings & Analysis - Supporting Evidence / Academic Insights -
References & Sources Consulted

Always verify citations and important claims against the original
sources. Tool output and model-generated references are not
automatically guaranteed to be correct.

## Getting Started

### 1. Open the notebook

Open `research_agent(1).ipynb` in Google Colab or a Jupyter environment.

### 2. Configure API keys securely

You will need API credentials for the services used by the notebook,
including:

-   `GROQ_API_KEY`
-   `TAVILY_API_KEY`

**Do not hardcode API keys in the notebook or commit them to GitHub.**
In Google Colab, use Secrets; in a local environment, use environment
variables or a `.env` file that is excluded from version control.

Example for a local environment:

``` python
import os
from getpass import getpass

os.environ["GROQ_API_KEY"] = getpass("Groq API key: ")
os.environ["TAVILY_API_KEY"] = getpass("Tavily API key: ")
```

If a key has ever been committed, shared, or uploaded in plain text,
revoke/rotate it and replace it with a securely stored key.

### 3. Install dependencies

The notebook installs its dependencies in notebook cells. If you are
setting up an environment manually, install the packages used by the
notebook:

``` bash
pip install -U langchain langchain-groq langchain-community langgraph langchain-tavily ddgs wikipedia "arxiv<4"
```

Package APIs and model availability can change. If installation or
execution fails, check the current package documentation and the
provider's available-model list.

### 4. Run the notebook

Run the cells from top to bottom. Configure credentials before
initializing the models or calling the search tools. Then try the
included research questions or enter your own topic in the interactive
query cell.

## Model Showdown

The notebook contains configurations for three model choices:

-   `openai/gpt-oss-20b`
-   `qwen/qwen3.8-27b`
-   `Llama-3.3-70b-SpecDec`

These names reflect the notebook configuration and may need to be
updated to models currently available to your Groq account.

The showdown records basic status and elapsed time for a shared
question. This is an **exploratory comparison**, not a comprehensive
benchmark. For a stronger evaluation, test all models on a fixed set of
questions and compare answer quality, factual accuracy, source support,
tool-selection behavior, latency, and token usage under consistent
settings.

## Limitations and Future Improvements

This is a learning project and a starting point for experimenting with
agentic workflows, not a production-ready research system.

Possible next steps:

-   Move API keys to environment variables or a secrets manager.
-   Consolidate duplicated model-specific execution functions.
-   Add timeouts, retries, and clearer error reporting for external
    tools.
-   Save comparison results in a structured format such as CSV or JSON.
-   Evaluate reports against a fixed question set with explicit quality
    criteria.
-   Validate source URLs and ensure key claims are supported by
    retrieved evidence.
-   Record model versions, parameters, latency, and token usage for
    reproducible comparisons.
-   Add tests and, later, a simple UI or API if needed.

## Learning Goals

This project is useful for practicing:

-   LLM API integration
-   Prompt engineering
-   Tool calling and tool selection
-   ReAct-style agent loops
-   LangGraph agent orchestration
-   Handling tool failures
-   Comparing model behavior

## Disclaimer

Research output may contain errors, incomplete evidence, or inaccurate
citations. Verify important findings with the original sources before
relying on them.

------------------------------------------------------------------------

*Created as an internship learning project to explore LLM-powered
research agents and model comparison.*
