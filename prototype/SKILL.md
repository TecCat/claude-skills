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
credits: |
  Adapted from mattpocock/skills/prototype.
  See References section below.
---

# Prototype

## The Core Idea

Prototypes are the thinking stage, not the shipping stage.
Before you commit to a design—before you start the sprint—
you ask the hard question by building and running it.

The single clearest question shapes everything: what you build, how long you spend,
where you put your energy. Two very different questions need very different artifacts.
Mixing them guarantees confusion and wasted effort.

---

## Step 1 — Identify Your Question

What are you actually trying to learn?

| If you're asking... | Reason | Build this | Output |
|---|---|---|---|
| **Can this state model actually handle all the cases?**<br>Can we represent X? Does this data structure break at edge cases? | You can't reason about complexity on paper. Complex state machines need to be walked through by hand. | Interactive terminal app<br>(state explorer) | You push buttons, watch state change, discover what doesn't work |
| **How should users experience this?**<br>Which layout works? What interaction feels right? Should this be a modal or a page? | You can't choose between designs by describing them. Visual comparison is 10× faster than debate. | Multiple UI variants<br>(3-5 designs, switchable) | You click to switch between designs, see trade-offs instantly |
| **Both at once** | ⚠️ **Stop here** | Split into two prototypes | One per question, one per artifact type |

**Ambiguous?** Default to the question type that matches your surrounding code:
- Backend module → logic (state/data question)
- Page or component → UI (interaction question)
- State your assumption at the top of the prototype.

---

## Step 2 — Locate and Name the Prototype

Place the prototype **next to the code it is prototyping** — same directory as the
module or component it explores. Context should be obvious to anyone opening the folder.

Name it so a casual reader knows it's **NOT production code**:

```
✅ Good names:
  src/checkout/prototype-payment-flow/
  src/components/UserCard/prototype-redesign/
  app/dashboard/prototype-v2/

❌ Bad names:
  src/checkout/payment-flow/  ← looks production
  ProtoPayment.jsx            ← too cryptic
```

### Create a README.md inside

Every prototype directory gets a `README.md` with exactly three sections:

```markdown
# Prototype: [Name]

## The Question
[One sentence. What are you trying to learn?]

Example: "Can we validate email on-blur without blocking UX?"

## How to Run
[One command. Whatever the project already uses.]

Example: `npm run proto:payment` or `python prototype.py`

## Answer
[Blank until you run it. Fill this in before deletion.]

[Your findings go here after you're done prototyping]
```

---

## Step 3 — Build Throwaway, Not Production

### Rules for Both Branches

These apply to **both LOGIC.md and UI.md** prototypes:

1. **No tests** — A prototype that needs tests isn't a prototype anymore; it's becoming production code. Stop and refactor.

2. **No real database** — Use in-memory state, mock data, or a scratch file clearly labeled "PROTOTYPE—wipe me".
   Exception: if the prototype's question is specifically about persistence (caching behavior, replication), then hit a real scratch DB.

3. **No generalization** — "What if we wanted to support X later?" = wasted effort.
   This prototype answers one question. When done, you delete it or fold the validated logic into real code.

4. **No error handling beyond runnable** — Skip try/catch, skip logging infrastructure, skip graceful degradation.
   If it crashes, that's fine—you'll see it immediately.

5. **Surface the state** — After every action (in logic) or every variant switch (in UI),
   print or render the full relevant state. The user must see what changed.

6. **Delete or absorb** — When the prototype answers its question, one of two things happens:
   - Delete it entirely, OR
   - Extract the validated logic and fold it into production code

   Don't leave prototypes rotting in the repo for months.

---

## Step 4 — Capture the Answer and Clean Up

### Before You Delete

The prototype will disappear, but the insight must stay. You have one day to capture it.

1. **Write the answer** into a durable place:
   - The `README.md` → Answer section (see Step 2)
   - An ADR: `docs/adr/NNNN-why-we-chose-X.md`
   - A GitHub issue or PR comment
   - A `DESIGN.md` in the component folder

2. **One sentence minimum**: "This turned out to matter more than I expected because..."

3. **Delete the prototype folder** (or the branch, or the file—whatever you created)

---

## For Teams (Recommended Additions)

These practices help teams scale prototype learning:

### Code Review the Prototype

Before deletion, have someone else walk through it:
- Does it actually answer your stated question?
- Did you learn something non-obvious?
- Does the insight belong in an ADR or decision log?

This takes 15 minutes and prevents re-prototyping the same question in 6 months.

### Prototype as Alignment Tool

When the team disagrees about UX (forms vs modal, pagination vs infinite scroll):
- Build both variants in the same prototype
- Let everyone click through
- Arguing about mockups is waste; clicking through designs converges faster

### Version Control Hygiene

Never commit prototypes to `main`:

```bash
git checkout -b feature/prototype-checkout-flow
# ... build and run prototype ...
# ... answer the question ...
git checkout main
git branch -D feature/prototype-checkout-flow  # Delete without merge
```

---

## Common Failures (Learn from these)

### Trap 1: The "Swiss Army Knife" Prototype

You try to answer 3 questions at once: state + UI + performance.

- **Result**: A franken-artifact that confuses everyone, including you.
- **Fix**: One question per prototype. When done, delete it and start fresh.

### Trap 2: Prototype Rot

It works so well that someone shoves it into production.
Now you're maintaining the throwaway code for years.

- **Fix**: Name it obviously (`prototype-*`). Delete it the day after you ship the real thing.
- **Better**: Use a branch, not main—delete the branch automatically.

### Trap 3: The Forgotten Answer

You built a brilliant prototype, learned something, deleted it.
Three months later: "Why did we choose that design?"
Nobody remembers.

- **Fix**: Before deletion, write the answer into `DESIGN.md` or an ADR (10 minutes).
- **Even better**: Link that ADR from the component's README.

---

## Quick Reference

| Scenario | Branch | Artifact | Effort |
|----------|--------|----------|--------|
| "Does this logic work?" | LOGIC.md | Interactive terminal | 30-90 min |
| "What should this look like?" | UI.md | 3-5 UI variants | 45-120 min |
| State/logic question, ambiguous context | LOGIC.md | See LOGIC.md | — |
| UI/design question, ambiguous context | UI.md | See UI.md | — |
| Not sure what you're asking | Stop → reread Step 1 | — | 5 min |

---

## References

This skill adapts the core prototype methodology from
[mattpocock/skills/prototype](https://github.com/mattpocock/skills/blob/main/skills/engineering/prototype/SKILL.md).

**Matt's version** is optimized for individual engineers shipping production code rapidly.

**This version (TecCat)** expands that framework for:
- **Team workflows**: shared documentation templates, code review integration
- **Extended duration**: tracking decisions across multiple prototypes and sprints
- **Cross-functional alignment**: helping non-engineers understand why you prototyped

**What we kept** from Matt's original:
- The core insight: "the question decides the shape"
- The two-branch routing (logic vs. UI)
- The discipline: throwaway from day 1, no persistence, no tests

**What we added** (original contributions):
- Step-by-step walkthrough for teams unfamiliar with the practice
- Structured README template with question + how-to + answer sections
- Detailed table-based decision framework
- Team code-review checklist
- Common failure modes and how to avoid them
- Version control guidance for team branches

Both versions share the same philosophy:
**write down your question first. That one sentence decides everything.**
