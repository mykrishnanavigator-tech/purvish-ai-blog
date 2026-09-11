---
title: "RAG for Tabular Datasets"
meta_title: "RAG for Tabular Datasets"
description: "What I learned building a Retrieval-Augmented Generation workflow over a structured Udemy courses dataset using chunking, embeddings, Chroma, evaluation, retrieval, and Gradio."
date: 2026-01-11T05:00:00Z
categories: ["My Learning"]
author: "Purvish Shah"
tags: ["rag", "tabular-data", "chroma", "gradio", "embeddings"]
draft: false
---

## What I Learned

My goal for this project was to deeply understand **Retrieval-Augmented Generation (RAG)** using a **tabular dataset**, moving beyond unstructured text use cases.

I worked with a real-world **Udemy Courses dataset in CSV format** sourced from Kaggle. The dataset provided rich structured fields such as course titles, descriptions, ratings, instructors, and pricing.

Dataset: [Udemy Courses on Kaggle](https://www.kaggle.com/datasets/andrewmvd/udemy-courses)

Project repository: [CourseLookup on GitHub](https://github.com/purvishce/CourseLookup)

## Step 1: Data Ingestion to Chunking

Chunking is **more than just splitting text**. It is how you organize knowledge for efficient and accurate retrieval.

### `create_chunks` Function

This function takes a course record and transforms it into **searchable chunks** with metadata and keywords, ready for tasks like indexing in a vector database or powering a recommendation system.

1. **Metadata extraction:** It first builds metadata about the course, such as ID, category, or level, using `build_metadata(course)`.
2. **Keyword generation:** A helper function, `tokens_from`, extracts unique and meaningful words from the course title, instructor, and description. It ignores short words and duplicates, up to a limit of 50. These become tags that help in searching or filtering.
3. **Chunk creation:** It combines all course details into a single text block: title, instructor, level, rating, duration, lectures, and description. This becomes the main chunk of content.
4. **Final output:** The function returns a list of chunks. Each chunk is a dictionary containing `"text"` for the combined course information and `"metadata"` for original metadata, chunk type, and search tags.

In short, it turns a course into a structured, searchable snippet with tags, making it ready for AI-driven search, recommendations, or analytics.

## Step 2: Data Ingestion to Embeddings and Chroma

This code takes the previously created course chunks and turns them into embeddings for **semantic search or AI retrieval**.

### Prepare Texts for Embedding

```python
texts = [chunk["text"] for chunk in chunks]
```

This extracts the main text from each chunk. The print statements show progress and total count.

### Batch Embeddings to Stay Under Token Limits

Large datasets can exceed model limits, so the text is split into batches.

```python
batch_size = 1000

for i in range(0, len(texts), batch_size):
    batch = texts[i:i + batch_size]
    emb = openai.embeddings.create(
        model=embedding_model,
        input=batch,
    ).data
    vectors.extend([e.embedding for e in emb])
```

Each batch is sent to the embedding model, and only the numeric embeddings are stored in `vectors`.

At the end of this step, you have a list of embeddings ready to insert into Chroma, enabling fast similarity search and retrieval for the course dataset.

## Step 3: RAG Evaluator

When building a **Retrieval-Augmented Generation (RAG)** system, it is not enough for it to retrieve documents and generate answers. You need a structured way to measure performance, both for retrieval and for the quality of generated answers.

That is what the combination of **`eval.py`**, **`evaluator.py`**, and **`tests.jsonl`** provides.

### What Is `tests.jsonl`?

`tests.jsonl` is a structured test dataset that defines realistic questions and expected answers. Each line is a JSON object.

```json
{
  "question": "Who won the IIOTY award in 2023?",
  "keywords": ["Maxine", "Thompson", "IIOTY"],
  "category": "Awards",
  "reference_answer": "Maxine Thompson won the Insurellm Innovator of the Year (IIOTY) award in 2023."
}
```

- **question:** The input to test the RAG system.
- **keywords:** Key terms that should appear in the retrieved documents.
- **category:** Groups tests for reporting purposes.
- **reference_answer:** Ground truth answer for evaluating the generated response.

> JSONL format is memory-efficient and ideal for iterating over large test sets.

### What Is `eval.py`?

`eval.py` is an evaluation script that can run in CLI mode or as part of a dashboard. Its job is to measure retrieval and answer quality.

It performs two main tasks: retrieval evaluation and answer evaluation.

### Retrieval Evaluation

Retrieval evaluation checks how well the system retrieves relevant documents from the vector database.

Metrics include:

- **MRR (Mean Reciprocal Rank):** Measures how quickly the correct document appears.
- **nDCG (Normalized Discounted Cumulative Gain):** Measures relevance of the top-k documents.
- **Keyword Coverage:** Measures the percentage of expected keywords found.

The script also logs diagnostics to track missing keywords or top retrieved documents.

### Answer Evaluation

Answer evaluation uses the LLM as a judge to evaluate generated answers against the reference answer.

It scores each answer on three dimensions:

- **Accuracy (1-5):** How factually correct the answer is.
- **Completeness (1-5):** How fully it covers the reference answer.
- **Relevance (1-5):** How well it directly addresses the question.

The evaluator provides textual feedback alongside the numeric scores.

### How It Works

1. **Load tests:** Reads `tests.jsonl` into `TestQuestion` objects.
2. **Evaluate retrieval:** Fetches top documents using `fetch_context`, then calculates MRR, nDCG, and keyword coverage.
3. **Evaluate answers:** Generates answers using `answer_question`, then evaluates them with the LLM-as-a-judge.
4. **Report results:** CLI mode prints detailed metrics and feedback for each test. Dashboard mode, using `evaluator.py`, integrates with Gradio to visualize metrics and category-level charts.

```text
tests.jsonl -> fetch_context -> RAG system -> answer generation -> LLM judgment -> metrics and feedback
```

## Step 4: RAG Retriever

### 1. Loading Environment Variables

```python
from dotenv import load_dotenv

load_dotenv(override=True)
```

Before starting, the application loads API keys and configuration from the `.env` file. This includes:

- OpenAI API key for embeddings and LLM access
- Chroma DB directory for storing course vectors

> Why this matters in RAG: the vector database and LLM need credentials to function. Loading them securely keeps the system safe and configurable.

### 2. Setting Up Models and Vector Database

```python
MODEL = "gpt-4.1-nano"
DB_NAME = "vector_db"
collection_name = "customerlookup_emails"

embeddings = OpenAIEmbeddings(model="text-embedding-3-large")

vectorstore = Chroma(
    persist_directory=DB_NAME,
    embedding_function=embeddings,
    collection_name=collection_name,
)
```

Here we define:

- **LLM (`gpt-4.1-nano`):** The generative engine that produces answers.
- **Embeddings (`text-embedding-3-large`):** Converts course text into vectors for semantic search.
- **Chroma vectorstore:** Stores vectorized course data and retrieves the most relevant information.

> RAG principle:
>
> **Retrieval -> LLM -> Answer**
>
> The LLM only generates answers from retrieved context, not from its own knowledge.

### 3. Crafting the System Prompt

```python
SYSTEM_PROMPT_TEMPLATE = """
You are a professional Course Advisor Assistant.
...
Context:
{context}
"""
```

The system prompt tells the LLM how to behave. Key points:

- Answer strictly using retrieved course information.
- Summarize multiple courses clearly.
- Maintain a professional and educational tone.
- Avoid hallucinations, and never invent courses or instructors.

> In RAG, this prompt ensures generation is grounded in retrieved knowledge.

### 4. Extracting Metadata Filters from Queries

```python
def extract_filters_from_query(query: str):
    ...
```

The retriever parses user queries to detect:

- **Instructor**, such as "by John Doe"
- **Rating**, such as "4-star courses"
- **Level**, such as "Beginner" or "Advanced"

> RAG benefit: filtering the retrieval step improves precision by giving the LLM only the most relevant courses.

### 5. Retrieving Courses

```python
def retrieve_courses(query: str, top_k=15):
    ...
```

This function:

1. Extracts filters from the query.
2. Retrieves the top-k relevant course chunks from Chroma.
3. Returns a list of documents for the LLM to use.

> RAG analogy: think of this as a smart search engine feeding the LLM with exactly the context it needs.

### 6. Generating Answers

```python
def answer_question(question: str, history=[]):
    docs = retrieve_courses(question)
    ...
    response = llm.invoke([
        SystemMessage(content=system_prompt),
        HumanMessage(content=question),
    ])
```

The answer pipeline follows four steps:

1. Retrieve relevant course documents.
2. Combine them into a single context string.
3. Feed the context and user question to the LLM.
4. Return a professional, context-aware response.

> Key RAG principle: the LLM never guesses. It only summarizes retrieved knowledge.

### 7. User Interface with Gradio

```python
gr.ChatInterface(answer_question).launch()
```

Gradio provides a ready-to-use chat interface so users can ask questions and get answers in real time.

- Input: user query
- Output: LLM-generated answer based on retrieved context

This completes the RAG loop: retrieval, generation, and user interaction.
