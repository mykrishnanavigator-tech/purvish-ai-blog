---
title: "NASA APOD Explorer + AI Narrator (Gradio App with OpenAI)"
meta_title: "NASA APOD Explorer + AI Narrator (Gradio App with OpenAI)"
description: "What I learned building a lightweight Gradio app that fetches NASA's Astronomy Picture of the Day and uses OpenAI to generate human-friendly narration."
date: 2026-09-10T05:00:00Z
categories: ["My Learning"]
author: "Purvish Shah"
tags: ["nasa", "apod", "openai", "gradio", "ai-narrator"]
draft: false
---

A lightweight Gradio app that fetches NASA's Astronomy Picture of the Day (APOD) and generates a concise, human-friendly narration using OpenAI. It supports HD images, date selection, graceful handling of videos, and clear error messages.

**Big thanks** to NASA for providing free access to their API.

## What I Learned

I learned how to build a simple interactive UI using **Gradio** and connect it to Python functions. I also learned how to call external APIs, including NASA APOD and OpenAI, then combine their outputs to generate image explanations.

This project also helped me structure prompts and use the **OpenAI chat completion API** with system and user messages.

Project repository: [AstronomyPictureExplorer on GitHub](https://github.com/purvishce/AstronomyPictureExplorer)

## `AstronomyPictureExplorer.py`

The app uses NASA's **APOD (Astronomy Picture of the Day)** API to fetch the daily astronomy image. The `get_nasa_apod()` function retrieves the title, image URL, and explanation.

Next, the `analyze_statement()` function sends the image URL to OpenAI.

It uses the following prompt:

```text
The following image is from NASA's Astronomy Picture of the Day.
Image URL: {image_url}
Create an explanation of the image in a way that is easy to understand and engaging.
```

The OpenAI call uses:

```python
openai.chat.completions.create(
    model="gpt-4o-mini",
    messages=[
        {"role": "system", "content": sytesmprompt},
        {"role": "user", "content": prompt},
    ],
)
```

This format, using system and user messages, is now the **standard way** to call OpenAI chat models.

Many other chat-focused LLM APIs, including Anthropic's Claude and Google's Gemini, follow a similar role and message structure.

For the UI, **Gradio** makes things very simple.

You provide:

- The function name, `app`
- The inputs array, including date and HD checkbox
- The outputs array, including title, image, and explanation

Gradio automatically builds the UI, passes values into the function, and displays whatever the function returns. It is a great library for fast prototypes and POCs, and I will continue using it for future learning projects.
