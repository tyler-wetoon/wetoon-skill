---
name: write-ticket
description: Turn a plain-language description into a well-structured Story, Task, or Bug ticket following the team's templates. Use whenever the user wants to create, write, or draft a ticket, issue, user story, task, or bug report. Decides the ticket type from the description, reads the source code to get the behavior right, asks about anything unclear or missing edge cases, and writes a clean, non-technical ticket that anyone on the team can read.
argument-hint: describe the feature, change, or bug in plain language
user-invocable: true
---

Turn a short description into a complete, ready-to-paste ticket. The golden rule: **the ticket is read by many people (PM, design, QA, business, dev) — so it describes behavior and intent in plain language, never code, file names, or implementation details.** You read the source code to get the facts right; you do not put the source code in the ticket.

## Core principles

- **Reader-first, not dev-first.** No file paths, function names, component names, framework terms, or code snippets in the ticket body. Describe what the user sees and does, and what the system should do — in everyday language.
- **Read the code to be accurate.** Explore the relevant feature so the flow, field names (as shown in the UI), states, and edge cases are correct. The code informs the ticket; it never appears in it.
- **Ask when it's genuinely unclear.** If the description is ambiguous or an edge case is unaddressed, ask focused questions before writing. Don't invent behavior. Don't ask about things you can answer by reading the code or that have an obvious default.
- **Pick the right type.** Decide Story vs Task vs Bug from the description (see below), state which you chose and why in one line, then write it in that template.
- **Clean and testable.** Acceptance criteria are specific and verifiable. Titles are short and descriptive. No filler.

## Workflow

### 1. Classify the ticket type

- **Story** — a requirement from users or the business: a new feature, a new rule, a change to how something should behave. Written from the user's perspective. *"We want users to…", "The system should…", "Prevent…", "Add…".*
- **Bug** — an already-built feature does not behave as its Story specified. There is a defect: something is broken, inconsistent, or missing versus the intended behavior. *"X is broken", "doesn't work", "shows wrong…", "should do Y but does Z".*
- **Task** — internal work with no direct user-facing requirement: refactor, performance, setup/config, tooling, dependencies, tech debt. A simple description is enough for these.

If it's ambiguous (e.g. "the validation is wrong" could be a Bug on existing behavior or a Story for new behavior), ask which before proceeding.

### 2. Read the source code for the truth

Locate the relevant feature and read enough to write accurately:

- The real user flow: screens, buttons, fields, and their **UI labels** (use the label the user sees, not the code identifier).
- Current behavior and states (validation, errors, loading, empty, success), so a Story's criteria are grounded and a Bug's expected/actual are precise.
- Edge cases the code already handles or clearly misses.

Use search/explore tools. This step is for *your* understanding — translate everything you learn into plain user-facing language for the ticket.

### 3. Ask about gaps and edge cases

Before writing, if anything material is unclear, ask concise questions — e.g. unspecified error copy, what should happen on an edge case, which platform (desktop/mobile) or account type is in scope, expected result at a specific step of a bug. Prefer a few sharp questions over guessing. Skip questions the code already answers.

### 4. Write the ticket in the matching template

Use the exact template for the chosen type (below). Fill every relevant section; omit a section only if it truly doesn't apply and say so. Keep language plain and behavior-focused.

### 5. Deliver

Output the finished ticket as clean markdown the user can copy-paste. Lead with one line stating the chosen type and a one-sentence reason. If you made any assumptions, list them briefly under the ticket so they can be corrected. Offer to save it to a file if the user wants.

## Templates

### Story

```
Title: [Clear, descriptive title summarizing the story or feature]

As a: [User role or persona]
I want to: [User's goal or action]
So that: [The benefit / why it matters]

Acceptance Criteria:
- [Specific, testable criterion]
- [Another criterion — cover the main flow and the edge cases]
- [Optional additional criteria]

Notes / Additional Info:
- [Context, dependencies, or edge cases — still in plain language]

Attachments:
- [Links to designs, screenshots, docs, if any]
```

### Bug

```
Title: [Short, descriptive title summarizing the issue]

Description

Pre-condition:
- [Any state/setup needed to reproduce, e.g. account type, logged in]

Steps to Reproduce:
1. Go to: [screen or section name]
2. Click on the [element name as labeled in the UI]
3. Enter [input value] into the [field name]
4. Click the [button name]
5. Observe the behavior
6. [Continue steps, including recovery steps if relevant]

Expected Result:
- [What should happen at each key step]

Actual Result:
- [What actually happens, and how it differs]

Attachments:
- [Screenshots, videos, logs, console errors]

Additional Info:
- [Test data or context that helps]

Environment:
- Stage: [Staging / Production]
- Platform: [e.g. Web – Chrome on macOS]
- App Version: [e.g. Latest staging build]
```

### Task

A simple description is sufficient. Give it a clear title and a short paragraph of what needs doing and why. Add a brief acceptance/definition-of-done line if it helps, but keep it lightweight — no user-story framing.

```
Title: [Clear, descriptive title]

Description: [What needs to be done and why, in a sentence or two]

Done when: [Optional — how we know it's complete]
```

## Writing rules

- **Titles:** short, specific, describe the outcome (Story) or the fault (Bug).
- **Banned from the ticket body:** file names/paths, function/component/variable names, framework or library names, code, API endpoints, DB details. If a technical dependency matters, describe it as a plain requirement in Notes (e.g. "should be validated on both the form and the server" — not the mechanism).
- **Use UI labels** the user actually sees for fields, buttons, and screens.
- **Acceptance criteria** are observable and testable — phrase them so QA can pass/fail each one.
- **Bug expected/actual** should be step-anchored and concrete, not vague ("it's broken").
- **State assumptions** rather than silently guessing; list them under the ticket.
