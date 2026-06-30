# Project 3: HR Onboarding Agent

**Stack:** watsonx.ai + watsonx.orchestrate  
**Duration:** 1 week  
**Difficulty:** Tier 2 — Intermediate  
**Mock documents:** [`project-03-mock-docs/`](project-03-mock-docs/)

---

## Overview

Build an agent that guides new hires through the onboarding process. The agent can answer questions about company policies, submit IT access requests, and book orientation sessions — all through a conversational interface. Unlike the Tier 1 projects, this is not a single model call: it is an orchestrated system where the model decides what action to take, calls the right tool to do it, and manages a multi-turn conversation across steps.

This project introduces the most important architectural shift in AI application development — moving from a model that *generates* to an agent that *acts*. With that shift comes a new class of problems: what should the agent be allowed to do on its own, what requires human approval, and what happens when it gets it wrong.

---

## What to Build

A working onboarding agent with:

1. **A conversational interface** — the new hire interacts with the agent via chat (CLI or simple UI)
2. **A policy Q&A skill** — the agent answers questions about HR policies using a small document set (can reuse RAG concepts from Project 1)
3. **An IT request skill** — the agent collects required information and submits a mock IT access request (writing to a file or a simple data store is sufficient — no real ticketing system needed)
4. **A session booking skill** — the agent checks available orientation slots and books one on behalf of the user (a hardcoded schedule is fine)
5. **A guardrail layer** — certain actions require the agent to confirm with the user before proceeding

The focus is on the orchestration logic, not on building production-grade integrations. Mock backends are expected and appropriate.

---

## Week Plan

### Day 1 — Understand agentic systems
- Read about the ReAct pattern (Reasoning + Acting): how an agent decides which tool to call, calls it, observes the result, and decides what to do next
- Study how watsonx.orchestrate defines skills and how the orchestration layer routes between them
- Map out the agent's capabilities on paper: what can it do, what inputs does each action need, what can go wrong?
- Deliverable: a hand-drawn or written diagram of the agent's decision flow

### Day 2 — Build the policy Q&A skill
- Use the provided mock HR documents in `project-03-mock-docs/` (leave policy, IT access policy, code of conduct, benefits guide, orientation guide)
- Build a retrieval-backed skill that answers policy questions (this can be a lightweight version of Project 1)
- Wire it into the orchestrate environment as a callable skill
- Deliverable: a skill the agent can invoke to answer "what is the leave policy?" style questions

### Day 3 — Build the IT request and session booking skills
- IT request skill: the agent must collect the new hire's name, role, and required systems before submitting — it should ask follow-up questions if any are missing
- Session booking skill: present available slots, confirm the user's choice, and write the booking to a simple store (a JSON file is fine)
- Deliverable: two working skills, each testable in isolation before being wired to the agent

### Day 4 — Wire everything together and add guardrails
- Connect all three skills to the orchestration layer
- Define which actions require explicit user confirmation before the agent proceeds (booking a session and submitting an IT request should both require confirmation)
- Test multi-turn conversations end to end: a new hire who asks a policy question, then requests IT access, then books a session in a single conversation
- Deliverable: a working end-to-end agent that handles a full onboarding conversation

### Day 5 — Test failure modes and reflect
- Deliberately trigger failure scenarios (see Common Pitfalls below) and document how the agent behaves
- Fix at least two failure modes
- Write a short reflection: what decisions did you make about what the agent can do autonomously vs. what requires human approval, and why?
- Deliverable: failure mode report and written reflection

---

## Key Concepts to Understand

These are the things the trainee should be able to explain by the end of the week.

### The Agentic Loop
A traditional model call is a single exchange: input in, output out. An agent runs a loop:

1. **Think** — given the conversation history and available tools, what should I do next?
2. **Act** — call a tool (or ask the user a question)
3. **Observe** — receive the result of the action
4. **Repeat** — feed the result back into the next thinking step

This loop continues until the agent decides the task is complete. Understanding this loop is essential because most agent bugs happen at the boundaries: the agent acts when it should ask, or gets stuck in a loop because it can't interpret a tool result.

### Tool/Skill Definition
Each skill the agent can call must be defined with:

- **Name and description** — the model uses this to decide when to call it
- **Input schema** — what parameters the skill requires
- **Output schema** — what it returns

The description is critically important. If it is vague or overlapping with another skill's description, the agent will call the wrong one or be unable to choose between them.

### Act vs. Ask vs. Escalate
One of the most important design decisions in any agent is defining the boundary between what it does automatically, what it confirms with the user, and what it hands off entirely:

- **Act autonomously:** low-stakes, reversible, or clearly within the user's stated intent (e.g. answering a policy question)
- **Ask for confirmation:** actions with side effects that are hard to reverse (e.g. submitting a request, booking a slot)
- **Escalate to a human:** anything outside the agent's defined scope, or where the agent is uncertain and the stakes are high

Trainees often default to making agents too autonomous because it feels more impressive. A good agent knows its limits.

### Stateful Conversation Management
An agent needs to remember what was said earlier in the conversation. This is typically managed by passing the full conversation history to the model on each turn. Key things to understand:

- The longer the conversation, the more tokens are consumed on each turn
- Important information (like the new hire's name and role) should be tracked explicitly rather than relying on the model to extract it from a long history
- If the conversation is interrupted and resumed, the state must be recoverable

### Failure Modes in Agentic Systems
Agents fail in ways that single model calls do not:

- **Infinite loops:** the agent keeps calling a tool that returns an unhelpful result and doesn't know how to stop
- **Ambiguous tool selection:** two skills have similar descriptions and the agent picks the wrong one
- **Missing required inputs:** the agent calls a skill before collecting all the information it needs
- **Hallucinated tool calls:** the agent invents parameters that weren't provided, rather than asking the user for them

---

## Acceptance Criteria

### For the trainee — the system must:
- [ ] Handle a full onboarding conversation covering all three capabilities (policy Q&A, IT request, session booking) without breaking
- [ ] Ask for user confirmation before submitting the IT request or booking a session
- [ ] Ask follow-up questions when required information is missing rather than proceeding with incomplete data or making something up
- [ ] Respond gracefully to out-of-scope questions ("what's the best restaurant near the office?") — acknowledge it can't help rather than attempting an answer
- [ ] Include a written failure mode report documenting at least 3 failure scenarios and how they were addressed

---

## Common Pitfalls to Watch For

- **Overlapping skill descriptions:** if the IT request skill and the policy Q&A skill both mention "employee information," the agent may confuse them. Descriptions should be unambiguous and non-overlapping.
- **No confirmation before side effects:** an agent that submits requests or books sessions without asking is dangerous in production. This is a design flaw, not a missing feature.
- **Relying on the model to remember everything:** long conversation histories become expensive and unreliable. Critical state (name, role, selections made) should be tracked explicitly in the application layer.
- **Only testing the happy path:** the agent will almost always work when the user provides exactly the right information in the right order. Testing must include messy inputs: vague requests, missing information, topic changes mid-conversation.
- **Not defining an exit condition:** what does "done" look like for this agent? Without a clear completion state, the agent may keep asking questions after the task is finished.

---

## Stretch Goals (for more experienced trainees)

- Add an **escalation path**: if the user's request is outside the agent's capabilities, it should offer to connect them with a human HR representative (mocked as logging the request to a file)
- Implement **conversation resumption**: if the user closes and reopens the chat, the agent should be able to pick up where it left off using persisted conversation state
- Add a **confidence threshold**: if the policy Q&A skill retrieves context with low similarity scores, the agent should flag that the answer may be incomplete rather than presenting it with full confidence
- Explore **parallel tool calls**: some orchestration frameworks allow the agent to call multiple skills simultaneously. Identify at least one point in the onboarding flow where this would reduce latency and implement it

---

## Resources

- watsonx.orchestrate documentation: skill definition, agent configuration, and conversation management
- "ReAct: Synergizing Reasoning and Acting in Language Models" (Yao et al., 2022) — the foundational paper behind most agentic frameworks
- watsonx.ai documentation: tool use and function calling in foundation models
