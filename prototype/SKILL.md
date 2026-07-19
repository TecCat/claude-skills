---
name: prototype
description: >
  Build a throwaway prototype to flesh out a design before committing to it.
  Routes between two branches — a runnable terminal app for state/business-logic
  questions, or several radically different UI variations toggleable from one route.
  Use when the user wants to prototype, sanity-check a data model or state machine,
  mock up a UI, explore design options, or says "prototype this", "let me play with
  it", "try a few designs".
disable-model-invocation: false
---

# Prototype

A prototype is throwaway code that answers a question. The question decides the shape.

## Step 1 — Identify the Question

Determine which question is being answered — from the user's prompt, the surrounding
code, or by asking if the user is around:

- **"Does this logic / state model feel right?"** → follow [LOGIC.md](./LOGIC.md)
  Build a tiny interactive terminal app that pushes the state machine through cases
  that are hard to reason about on paper.

- **"What should this look like?"** → follow [UI.md](./UI.md)
  Generate several radically different UI variations on a single route, switchable
  via a URL search param and a floating bottom bar.

The two branches produce very different artifacts — getting this wrong wastes the
whole prototype.

If the question is genuinely ambiguous and the user isn't reachable, default to
whichever branch better matches the surrounding code (a backend module → logic;
a page or component → UI) and state the assumption at the top of the prototype.

## Step 2 — Locate and Name the Prototype

Place the prototype **next to the code it is prototyping** — same directory as the
module or page — so context is obvious.

Name it so a casual reader can see it is NOT production:

```
# Examples
src/checkout/prototype-payment-flow/
src/components/UserCard/prototype-redesign/
app/dashboard/prototype-v2/
```

Add a `README.md` inside with:
1. **The question** this prototype is answering (one sentence)
2. **How to run it**
3. A blank `## Answer` section to be filled in when done

## Step 3 — Build Throwaway, Not Production

Rules that apply to both branches:

- **No tests** — a prototype that needs tests is no longer a prototype
- **No real database** — use in-memory state unless the question is specifically
  about persistence
- **No generalisation** — no "what if we wanted to support X later"
- **No error handling beyond what you need to run**
- **Surface the state** — after every action (logic) or on every variant switch
  (UI), print or render the full relevant state so the user can see what changed

## Step 4 — Answer and Clean Up

When the prototype has answered its question:

1. **Capture the answer** somewhere durable before deleting:
   - A commit message
   - An ADR (`docs/adr/`)
   - A GitHub issue
   - A `NOTES.md` next to the prototype

2. **Delete or absorb** — either delete the prototype entirely, or fold the
   validated decision into the real code. Don't leave it rotting.

The answer is the only thing worth keeping from a prototype.

---

## Quick Reference

| Question type | Branch | Artifact |
|---|---|---|
| "Does this state model feel right?" | LOGIC.md | Interactive terminal app |
| "What should this look like?" | UI.md | Multi-variant web page |
| Ambiguous (backend module) | LOGIC.md | Interactive terminal app |
| Ambiguous (page / component) | UI.md | Multi-variant web page |
