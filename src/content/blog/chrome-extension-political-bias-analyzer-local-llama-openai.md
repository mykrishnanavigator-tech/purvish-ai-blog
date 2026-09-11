---
title: "Chrome Extension: Political Bias Analyzer (Local LLAMA + OpenAI)"
meta_title: "Chrome Extension: Political Bias Analyzer (Local LLAMA + OpenAI)"
description: "What I learned building a Chrome extension that extracts article content, analyzes political bias with either a local LLAMA API or OpenAI, and visualizes left-right leaning percentages."
date: 2026-09-10T05:00:00Z
categories: ["My Learning"]
author: "Purvish Shah"
tags: ["chrome-extension", "llama", "openai", "political-bias", "visualization"]
draft: false
---

A Chrome extension that analyzes political bias in news articles and web content by extracting article content and providing a visual breakdown of left vs. right political leaning percentages. The extension can leverage either a local LLAMA API or OpenAI's API for bias analysis.

## What I Learned

This was a fun project. I built a Chrome extension that reads web page content and integrates with LLM APIs and OpenAI APIs for real-time analysis. I learned to parse AI outputs and visualize data with interactive charts.

## Project Repositories

- [OpenAI edition](https://github.com/purvishce/chromeextension.Ideologicallabeling.OpenAI)
- [LLAMA edition](https://github.com/purvishce/chromeextension.Ideologicallabeling.LLAMA)

## Project Folder Structure

```text
chromeextension.Ideologicallabeling/
+-- manifest.json    # Extension configuration
+-- popup.js         # Main popup interface logic
+-- hello.html       # Extension popup UI
+-- content.js       # Content script for article extraction
+-- background.js    # Background service worker
+-- README.md
```

## LLAMA Edition

The LLAMA edition uses a local LLAMA API for bias analysis, allowing the extension to run against a locally hosted model instead of relying on a hosted LLM provider.

## OpenAI Edition

The OpenAI edition uses OpenAI's API for real-time article analysis and response generation. The extension extracts article content from the page, sends it for analysis, parses the model response, and renders a visual left vs. right leaning breakdown in the popup UI.
