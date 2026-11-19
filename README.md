# IBM RAG and Agentic AI Professional Certificate: Labs

My hands-on lab work from the [IBM RAG and Agentic AI Professional Certificate](https://www.coursera.org/professional-certificates/ibm-rag-and-agentic-ai) on Coursera. The program covers building generative AI applications with prompt engineering, LangChain, retrieval-augmented generation (RAG), vector databases, multimodal models, and AI agents (LangGraph, CrewAI, AG2, MCP).

Each course has its own folder with the lab notebooks and a short README on what I built and learned. Larger portfolio projects that build on this coursework live in separate repositories.

## Progress

| # | Course | Status | Labs |
|---|--------|--------|------|
| 1 | Develop Generative AI Applications: Get Started | 🟡 In progress | [Course 1 labs](course-01-develop-generative-ai-applications-get-started/) |
| 2–9 | … | ⚪ Not started | |
| 10 | RAG and Agentic AI Capstone Project | ⚪ Not started | |

## Highlights so far
- **Prompt engineering with IBM Granite:** zero-, one- and few-shot prompting, chain-of-thought and self-consistency, compared on real model outputs.
- **LangChain LCEL chains:** a product review analyzer that returns structured JSON (`prompt | llm | JsonOutputParser`), which removed the extra fields the model made up in free-text mode.

## Tech stack
Python · LangChain (LCEL) · IBM watsonx.ai · IBM Granite · Jupyter

## Running the notebooks
The labs were run in IBM Skills Network's hosted JupyterLab, which provides watsonx.ai access without API keys. To run them locally, create a watsonx.ai project and supply your own credentials through environment variables (never commit keys):

```bash
pip install "ibm-watsonx-ai==1.0.8" "langchain==0.2.11" "langchain-ibm==0.1.7" "langchain-core==0.2.43"
export WATSONX_APIKEY="your-key"
export WATSONX_PROJECT_ID="your-project-id"
```

## Credits
Lab material © IBM Skills Network, from the IBM RAG and Agentic AI Professional Certificate. Exercise solutions, extensions and write-ups are my own.
