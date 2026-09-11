# AI Engineering Fundamentals

## Tokens

LLMs process text as tokens rather than exactly as words. Input and output limits, cost, and latency are measured using tokens.

## Context windows

A context window is the maximum amount of tokenized input and output a model can process at one time. Too much irrelevant context can reduce answer quality.

## Prompting

Good prompts specify the task, relevant context, constraints, and desired output format.

## Structured output

Structured output requires a predictable schema, such as JSON, so downstream Python code can parse and validate the response.

## Reliability

Hallucinations are unsupported or invented responses. Grounding with trusted data, citations, validation, and an explicit unknown option can reduce the risk.

## Temperature

Lower temperature is generally better for deterministic extraction and structured data. Higher temperature is useful for creative variation.
