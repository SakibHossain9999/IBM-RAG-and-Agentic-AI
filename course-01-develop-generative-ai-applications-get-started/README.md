# Course 1: Develop Generative AI Applications: Get Started

Building generative AI applications with IBM watsonx.ai, IBM Granite, LangChain, Flask and Gradio.

## Labs

| # | Lab | Notebook |
|---|-----|----------|
| 1 | Prompt Engineering and LangChain Prompt Templates | [01-foundations-of-generative-ai-and-prompt-engineering](01-foundations-of-generative-ai-and-prompt-engineering/In-Context%20Learning%20and%20Prompt%20Templates%20for%20Advanced%20AI.ipynb) |

---

## Lab 1: Prompt Engineering and LangChain Prompt Templates

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
