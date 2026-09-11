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
