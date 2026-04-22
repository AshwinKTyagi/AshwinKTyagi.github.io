---
title: "Chat Optimizer"
summary: "A Next.js TypeScript chatbot that classifies user intent using vector embeddings and Small Language Models (SLMs), with graceful fallbacks for each approach."
date: 2025-04-01T00:00:00-00:00
aliases: ["/chatoptimizer"]
tags: ["Projects", "Chat Optimizer"]
author: "Me"
showToc: true
TocOpen: false
draft: false
math: false
hidemeta: true
comments: false
description: "Duration: April 2025 - Current"
canonicalURL: "https://canonical.url/to/Projects/chatoptimizer"
disableHLJS: false
disableShare: false
hideSummary: false
searchHidden: true
ShowReadingTime: false
ShowBreadCrumbs: false
ShowPostNavLinks: false
ShowWordCount: false
ShowRssButtonInSectionTermList: false
UseHugoToc: true
cover:
    image: "<image path/url>"
    alt: "<alt text>"
    caption: "<text>"
    relative: false
    hidden: true
editPost:
    URL: "https://github.com/AshwinKTyagi/AshwinKTyagi.github.io/tree/main/content"
    Text: "Suggest Changes"
    appendFilePath: true
---

### [Link to GitHub](https://github.com/AshwinKTyagi/chat-optimizer)

## Project Description

Chat Optimizer is a Next.js TypeScript chatbot application that explores two different approaches to user intent classification: vector embeddings and Small Language Models (SLMs). The goal of this project is to compare these strategies in terms of accuracy, performance, and reliability — and to build a system that degrades gracefully when external services are unavailable.

## Tech Stack

**Frontend & Routing**
- Next.js 13+ with TypeScript

**Intent Classification**
- Vector Embeddings via `nomic-embed-text` (with OpenAI API fallback)
- Small Language Model via `phi3:instruct` through Ollama

**Infrastructure**
- Ollama for local model inference
- In-memory vector store with performance caching

## Architecture

The project is organized into two core services, each exposing its own API endpoint:

### 1. Vector Embedding Service

The embedding service converts user messages into high-dimensional vectors and compares them against a set of pre-labeled intent documents using cosine similarity. This approach is fast and effective for matching semantically similar phrasing.

- **Primary**: `nomic-embed-text` model via Ollama
- **Fallback**: OpenAI Embeddings API (if configured)
- **Fallback fallback**: Deterministic character-based hashing when no external API is available
- **Endpoint**: `POST /api/intent/embedding` — returns the matched intent with similarity scores

### 2. SLM Classification Service

The SLM service uses `phi3:instruct` to directly classify the intent of a user message. This approach is more flexible for handling novel phrasing but involves more latency.

- **Primary**: Ollama-hosted `phi3:instruct`
- **Fallback**: Keyword-based classification when Ollama is unavailable
- **Endpoint**: `POST /api/intent/slm` — returns the classified intent with confidence metrics

### Singleton Pattern

Both services are implemented as singletons, ensuring a single consistent service instance is reused across all API routes. This avoids redundant model loading and keeps the in-memory vector store coherent.

## Key Design Decisions

**Graceful Fallbacks**: Every external dependency (Ollama, OpenAI) has a fallback so the app remains functional even without internet access or a running model server. This was an intentional design choice to make the system more robust during development and demos.

**Modular Structure**: The codebase is split into `/app` (UI and routes), `/services` (embedding and SLM logic), `/data` (intent documents), and `/lib` (shared utilities). This separation makes it easy to swap out models or add new intent categories.

**Comparing Approaches**: By exposing both classification strategies through separate endpoints, the project makes it straightforward to benchmark embedding-based vs. SLM-based classification side by side.

## What's Next

- Add a UI toggle to switch between embedding and SLM classification in real time
- Expand the intent document set to cover more use cases
- Add logging and latency metrics to quantify the performance tradeoff between the two approaches
- Explore hybrid classification: use embeddings as a fast first pass, then fall back to the SLM for low-confidence results
