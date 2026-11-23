# IBM RAG and Agentic AI Professional Certificate: Labs

My hands-on lab work from the [IBM RAG and Agentic AI Professional Certificate](https://www.coursera.org/professional-certificates/ibm-rag-and-agentic-ai) on Coursera. The program covers building generative AI applications with prompt engineering, LangChain, retrieval-augmented generation (RAG), vector databases, multimodal models, and AI agents (LangGraph, CrewAI, AG2, MCP).

Each course has its own folder with the lab notebooks and a short README on what I built and learned. Larger portfolio projects that build on this coursework live in separate repositories.

## Progress

| # | Course | Status | Labs |
|---|--------|--------|------|
| 1 | Develop Generative AI Applications: Get Started | 🟡 In progress (2 labs so far) | [Course 1 labs](course-01-develop-generative-ai-applications-get-started/) |
| 2–9 | … | ⚪ Not started | |
| 10 | RAG and Agentic AI Capstone Project | ⚪ Not started | |

## Highlights so far
- **Prompt engineering with IBM Granite:** zero-, one- and few-shot prompting, chain-of-thought and self-consistency, compared on real model outputs.
- **LangChain LCEL chains:** a product review analyzer that returns structured JSON (`prompt | llm | JsonOutputParser`), which removed the extra fields the model made up in free-text mode.
- **First RAG pipeline:** web page → chunks → Granite embeddings → Chroma → retriever → RetrievalQA, with a look at how chunking and embedding settings affect retrieval.
- **Memory and agents:** a chatbot with buffer and summary memory, and a ReAct agent with calculator and text-formatting tools (4/4 tasks solved).

## Tech stack
Python · LangChain (LCEL, chains, memory, agents) · IBM watsonx.ai · IBM Granite · Meta Llama 4 · Chroma · Jupyter

## Running the notebooks
The labs were run in IBM Skills Network's hosted JupyterLab, which provides watsonx.ai access without API keys.

To run a notebook locally:
1. Run its first **Install required libraries** cell. Each lab pins its own package versions there.
2. Create a watsonx.ai project and supply your own credentials through environment variables (never commit keys):

```bash
export WATSONX_APIKEY="your-key"
export WATSONX_PROJECT_ID="your-project-id"
```

## Credits
Lab material © IBM Skills Network, from the IBM RAG and Agentic AI Professional Certificate. Exercise solutions, extensions and write-ups are my own.
