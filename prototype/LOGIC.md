# LOGIC Prototype Branch

A tiny interactive terminal app that lets the user drive a state model by hand.

Use this when the question is about **business logic, state transitions, or data
shape** — the kind of thing that looks reasonable on paper but only feels wrong
once you push it through real cases.

**Trigger phrases:**
- "I'm not sure if this state machine handles the edge case where X then Y."
- "Does this data model actually let me represent the case where..."
- "I want to feel out what the API should look like before writing it."
- Anything where the user wants to press buttons and watch state change.

If the question is "what should this look like" — wrong branch. Use [UI.md](./UI.md).

---

## Before Writing Code

Write down two things (in the prototype README or a comment at the top of the file):

1. **The state model** — what data are we driving?
2. **The question** — what are we trying to learn?

A logic prototype that answers the wrong question is pure waste. Make the question
explicit so it can be checked later, whether the user is watching now or returning
to it AFK.

---

## Building the Terminal App

### Structure

```
prototype-<name>/
├── README.md        ← question + how to run + ## Answer (blank)
├── index.ts         ← main loop
├── state.ts         ← state model + transitions
└── actions.ts       ← named user actions
```

### Implementation Rules

**State lives in memory — one object, printed in full after every action.**

```typescript
// state.ts — define the full state shape first
type State = {
  // ... your model
}

const initialState: State = { /* ... */ }
```

**Main loop pattern:**

```typescript
// index.ts
import * as readline from "readline";
import { State, initialState } from "./state";
import { actions } from "./actions";

let state: State = initialState;

function printState(s: State) {
  console.clear();
  console.log("=== STATE ===");
  console.log(JSON.stringify(s, null, 2));
  console.log("\n=== ACTIONS ===");
  Object.keys(actions).forEach((key, i) => console.log(`  ${i + 1}. ${key}`));
}

const rl = readline.createInterface({ input: process.stdin });
printState(state);

rl.on("line", (input) => {
  const index = parseInt(input.trim()) - 1;
  const actionName = Object.keys(actions)[index];
  if (actionName && actions[actionName]) {
    state = actions[actionName](state);
  }
  printState(state);
});
```

**Actions pattern — pure functions, no side effects:**

```typescript
// actions.ts
import { State } from "./state";

export const actions: Record<string, (s: State) => State> = {
  "action name here": (state) => ({
    ...state,
    // ... updated fields
  }),
};
```

### Running

Use whatever runtime fits the project:

```bash
# TypeScript
npx tsx index.ts

# JavaScript
node index.js

# Python (if that's your stack)
python main.py
```

---

## Constraints

- **No tests** — if you're writing tests, stop. This is a prototype.
- **No database** — in-memory only, unless the question IS about persistence.
- **No generalisation** — one question, one state model.
- **No blur between logic and UI** — the terminal IS the UI here. Keep it text-only.
- **Print full state** — after every action, show everything. No partial diffs.

---

## When You Have the Answer

1. Fill in the `## Answer` section of the prototype README.
2. Capture it somewhere durable (ADR, issue, commit message).
3. Delete the prototype directory.

If the user is around: ask what the prototype taught them.
If not: leave a `NOTES.md` so the answer can be filled in before deletion.
