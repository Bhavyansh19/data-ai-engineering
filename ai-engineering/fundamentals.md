# AI Engineering Basics

## Tokens

LLMs don’t read text exactly like we do. They break it into smaller pieces called tokens. Input and output limits, cost, and response time are all connected to tokens.

## Context windows

A context window is the maximum amount of text, measured in tokens, that a model can handle at one time. Giving it too much irrelevant information can make the answer worse.

## Prompting

Good prompts clearly say what we want, give the useful context, set any limits, and explain the format we want back.

## Structured output

Structured output gives us a predictable format, like JSON, so Python code can read and check the response properly.

## Reliability

Hallucinations happen when the model gives us something made up but says it confidently. Trusted data, citations, validation, and allowing the model to say “I don’t know” can reduce this.

## Temperature

Low temperature is better when we want consistent data extraction. Higher temperature is more useful for creative answers.

## Embeddings

Embeddings convert text into numerical vectors. Texts with similar meanings tend to have vectors that are close together, even when they use different words. The individual dimensions usually do not correspond to simple human-readable concepts.

## Cosine similarity

Cosine similarity compares the direction of two vectors. A higher similarity generally indicates more similar meaning, which makes it useful when searching for relevant text embeddings.

## Vector databases

Vector databases store embedding vectors along with their text chunks or references and metadata. They can search for vectors close to a query vector and filter results using metadata.

## Retrieval-Augmented Generation (RAG)

A basic RAG pipeline splits source documents into chunks, creates embeddings for the chunks, stores them, embeds the user question, retrieves similar chunks, and sends the retrieved context with the question to an LLM.

## Chunking and retrieval quality

Chunks that are too small may lose important context. Chunks that are too large can reduce retrieval precision, increase token usage, and exceed context limits. Retrieval quality can be improved with better chunking, stronger embeddings, metadata filters, hybrid keyword-plus-vector search, and reranking.
