---
title: "WiseHoots Space Explorer AI Agent"
meta_title: "WiseHoots Space Explorer AI Agent"
description: "How WiseHoots Space Explorer turns NASA and JPL data into clear, kid-friendly space stories using a small multi-agent newsroom workflow."
date: 2026-10-02T05:00:00Z
categories: ["AI Agents"]
author: "Purvish Shah"
tags: ["nasa", "openai", "ai-agent", "fastapi"]
draft: false
---

WiseHoots Space Explorer is a kid-friendly NASA news system. It takes real space data from trusted NASA and JPL sources and turns it into clear, engaging answers for young readers.

The idea is simple: a child asks a space question, and the system responds like a small newsroom. One editor agent coordinates the work, while specialist agents discover sources, check facts, write the explanation, and keep the final answer safe for kids.

<div class="my-8 overflow-hidden rounded-lg">
  <iframe
    class="aspect-video w-full"
    src="https://www.youtube.com/embed/JOARhNL_VCU"
    title="WiseHoots Space Explorer video"
    loading="lazy"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen>
  </iframe>
</div>

## Why I Built It

Space information is fascinating, but it is often spread across technical APIs, scientific terms, raw metadata, and measurements that are not written for children.

A simple request like "Give me a NASA story" actually requires several steps:

1. Find a trustworthy NASA or JPL source.
2. Choose a story that will interest young readers.
3. Check the facts, dates, measurements, and safety-related wording.
4. Explain the science in simple language.
5. Create quiz questions when needed.

WiseHoots Space Explorer wraps those steps into one clear workflow.

## The Goal

The goal is to complete the whole process with one API request:

```http
POST /nasa-newsroom
Content-Type: application/json
```

```json
{
  "message": "NASA Story"
}
```

The API returns a structured response that the chat UI can display as a kid-friendly answer, with source-backed details and optional quiz content.

## Architecture

![WiseHoots Space Explorer architecture](/images/space-explorer-ai-agent.png)

The flow has three main layers:

1. The chat UI collects a space question from the user.
2. FastAPI receives the request at `/nasa-newsroom`.
3. The editor agent coordinates guardrails, discovery, fact-checking, writing, quizzes, and shared NASA/JPL tools.

## How the System Works

### Editor Agent

The main agent, **NASA Space Newsroom**, manages the workflow. It decides which specialist agents to call and combines their work into one final response.

### Input Guardrail

Before the system starts researching, it checks that the request is actually about NASA, space, astronomy, planets, asteroids, spacecraft, or space science. Unrelated requests are rejected early.

### Discovery Scout

The Discovery Scout finds possible story ideas from trusted sources such as:

- NASA Astronomy Picture of the Day (APOD)
- NASA Image and Video Library
- NASA Near-Earth Object Web Service (NeoWs)

### Science Fact-Checker

The Fact-Checker verifies the selected story against NASA and JPL information. It checks:

- Title and publication date
- Source reliability
- Measurements and scientific details
- Unsupported claims
- Asteroid-risk wording
- Confidence level

### Young Explorer Writer

The Writer turns verified facts into a friendly explanation for a 9-year-old reader. It uses simple language and relatable comparisons without inventing unsupported details.

### Space Quiz Agent

When requested, the Quiz Agent creates two multiple-choice questions and one imaginative question based on the final story.

### Output Guardrail

Before the response goes back to the chat UI, the Output Guardrail checks that the content is safe, appropriate, and easy for young readers to understand.

## Technical Flow

The request enters a FastAPI application. A Pydantic model checks that the message is present and not empty. The API then runs the newsroom agent and returns structured JSON.

The API also handles common error cases:

- Invalid or empty requests
- Out-of-scope questions
- Fact-checking or safety failures
- Timeouts
- Unexpected internal errors

## Why This Architecture Works

This project uses an **agent-as-tool** pattern. The editor agent stays in control, while specialist agents handle focused tasks.

That separation makes the system:

- Easier to understand
- Easier to test and maintain
- More reliable for fact-checking
- Better suited to age-appropriate writing
- Easier to extend with new capabilities

## Summary

WiseHoots Space Explorer turns real NASA and JPL information into educational stories for children. The multi-agent workflow discovers interesting science, verifies the facts, explains them clearly, and can add quiz questions for learning.

The result is a simple newsroom-style system that combines trusted data sources, focused AI agents, and safety checks into one kid-friendly space explorer.
