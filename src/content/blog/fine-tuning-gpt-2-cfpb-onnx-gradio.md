---
title: "Fine-Tuning GPT-2 on CFPB Dataset with ONNX and Gradio"
meta_title: "Fine-Tuning GPT-2 on CFPB Dataset with ONNX and Gradio"
description: "What I learned fine-tuning GPT-2 on the CFPB consumer complaints dataset, exporting the model to ONNX, quantizing it, and serving it through a Gradio app."
date: 2026-09-10T05:00:00Z
categories: ["My Learning"]
author: "Purvish Shah"
tags: ["fine-tuning", "gpt-2", "onnx", "gradio", "nlp"]
draft: false
---

## What I Learned

1. **Work with real-world datasets:** Cleaning and preparing the CFPB dataset for model training.
   Dataset: [CFPB Consumer Finance Complaints](https://huggingface.co/datasets/CFPB/consumer-finance-complaints)
2. **Fine-tune GPT-2 models:** Adapting a pre-trained language model to a specific domain.
3. **Export and optimize models:** Converting GPT-2 to ONNX format and applying quantization for faster and more efficient inference.
4. **Build interactive AI applications:** Creating a user-friendly Gradio interface to generate synthetic text on demand.
5. **Integrate AI workflows:** Connecting dataset processing, model training, optimization, and deployment into a seamless pipeline.

This project strengthened my understanding of NLP, model optimization, and deploying AI models for practical, real-world applications.

Project repository: [CFPBSyntheticData on GitHub](https://github.com/purvishce/CFPBSyntheticData)

## Project Folder Structure

```text
project-root/
+-- data/
|   +-- cfpb_complaints.csv          # Raw dataset
|   +-- dataset_loader.py            # CSV chunked preprocessing script
|   +-- preprocess.py                # Cleaning and tokenization helpers
|
+-- models/
|   +-- train.py                     # Fine-tune GPT-2 model
|   +-- dataset_loader.py            # ComplaintDataset torch Dataset class
|   +-- export_onnx.py               # ONNX export, torch-based
|   +-- export_gpt2_onnx_simple.py   # Simple Optimum-based exporter
|   +-- quantize.py                  # ONNX quantization script
|   +-- output_gpt2_fast/            # Trained weights and ONNX files
|
+-- gradio_app/
|   +-- app.py                       # Gradio demo using quantized ONNX model
|
+-- utils/
|   +-- config.py                    # Configuration values, paths, defaults
|   +-- tokenizer_utils.py           # GPT-2 tokenizer helper
|
+-- venv/                            # Virtual environment, optional
```

## Step 1: Data Cleaning and Preprocessing

First, I prepared the [CFPB dataset](https://huggingface.co/datasets/CFPB/consumer-finance-complaints) using a custom `preprocess_dataset` function to clean the data.

Key preprocessing steps:

- **Masking sensitive information:** Replaced phone numbers and emails.
- **Filtering irrelevant entries:** Removed short or non-informative complaints.
- **Removing duplicates:** Dropped duplicate rows in the **Consumer complaint narrative** column.

**Important:** Use `random_state=42` to ensure consistent training data across runs.

## Step 2: Dataset Loader

The **12 million record** dataset is processed in **50,000-row batches**. Each batch is cleaned and saved, then duplicates are removed and text is tokenized for the model.

Process overview:

- **Load in batches:** Dataset divided into 50,000-row chunks, cleaned, and saved.
- **Combine and remove duplicates:** Batches merged, duplicates dropped, and sample selected.
- **Save clean data:** Final dataset saved for training.
- **Tokenization for GPT-2:** Complaints tokenized and padded to a standard length using the GPT-2 pretrained model tokenizer.
- **Attention masks and labels:** An attention mask indicates which tokens are real versus padding, and labels are set to the same token IDs so GPT-2 can learn to predict the next token in the sequence.

```yaml
Text: My loan was denied due to low credit score .
Tokens:
  - My
  - loan
  - was
  - denied
  - due
  - to
  - low
  - credit
  - score
  - EOS
Token IDs: [72, 1410, 366, 1590, 284, 466, 151, 2197, 1132, 50256]
Attention: [1, 1, 1, 1, 1, 1, 1, 1, 1, 1]
Labels: [72, 1410, 366, 1590, 284, 466, 151, 2197, 1132, 50256]

Each input token predicts the next token in the labels.
```

## Step 3: Train, Export to ONNX, and Quantize

In this stage, the workflow fine-tunes a pretrained GPT-2 model on the cleaned dataset, converts the trained model to an optimized ONNX format, and applies quantization to make inference faster and lighter for deployment.

What happens in this step:

- Load the **GPT-2 pretrained model** from Hugging Face, with no API key needed.
- Download the model once and cache it locally for future runs.
- Fine-tune GPT-2 using the tokenized training dataset.
- Export the trained model to **ONNX format** for performance-optimized inference.
- Apply **dynamic quantization** to reduce model size and improve CPU inference speed.

## Step 4: Running GPT-2 Inference in Gradio Using an ONNX Model

- **Load the quantized ONNX model:** The model is loaded into an `InferenceSession`, which acts like the engine that runs the AI locally.
- **Initialize a local tokenizer:** The tokenizer converts prompt text into numerical token IDs, called `input_ids`, and creates an `attention_mask` so the model knows which parts of the input to focus on.
- **Run inference using ONNX Runtime:** The session takes the tokenized input and predicts the next tokens using the optimized quantized model.
- **Decode the output back to text:** The tokenizer's `decode()` method transforms the predicted token IDs into human-readable text.

## Why the Output Is Gibberish

- I reduced my dataset from **100,000 to 5,000** samples so I could fine-tune it on my PC. That is too small for GPT-2 to learn meaningful patterns.
- I shortened **max_length from 256 to 128**, so the model sees less context.
- Together, a small dataset and short sequences make the model generate incoherent or repetitive text.

**Bottom line:** Too little training data and too-short sequences lead to poor-quality output.
