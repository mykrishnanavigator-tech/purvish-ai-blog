---
title: "Sales Update AI Assistant (Running on HuggingFace - Space)"
meta_title: "Sales Update AI Assistant on Hugging Face Spaces"
description: "A practical AI learning project that turns long sales update narratives into structured analysis, history lookup, and follow-up insight using Gradio on Hugging Face Spaces."
date: 2026-03-14T05:00:00Z
categories: ["My Learning"]
author: "Purvish Shah"
tags: ["ai-assistant", "huggingface", "gradio", "sales", "automation"]
draft: false
---

Sales leaders often receive **long narrative updates** from team members through email or chat. These updates contain useful information, but they are often inconsistent, difficult to compare week to week, and hard to track historically.

The **Sales Update AI Assistant** solves this problem by converting raw sales narratives into an interactive AI-powered workflow that supports structured updates, gap analysis, and historical retrieval.

This project powers a live application deployed on **Hugging Face Spaces** using **Gradio**.

## The Problem

Sales leaders frequently face challenges such as:

- Sales updates arriving as long unstructured emails
- Lack of consistency between reporting periods
- Difficulty identifying missing information
- No easy way to compare updates over time
- Manual effort required to track progress or follow-ups

Without structure, valuable insights can be lost.

## The Solution

The **Sales Update AI Assistant** transforms narrative updates into an AI-supported workflow.

The application allows users to:

1. Submit sales updates
2. Automatically analyze gaps between updates
3. Retrieve historical updates
4. Maintain a searchable internal knowledge base

Instead of static emails, the updates become part of an interactive AI assistant interface.

## Project Repository

[View the project on GitHub](https://github.com/purvishce/SalesUpdateAIAssistant)

## Key Features

### Guided Update Submission

Users select a salesperson and paste their update narrative into the interface.

The system stores the update in a **SQLite history database** and makes it available for analysis.

### AI Gap Analysis

The assistant compares the **latest update** with the **previous submission** to detect missing or unclear information.

Example insights include:

- Missing follow-up actions
- Pipeline progress not mentioned
- Clients referenced previously but not updated
- Lack of timeline updates

This helps managers quickly identify what information is missing.

### Historical Update Retrieval

Users can query past updates within a configurable date range.

Results are displayed as structured cards showing:

- Date of update
- Full narrative text
- Easy comparison across reporting periods

This helps leadership track progress over time.

### Clean Chat-Based Interface

The UI uses **Gradio Blocks** with custom CSS to create a polished experience.

Key elements include:

- Chat-style responses
- Structured analysis cards
- Clear workflow actions
- Interactive history lookup

## System Architecture

The application follows a simple but effective architecture.

```text
User Interface (Gradio)
        |
        v
Application Logic (app.py)
        |
        +-- Gap Analysis (summarizer.py)
        |
        +-- Database Operations (db.py)
        |
        v
SQLite Database (sales_updates.db)
```

## Screenshots

### Fresh Session

The chat board loads with the gradient theme, dropdown and date controls, and three action buttons before any submissions.

This view shows the initial greeting card, the composer for update text, and the default date ranges before an operator selects an action.

![Fresh session](https://github.com/purvishce/SalesUpdateAIAssistant/raw/main/Screenshot%202026-03-10%20205731.png)

### Gap Analysis Response

After submitting new copy, the assistant compares it to the previous update and returns a **Gap Analysis** card with executive-friendly sections.

The card surfaces the meta tag, missing items, and immediate actions without overwriting prior history in the chat.

![Gap analysis](https://github.com/purvishce/SalesUpdateAIAssistant/raw/main/Screenshot%202026-03-10%20205947.png)

### History Lookup

**View Previous** fetches prior notes and displays them as per-date sections so leadership can trace what was already communicated.

Each section retains the original paragraphs saved in SQLite, helping snapshot comparisons.

![History lookup](https://github.com/purvishce/SalesUpdateAIAssistant/raw/main/Screenshot%202026-03-10%20210047.png)

## Hosted Demo

The project is hosted on Hugging Face Spaces:

[Sales Update AI Assistant on Hugging Face Spaces](https://huggingface.co/spaces/purvishce/SalesUpdateAIAssistant)

The space is not publicly accessible at the moment.

## Next Steps

I will post another blog on the enterprise version of this idea. That version will involve Microsoft Teams, Azure Functions, Azure AI Foundry, and storing emails in a SharePoint library using Power Automate.
