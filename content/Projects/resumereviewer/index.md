---
title: "Resume Reviewer"
summary: "I developed an app that allows users to upload their resumes in PDF or DOCX format and provides feedback from an LLM."
date:  2025-02-01T0:00:00-00:00
# weight: 1
aliases: ["/resumereviewer"]
tags: ["Projects", "Resume Reviewer"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false #change this to publish
math: true
hidemeta: true
comments: false
description: "Duration: Feburary 2025 - Current" 
canonicalURL: "https://canonical.url/to/Projects/mlprojects"
disableHLJS: false # to disable highlightjs
disableShare: false
disableHLJS: true
hideSummary: false
searchHidden: true
ShowReadingTime: false
ShowBreadCrumbs: false
ShowPostNavLinks: false
ShowWordCount: false
ShowRssButtonInSectionTermList: false
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/AshwinKTyagi/AshwinKTyagi.github.io/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Github: https://github.com/AshwinKTyagi/Resume-Reviewer

## Description

I developed an app that allows users to upload their resumes in PDF or DOCX format. The backend extracts the text from the uploaded resume and processes it using a large language model to provide feedback.

## Backend Techstack
    Routing
    - FastAPI

    Document Processing
    - pdfminer
    - python-docx

    LLM Support
    - OpenAI API
    - OLLaMa
    - LangChain Community Embeddings

    Storage and Authentication
    - MongoDB
    - FastAPI's JWT Auth

## Frontend Techstack
    App Construction
    - NextJS

    Styling
    - TailwindCSS
    - React Dropzone/Markdown

## Features 
### Resume Document Processing

The first step in the resume review pipeline occurs where uploaded documents are parsed and prepped for analysis. Here is the process:

1. File Upload 
    - Users can upload resumes in PDF or DOCX format through the frontend interface
    - Once uploaded, the file is sent to the `FastAPI` backend for processing
2. Text Extraction
    - The backend extracts clean text content from the document using `pdfminer` or `python-docx`.
    - The text is then prepped for downstream analysis by the LLM.
3. Caching & Deduplication
	- Before submitting the extracted text to the LLM, the backend checks `MongoDB` to see if the same document has already been processed.
    - If a match is found, the backend returns the cached result, avoiding redundant processing and minimizing compute usage.
	- This optimization helps reduce unnecessary calls to `OpenAI`’s API or a local `Ollama`-hosted `LLaMA 2` instance, saving both time and money.

### Authentication

To ensure secure access to resume-data and the AI-generated insights, the user's information is protected by a simple but effective authentication flow. Here is how I handled it:

1. User Registration
	- New users can create an account by providing an email and password.
	- Passwords are hashed and salted using a secure algorithm (`bcrypt`) before being stored in `MongoDB`.
2. User Login
	- Returning users can log in with their credentials.
	- The backend verifies the email and compares the submitted password with the stored hash.
3. Session Management
    - On successful registration and login, the user is assigned a new `JWT` token which the frontend stores and uses for subsequent requests.
    - These tokens are inclueded in the Auth header of every request to protected endpoints.
    - The `FastAPI` uses middleware to decode and verify each token so that only authenticated users can access and modify data
4. User-Specific Data Access
    - Almost every database action is linked to a user's ID, which is extracted from the token.
    - This ensures data isolation so users can only access and interact with their own content.

### Chat System with RAG

The resume reviewer includes a chat interface where users can ask questions or request more feedback about a specific resume. This feature is powered by a Retrieval-Augmented Generation (RAG) Approach, which enables context-aware, document-specifc responses. Here's how it works:

1. Message Submission
    - Users submit questions via the frontend chat UI.
    - The query, along with the user's *file_id* is sent to the backend.
2. Context Retrieval
    - The backend looks up the resume associated with the *file_id* in `MongoDB` and retrieves the latest extracted text.
3. RAG Construction
    - A RAG prompt is built by combining 
        - the users question: __{query}__
        - the retrieved resume text and chat history: __{context}__
    - This prompt is designed to anchor the LLM’s generation in document-specific data, in order to improve consistency and relevance.
4. Conversation Persistence
    - The user's message and AI's reply are appended to a *chat_history* array associated to the document in `MongoDB`.
    - This allows the frontend to display a continuous and contextual conversation

## Future Plans

Handle Vector Embeddings
- Embedding-Based Job Matching
    - The goal is to compare a user’s resume embedding to those of successful, accepted resumes for specific job roles.
    - By computing cosine similarity between vectors, the system can provide a relevance score and actionable feedback
- Improved RAG Context Filtering
    - Embeddings can also help narrow down which parts of the resume to include as context for RAG-style prompts—especially useful when the resume is long or highly technical.