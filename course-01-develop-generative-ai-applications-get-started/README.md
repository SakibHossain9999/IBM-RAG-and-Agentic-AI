# Course 1: Develop Generative AI Applications: Get Started

Building generative AI applications with IBM watsonx.ai, IBM Granite, LangChain, Flask and Gradio.

## Labs

| # | Lab | Notebook |
|---|-----|----------|
| 1 | Master Prompt Engineering and LangChain PromptTemplates | [01-foundations-of-generative-ai-and-prompt-engineering](01-foundations-of-generative-ai-and-prompt-engineering/In-Context%20Learning%20and%20Prompt%20Templates%20for%20Advanced%20AI.ipynb) |
| 2 | Build Smarter AI Apps: Empower LLMs with LangChain | [02-introduction-to-langchain-in-genai-applications](02-introduction-to-langchain-in-genai-applications/Build%20Smarter%20AI%20Apps%20Empower%20LLMs%20with%20LangChain.ipynb) |

---

## Lab 1: Master Prompt Engineering and LangChain PromptTemplates

Prompt experiments with IBM Granite (`ibm/granite-4-h-small`) on watsonx.ai, followed by reusable LangChain LCEL chains for common LLM tasks.

### What I did
- **Basic prompts:** open-ended sentence completion with no instructions.
- **Zero-shot:** movie review sentiment, paragraph summarization, English→Spanish translation.
- **One-shot:** a formal email to a university admissions office, a plain-language explanation of machine learning, and keyword extraction, each guided by a single example I wrote.
- **Few-shot, chain-of-thought and self-consistency:** emotion classification, step-by-step reasoning for a decision problem and a process explanation, and cross-checking several answers to the same problem.
- **LangChain `PromptTemplate` + LCEL chains** (`prompt | llm | parser`) for summarization, question answering, text classification, SQL generation and an interactive role-play chat.

### Highlight: product review analyzer
An LCEL chain that takes a raw review and returns its sentiment, the product features mentioned and a one-sentence summary. I built two versions:

```python
text_chain = RunnableLambda(format_review_prompt) | llm | StrOutputParser()
json_chain = RunnableLambda(format_json_prompt)   | llm | JsonOutputParser()
```

- **Free-text version:** the analysis was correct, but the model also made up fields I never asked for ("Suggestions for Improvement", "Suggested Response").
- **JSON version:** returned exactly `sentiment`, `features` and `summary` as a Python dict that downstream code can use directly, with error handling for the occasional malformed response.

### What I observed
- **Without instructions, a prompt can go anywhere.** "The wind is" turned into an airplane-velocity physics problem.
- **The wording sets the output style.** "Once upon a time…" produced a story, while "The benefits of … include" produced a list.
- **Models don't always follow format instructions.** Asked for one word, the model answered "Negative" plus an explanation. Shown a comma-separated keyword example, it returned a numbered list.
- **Structured output (JSON + parser) is more reliable than free-text instructions** when results feed into other code.

### Skills
Prompt engineering · in-context learning · LangChain `PromptTemplate` · LCEL · output parsers · IBM watsonx.ai

---

## Lab 2: Build Smarter AI Apps: Empower LLMs with LangChain

A tour of LangChain's core building blocks on watsonx.ai (IBM Granite and Meta Llama 4 Maverick): models, prompt templates, output parsers, document loaders, text splitters, embeddings, vector stores, retrievers, memory, chains and agents.

### What I did
1. **Model and temperature comparison:** sent creative, factual and instruction prompts to Granite and Llama at temperature 0.8 and 0.1, running each twice to measure run-to-run variation.
2. **JSON output parser:** `prompt | llm | JsonOutputParser()` returning movie info as a Python `dict` (title, director, year as an `int`, genre) for four movies.
3. **Document loaders and text splitters:** loaded a research paper (PDF) and a web page, then compared `CharacterTextSplitter` (300/30) with `RecursiveCharacterTextSplitter` (500/50) and checked that metadata carries over to every chunk.
4. **Retrieval system:** web page → chunks → Granite embeddings (`granite-embedding-278m-multilingual`) → Chroma vector store → retriever → `RetrievalQA` answers to three questions.
5. **Chatbot with memory:** `ConversationChain` with `ConversationBufferMemory`, plus `ConversationSummaryMemory` for comparison.
6. **Multi-step chains:** a three-step review pipeline (sentiment → key points → customer reply), built twice: legacy `LLMChain` + `SequentialChain`, and LCEL with `RunnablePassthrough.assign()`.
7. **ReAct agent:** a calculator tool and a text-formatting tool, used by an agent built with `create_react_agent` and `AgentExecutor`.

### Results
| Experiment | Result |
|---|---|
| Splitters on the 6-page PDF | Character 300/30: **95 chunks**, avg 266 chars · Recursive 500/50: **57 chunks**, avg 453 chars |
| Metadata preservation | All 13 chunks from page 2 kept identical `source` and `page` metadata |
| JSON parser | All 4 movies parsed into a `dict` with the correct keys, `year` as an `int` |
| Agent | 4/4 tasks solved in one tool call each (88, HELLO WORLD, 105, Langchain Is Awesome) |

### What I observed
- **Completion vs. chat wrappers matter.** `WatsonxLLM` sends raw text, so the models often continued the prompt instead of answering: Granite invented extra instructions ("The poem should have 5 stanzas…"), and Llama wrote like a web page ("- GeeksforGeeks", "| by Saba | Medium").
- **Memory stores whatever the model writes, including made-up turns.** In the memory exercise, the model wrote fake follow-up turns such as "Human: I like light blue." inside its own reply. These were saved to memory, and the summary memory later "remembered" details Alice never said (the Rocky Mountains, Longs Peak). Hallucinations can end up in memory and get repeated as fact.
- **Agents need the model to follow the format exactly.** With `ChatWatsonx`, the model ignored the stop signal at "Observation", invented its own observations and broke every calculation. With `WatsonxLLM`, which respects the stop sequence, the same agent solved all 4 tasks.
- **Higher temperature means more variety and more risk.** At 0.8, Granite made up a citation ("Smith et al., 2022"). Low temperature (0.1) was better for factual and instruction-following prompts, and even then the two runs were not always identical.
- **Recursive splitting respects its size limits.** Max chunk sizes stayed within limits (299 of 300, 498 of 500), and fewer, larger chunks keep more context in each one.
- **RAG is only as good as its data.** The LangChain docs URL now redirects to a new site, so several retrieved chunks were navigation menu text. Cleaning the source matters as much as the retrieval code.
- **An embedding setting can quietly break retrieval.** The lab's default `TRUNCATE_INPUT_TOKENS: 3` embeds only the first few words of each chunk, so I raised it to 512.
- **LCEL vs. legacy chains:** both gave equivalent results. LCEL is shorter, composable and supports streaming. `LLMChain` and `SequentialChain` are more explicit but deprecated.

### Skills
LangChain · watsonx.ai · IBM Granite · Llama 4 · output parsers · document loaders · text splitters · embeddings · Chroma · retrievers · RetrievalQA · conversation memory · LCEL · ReAct agents · tool calling
