# Project 2: Multi-Tone Content Generator

**Stack:** watsonx.ai  
**Duration:** 1 week  
**Difficulty:** Tier 1 — Foundation

---

## Overview

Build a tool that takes a topic or a piece of raw information and generates polished content in multiple tones — a formal report summary, a casual social media post, and a concise executive briefing. The user provides the input once, and the tool produces all three variations.

This project is a focused deep-dive into prompt engineering. Unlike the RAG project, there is no external data retrieval here — the quality of the output depends entirely on how well the trainee crafts and structures their prompts. It also introduces the practical reality of model selection: not every task needs the most powerful (and most expensive) model.

---

## What to Build

A working content generation pipeline with:

1. **Input handling** — accept a topic, a block of raw text, or a set of bullet points from the user
2. **Prompt templates** — a well-crafted prompt for each of the three tones
3. **Parallel generation** — call watsonx.ai to produce all three variations
4. **Structured output** — return results in a clean, consistent format (JSON or formatted text)
5. **A simple interface** — a minimal UI or CLI where the user inputs content and receives the three variations side by side

The domain is flexible. Good defaults: summarising a technical report, turning meeting notes into communications, or generating product descriptions.

---

## Week Plan

### Day 1 — Understand the problem
- Read about the difference between system prompts and user prompts in foundation model APIs
- Explore watsonx.ai's prompt lab — experiment manually with the same input using different instructions and observe how the output changes
- Define the three tones the tool will support and write down in plain English what makes each one distinct

### Day 2 — Build the first prompt template
- Pick one tone (start with the formal report summary)
- Write a system prompt that reliably produces that tone
- Test it against at least 5 different inputs — does it hold the tone consistently?
- Deliverable: a working, tested prompt for one tone with 5 example outputs

### Day 3 — Build the remaining prompt templates
- Repeat the process for the casual social post and executive summary tones
- Pay attention to length constraints: social posts should be short, executive summaries scannable
- Experiment with few-shot examples — add 1–2 example outputs inside the prompt and observe whether consistency improves
- Deliverable: three working prompt templates, each tested against the same 5 inputs

### Day 4 — Add structured output and wire it together
- Modify the prompts to return output in a consistent JSON structure (e.g. `{ "tone": "formal", "output": "..." }`)
- Build the pipeline that takes one input and calls the model three times (once per tone)
- Handle failures gracefully — what happens if one call fails or returns malformed output?
- Deliverable: end-to-end pipeline that returns all three variations for a given input

### Day 5 — Evaluate, compare models, and reflect
- Build a test set of at least 20 inputs and evaluate output quality for each tone
- Swap the model out for a smaller/cheaper one — does quality drop noticeably? For which tone?
- Document findings in a short evaluation report
- Deliverable: evaluation report covering tone consistency, quality observations, and model comparison

---

## Key Concepts to Understand

These are the things the trainee should be able to explain by the end of the week.

### System Prompts vs. User Prompts
Foundation models distinguish between two types of input:

- **System prompt:** sets the model's persistent behaviour, role, and constraints for the entire interaction. This is where you define the tone, the output format, and any rules the model must follow.
- **User prompt:** the actual input for this specific request — the topic or raw text to transform.

Keeping these separate matters because it lets you reuse the same system prompt (tone definition) across many different user inputs without rewriting it each time. Mixing them together makes your prompts brittle and harder to iterate on.

### Few-Shot Prompting
A zero-shot prompt gives the model instructions only. A few-shot prompt also includes examples of what good output looks like:

```
Transform the following text into a casual social media post.

Example input: Q3 revenue increased by 12% year-over-year driven by cloud services growth.
Example output: Big news — our cloud business is booming! Revenue up 12% vs last year. 

Now transform this:
[user input]
```

Few-shot examples are one of the most reliable ways to steer a model toward a specific style. The key is that the examples must be genuinely representative — bad examples teach bad behaviour.

### Output Formatting and Structured Generation
Asking a model to return JSON is useful but fragile if not done carefully. The prompt must be explicit:

- State the exact structure expected
- Provide a schema or example of the JSON
- Instruct the model not to add explanation or preamble outside the JSON

Even with careful prompting, models occasionally produce malformed JSON. The pipeline must handle this — either by validating and retrying, or by falling back to plain text.

### Model Selection Tradeoffs
Not all tasks need the most capable model. A useful mental model:

| Task | What it needs | Model tier |
|---|---|---|
| Tone transformation of short text | Instruction following, style | Smaller / faster |
| Summarising a complex technical document | Reasoning, compression | Larger |
| Extracting structured data from messy input | Precision, format adherence | Larger |

Choosing a smaller model for tone generation is often the right call — it's cheaper, faster, and the quality difference is frequently negligible for style-heavy tasks. The trainee should be able to argue their model choice, not just accept the default.

### Prompt Brittleness
A prompt that works well on 5 test cases can fail on the 6th. Common reasons:

- The input is longer or shorter than the examples the prompt was designed around
- The input contains formatting (bullet points, tables) the prompt doesn't account for
- The input is in a different domain than what was tested

Robustness means testing prompts against diverse inputs — not just the easy ones.

---

## Acceptance Criteria

### For the trainee — the system must:
- [ ] Produce distinct, recognisably different outputs for each of the three tones given the same input
- [ ] Return output in a consistent, structured format (JSON or clearly delimited sections)
- [ ] Include at least one few-shot example per prompt template
- [ ] Handle malformed or unexpected model output without crashing
- [ ] Include an evaluation report covering: tone consistency across 20 inputs, at least one failure case per tone, and a model comparison

### For the mentor — evaluate on:
| Criterion | What to look for |
|---|---|
| **Prompt quality** | System and user prompts are cleanly separated; instructions are unambiguous |
| **Tone differentiation** | The three outputs are genuinely distinct — not just the same text with minor rewording |
| **Few-shot use** | Examples in the prompt are well-chosen and actually representative of the target tone |
| **Structured output** | JSON is valid and consistently structured; error handling exists for when it isn't |
| **Model reasoning** | Trainee can articulate why they chose their model and what they observed when they changed it |

---

## Common Pitfalls to Watch For

- **Prompt drift across tones:** trainees often write the first prompt carefully and rush the other two. All three need the same level of rigour.
- **Over-constraining length:** telling the model "write exactly 280 characters" is much harder to enforce than "keep it under 3 sentences." Soft constraints are more reliable than hard ones.
- **Not testing edge cases:** what happens if the input is already in the target tone? What if the input is a single sentence? What if it's in another language?
- **Assuming JSON is always valid:** models will occasionally return text before or after the JSON block, add trailing commas, or use single quotes. The pipeline needs a parsing step that handles this.
- **Treating all failures as prompt failures:** sometimes the model produces poor output because the input itself is ambiguous or very short. Trainees should distinguish between prompt problems and input problems.

---

## Stretch Goals (for more experienced trainees)

- Add a **fourth tone** of the trainee's own design — they must define it, write the prompt, and justify why it's a useful addition
- Implement **self-evaluation**: after generating each variation, make a second model call that scores the output on tone adherence (1–5) and flags any that fall below a threshold for regeneration
- Add a **batch mode**: accept a CSV of inputs and generate all three tones for each row, outputting results to a structured file
- Explore **parameter tuning**: vary temperature and top-p settings and document how they affect creativity vs. consistency in each tone

---

## Resources

- watsonx.ai documentation: prompt engineering guide and model parameters reference
- IBM prompt lab: useful for manual experimentation before writing code
- "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models" (Wei et al., 2022) — useful background on how prompt structure shapes model behaviour
