---
title: "From AI Anxiety to Shipping My First iOS App"
meta_title: ""
description: "How My Krishna began as a response to AI anxiety and became an MVP built with Next.js, Supabase, Vercel, and Capacitor."
date: 2026-06-08T05:00:00Z
banner: true
hide_tags: true
categories: ["My Krishna"]
author: "Purvish Shah"
draft: false
---

*Part 1 of a series documenting the journey of building an AI-powered personal growth app inspired by Hindu philosophy.*

Over the last few years, AI has changed how we work. Ideas that once needed a team can now be prototyped by one person. Tasks that took days can often be completed in hours. The pace is exciting, but it can also create uncertainty.

I found myself asking the same questions many people are asking:

- How do I stay relevant?
- How do I adapt to constant change?
- How do I deal with anxiety about the future?
- How do I keep growing when everything is moving so quickly?

Whenever I faced questions like these, I often turned to Hindu philosophy, especially teachings from the Bhagavad Gita and the Upanishads. These teachings have helped people navigate uncertainty for thousands of years.

That led to a simple idea: what if I could combine AI with timeless wisdom to help people work through life's challenges?

That idea became the foundation for My Krishna.

## Learning AI by Building

Before building the app, I spent time exploring AI development through small experiments:

- AI chat applications
- Retrieval-Augmented Generation
- Vector databases
- Prompt engineering
- AI-powered proofs of concept

Those experiments helped me see an important distinction. AI can generate answers, but many people are looking for guidance. Not generic advice. Not motivational quotes. Guidance grounded in principles that have stood the test of time.

## Defining the MVP

I wanted My Krishna to help users reflect, journal, explore wisdom by topic, receive personalized insights, and track personal growth over time.

Instead of trying to build everything at once, I focused on the smallest version that could deliver value.

The MVP centered on five ideas:

1. Daily emotional journaling for thoughts, feelings, challenges, and reflections.
2. Wisdom organized by topics like anxiety, relationships, discipline, purpose, karma, anger, and self growth.
3. AI-powered personalization based on conversations, journal entries, and emotional patterns.
4. A journal timeline so users can revisit previous questions, lessons, and reflections.
5. A simple profile dashboard showing activity, topics explored, saved wisdom, and reflection progress.

The goal was not to overbuild. The goal was to validate one question: would people find value in combining AI conversations with timeless philosophical wisdom?

## Choosing the Stack

For an MVP, speed matters. I chose tools that helped me move quickly while keeping future options open.

**Next.js** gave me a familiar React-based development experience and made it easier to focus on the product instead of learning a completely new framework.

**Supabase** became the backbone of the app. It provided PostgreSQL, authentication, storage, Row-Level Security, and a path toward future vector search. Using PostgreSQL also kept the data model portable.

**Vercel** handled deployment and API hosting. Connecting the repository to Vercel gave me automatic deployments, preview environments, and fast mobile testing.

**Capacitor** allowed me to wrap the web application as an iOS app, reuse the UI, and move much faster than building a fully native iOS app from day one.

## What I Deliberately Did Not Build

One of the biggest lessons was that every feature adds complexity. I intentionally postponed:

- Full RAG implementation
- Push notifications
- Native iOS architecture
- Advanced analytics
- Recommendation engine
- Subscription management
- Multi-platform support

AI has lowered the barrier to creating software, but product decisions still matter. Technology can help build faster. It cannot decide what is worth building.

That responsibility still belongs to the builder.

##
