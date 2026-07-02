# Project 0: Development Environment & Engineering Basics

**Stack:** None — no watsonx, no AI. Pure software engineering fundamentals.
**Duration:** 1 day
**Difficulty:** Pre-work — optional, ungraded

---

## Overview

Before anyone touches a foundation model, this project checks that the basic engineering scaffolding is solid: setting up a project properly, calling an external service, handling secrets correctly, testing your own code, and using git like it matters. None of this is AI — that is the point. Every project from here on assumes you can do this without thinking about it, and if that assumption is wrong, Project 1 is the wrong place to find out.

This project is optional and not graded in the way later projects are. There is no accuracy threshold, no evaluation report. If you're already comfortable with everything in "What to Build" below, you can skip straight to Project 1. If you're not sure, do it anyway — it exists so you and your mentor both know, before the AI work starts, where you're starting from.

---

## What to Build

A small command-line tool, with no AI involved, that:

1. Lives in a properly structured git repository with a dependency manifest
2. Calls a public REST API and displays real data it retrieved
3. Reads any required configuration (API keys, etc.) from environment variables — never hardcoded, never committed
4. Has a small test suite covering its core logic
5. Fails gracefully when the external API is unreachable or returns something unexpected

The API you call is up to you — pick anything free and public (a weather API, a public GitHub endpoint, a currency conversion API, whatever interests you). The tool itself can be as simple as "fetch this data and print it nicely." The point is not the tool. The point is everything around it.

---

## Milestones

Work through these in order. There is no fixed day-by-day schedule — move at the pace that gets each milestone genuinely done, not just checked off.

### Milestone 1 — Set up the project properly
- Initialize a git repository
- Add a `.gitignore` before you add anything else — it must exclude your virtual environment, any `.env` file, and any other local-only files
- Set up a virtual environment or equivalent dependency isolation (venv + pip, poetry, conda — your choice) and a dependency manifest (`requirements.txt`, `pyproject.toml`, etc.)
- Create a minimal project structure (a source folder, an entry point, a placeholder README)
- Deliverable: an empty-but-structured repo with a first commit that contains no secrets and no dependency artefacts

### Milestone 2 — Call an external API safely
- Write a script that calls your chosen public API and prints a formatted result
- If the API requires a key, load it from an environment variable via a `.env` file — never hardcode it in source
- Confirm, by checking your git history, that the key has never been committed — not even in an earlier commit you later "fixed"
- Deliverable: a working script that fetches and displays real data, with no secret ever present in version control

### Milestone 3 — Add tests and handle failure
- Write at least 2–3 unit tests for your script's logic (e.g. parsing the API response, formatting the output) using a standard test runner for your language
- Add explicit error handling: what happens if the API is unreachable, times out, or returns malformed data? The script must not crash with an unhandled stack trace — it should fail with a clear, human-readable message
- Deliverable: a passing test suite, and a script that degrades gracefully when the external service misbehaves

### Milestone 4 — Reflect and clean up
- Review your git history — does it read as a sequence of meaningful steps, or is it one giant commit? Tidy it if needed
- Write a short README: what the tool does, how to install dependencies, how to set the required environment variable, how to run it and run the tests
- Deliverable: a clean, documented repo you'd be comfortable handing to someone else cold

---

## Key Concepts to Understand

These are the things you should be able to explain by the end, and that every later project will assume you already know.

### Dependency Isolation
Installing packages globally on your machine works until two projects need different versions of the same library. A virtual environment (or equivalent) gives each project its own isolated set of dependencies, and a manifest file records exactly what they are so anyone else can reproduce your setup.

### Secrets Management
An API key or credential must never appear in source code or be committed to git — not in the code, not in a config file, not "temporarily" while you get something working. The standard pattern is: read secrets from environment variables, keep them in a local `.env` file, and make sure `.gitignore` excludes that file *before* it's ever created. If a secret is committed once, it exists in your git history forever, even if you delete it in a later commit — the only real fix is treating the credential as compromised and rotating it.

### Calling a REST API
The mechanics that every later project will build on: making an HTTP request, checking the status code, parsing a JSON response, and handling the case where any of that fails. If you've never done this before, this is the milestone to slow down on.

### Testing Basics
A unit test checks that a specific piece of logic does what you expect, independent of the rest of the system. Good tests cover more than the happy path — at minimum, test what your code does with the input it expects *and* with input that will break it. A test suite that only ever tests success gives you false confidence.

### Failing Gracefully
Code that assumes everything will go right is not production code — it's a demo. An external API you don't control will eventually be slow, down, or return something you didn't expect. Deciding what your program does in that moment, deliberately, is a basic engineering habit that every subsequent project depends on.

### Git as a Working Log
Commits are not a formality — a clear commit history is how you (and anyone reviewing your work) reconstruct what happened and why. Meaningful, incremental commits with clear messages are a habit, not a one-time cleanup step at the end.

---

## Acceptance Criteria

### The project must:
- [ ] Live in a repo with a clear structure and a dependency manifest
- [ ] Contain no secrets or API keys anywhere in the git history — verified by checking that `.env` (or equivalent) is gitignored from the first commit
- [ ] Successfully call a public API and display real, live data
- [ ] Include at least 2–3 passing unit tests covering the tool's core logic
- [ ] Fail gracefully — no unhandled crash — when the API call fails or returns unexpected data
- [ ] Include a README covering setup, configuration, and how to run the tool and its tests
- [ ] Have a git history of at least 3 meaningful, incremental commits

---

## Common Pitfalls to Watch For

- **Hardcoding a key "just to get it working," then forgetting to move it to an environment variable.** This is the single most common mistake — and the fact that it's common is exactly why this project exists before any real API keys (watsonx credentials) are involved.
- **Committing a virtual environment folder or a `.env` file** because `.gitignore` wasn't set up first. Once committed, removing it from the working tree doesn't remove it from history.
- **Tests that only check the happy path.** A test suite with no failure case tested is not verifying the part of the code that will actually break in production.
- **Treating this as busywork and rushing it.** The value of this project is entirely in what it reveals about your baseline habits — rushing through it defeats the purpose for both you and your mentor.

---

## Resources

- Your language's official documentation on virtual environments / dependency management (e.g. Python's `venv` and `pip`, or your stack's equivalent)
- Your chosen public API's documentation
- Your test runner's getting-started guide (e.g. `pytest` for Python)
- A short git basics guide, if you're not already comfortable with commits, `.gitignore`, and viewing history
