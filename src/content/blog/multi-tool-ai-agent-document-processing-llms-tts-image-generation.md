---
title: "Multi-Tool AI Agent - Document Processing with LLMs, TTS & Image Generation"
meta_title: "Multi-Tool AI Agent - Document Processing with LLMs, TTS & Image Generation"
description: "What I learned building an agentic document-processing workflow that uses LLM planning, OCR, text-to-speech, image generation, SQLite, and a Gradio interface."
date: 2026-09-10T05:00:00Z
categories: ["My Learning"]
author: "Purvish Shah"
draft: false
---

An intelligent, multi-tool AI agent that automatically processes documents using LLMs, TTS, and image generation, all orchestrated through a SQLite database and a Gradio web interface.

## What I Learned

This project taught me how a real **agentic workflow** operates behind the scenes. I learned how the agent reads the document's current state from the database, uses an LLM to decide the next required action, and automatically triggers the right tool: summarization, text-to-speech, or image generation. The workflow runs in a loop until all steps are completed, without any hardcoded sequence.

Seeing how the LLM plans, executes, and re-plans each step gave me a clear understanding of how modern agentic systems coordinate multiple AI capabilities and operate autonomously. It is a powerful, reusable pattern for any multi-step AI pipeline.

Project repository: [doc-agent on GitHub](https://github.com/purvishce/doc-agent)

## Project Folder Structure

```text
doc-agent/
|
+-- src/
|   +-- main.py             # Entry point for tests and manual runs
|   +-- ui.py               # Gradio UI for interactive usage
|   +-- database.py         # SQLite DB operations
|   +-- agent_planner.py    # Core AI agent logic and workflow
|   +-- tts_service.py      # Optional TTS service helper
|   +-- models/             # Optional Python models for structured data
|
+-- data/
|   +-- doc_agent.db        # SQLite database
|   +-- uploads/            # Uploaded documents
|
+-- output/
|   +-- audio/              # Generated MP3 files
|   +-- images/             # Generated images
|
+-- database_migration.py   # Helper script to add DB columns
+-- .env                    # OpenAI API key configuration
+-- README.md
```

## Step 1: Supported Class Files: `Database` and `OCRService`

This project includes two core components:

1. **A `Database` class** that manages CRUD operations using the SQLite library.
2. **An `OCRService` class** that extracts text from PDF documents and images using PyMuPDF and Tesseract.

## Step 2: Agent Planner Class and Gradio Input Workflow

In this step, we introduce the **AgentPlanner**, the central component that coordinates every AI action in the document-processing workflow. When the class is initialized, its constructor loads the OpenAI API key and sets up the core services:

- The **Database** class for storing document states, summaries, paths, and related metadata
- The **OCRService** used to extract text when needed
- The mapping of workflow tools:
  - `summarize_document()`
  - `text_to_speech()`
  - `generate_image_from_doc()`

These components allow the agent to process a document intelligently, step by step.

```python
self.tools = {
    "summarize": self.summarize_document,
    "tts": self.text_to_speech,
    "generate_image": self.generate_image_from_doc,
}
```

When I upload a document through the Gradio interface and click **Process Document**, the backend executes the following sequence, exactly as seen in my `process_document()` function:

1. The uploaded file is copied into the local `data/uploads` folder.
2. OCR is executed immediately to extract text.
3. The extracted text is stored in the database when inserting the new document record.
4. The status is updated to `"text_extracted"`.

Next, the workflow begins:

```python
for _ in planner.run_agentic_workflow(doc_id):
    pass
```

This line **triggers the agentic workflow loop**, where the agent repeatedly:

- Reads the document's current state from the database
- Sends the state to `plan_next_step_agentic()`
- Receives the next required action from the LLM
- Performs the correct operation: summarize, TTS, generate image, or complete

Depending on what fields are missing, such as `summary`, `tts_path`, or `image_path`, the planner may choose:

- `extract_text`
- `summarize`
- `tts`
- `generate_image`
- `complete`

## Final Output

The final result is a working Gradio application where the user uploads a document, starts the process, and the agent completes the document workflow by coordinating OCR, summarization, text-to-speech, and image generation.
