---
name: meric-spec-apply
description: Use this skill for Stage 3 (Apply) of the Meric-Spec workflow. Sequentially executes every confirmed step in 02-exploration.md while matching the target codebase's exact indentation, spacing, newline, syntax, and architecture conventions, writes detailed change and build/test output logs to 03-apply.md, and automatically transitions to meric-spec-verify.
---

# Stage 3: Apply (`meric-spec-apply`)

## Role & Objective

You are executing **Stage 3 (`Apply`)** of the **Meric-Spec** workflow. You operate strictly from the confirmed `01-proposal.md` and `02-exploration.md` inside `specs/active/<YYYY-MM-DD-HHmm>-<slug>/`.

Your responsibility is to apply **every checklist item** in `02-exploration.md` one by one in order, match the existing codebase and connected environment's exact styling, spacing, newline conventions, and architectural patterns, write complete execution evidence to `03-apply.md` so Stage 4 (`meric-spec-verify`) can independently verify everything built, and transition seamlessly into `meric-spec-verify`.

---

## Strict Rules

1. **Verify Exploration Is Confirmed:** Check `- **Status:** CONFIRMED` in `02-exploration.md` (or ask the user to confirm first if still `PENDING_CONFIRMATION`) before editing code.
2. **Execute Checklist Items Sequentially (1-by-1):** Work through every `- [ ] Step N` in `02-exploration.md` in exact order. Mark each completed item `[x]` as you go. Do not skip steps silently or improvise unrelated refactors outside `01-proposal.md`'s scope.
3. **Preserve Exact Codebase Styling & Syntax:** Strictly follow `## 2. Codebase Style, Spacing & Architecture Fingerprint` from `02-exploration.md`:
   * Match indentation width, tabs vs. spaces, quote style, trailing commas, brace placement, blank lines between blocks, `LF`/`CRLF` line endings, and trailing EOF newlines.
   * Reuse existing helpers, base classes, error patterns, and docstrings rather than duplicating logic.
   * Run the project's formatter/linter command if configured (e.g., `prettier`, `eslint`, `ruff`, `gofmt`, `cargo fmt`) so zero formatting diffs remain.
4. **Zero-Hallucination Edits:** Only import, reference, or modify verified paths and symbols observed in `02-exploration.md` or read directly on disk.
5. **Write Complete Verification Inputs in `03-apply.md`:** Document exact modified file paths, line ranges, added/changed symbols, and raw command outputs (build, format, deploy, initial test runs) so Stage 4 can verify every deliverable cleanly.
6. **Automatic Transition:** Once all checklist items in `02-exploration.md` are marked `[x]` and `03-apply.md` is saved (or when the user types **`continue`**, **`next`**, or **`verify`**), **immediately invoke [`meric-spec-verify`](../meric-spec-verify/SKILL.md)**.

---

## Step-by-Step Instructions

### 1. Load Confirmed Spec Context
Read both `01-proposal.md` and `02-exploration.md` in `specs/active/<YYYY-MM-DD-HHmm>-<slug>/` so every goal, scope boundary, style rule, and step is loaded before your first edit.

### 2. Apply Every Step One by One
For each `- [ ] Step N` in `02-exploration.md`:
1. Inspect the exact target block on disk if not already in context.
2. Apply clean, modular, minimal edits matching the codebase's spacing, newline, naming, and architecture conventions.
3. Update or add unit/integration tests and companion metadata/config files listed in the step.
4. Mark the item `[x]` in `02-exploration.md`.

### 3. Run Formatter / Build Steps & Write `03-apply.md`
Run the project formatter/build steps noted in `02-exploration.md` and record everything in `specs/active/<YYYY-MM-DD-HHmm>-<slug>/03-apply.md`:

```markdown
# Apply Log: <Session Title>

- **Proposal Ref:** [`01-proposal.md`](./01-proposal.md)
- **Exploration Ref:** [`02-exploration.md`](./02-exploration.md)
- **Applied At:** `<YYYY-MM-DD HH:mm>`
- **Status:** `APPLIED` <!-- IN_PROGRESS | APPLIED -->

## 1. Completed Checklist Execution
| Step | Status | File(s) Touched & Line Ranges | Summary of Applied Change |
| :--- | :--- | :--- | :--- |
| Step 1 | Done | `<path/file.ext>` (L10-L45) | <Exact functions/types/changes implemented> |
| Step 2 | Done | `<path/test.ext>` (L1-L78) | <Exact test cases & fixtures added> |

## 2. Style, Spacing & Newline Compliance
- Matched `<indentation / spacing / EOF newline / sharing or error pattern>` from `02-exploration.md`.
- Formatter command executed: `<exact command & exit code>`

## 3. Build / Deploy / Raw Outputs (Inputs for Verification)
- **Command(s) Run:** `<e.g., npm run build / pytest / go build / sf project deploy>`
- **Observed Output Summary:** `<Exact exit code, artifact/deploy ID, or errors encountered & fixed>`
```

### 4. Auto-Transition to `meric-spec-verify`
Immediately proceed to Stage 4 ([`meric-spec-verify`](../meric-spec-verify/SKILL.md)) once all checklist steps are applied and `03-apply.md` is complete (unless the user explicitly asked to stop before verification).

## Related Skills

* **Previous Stage:** [meric-spec-explore](../meric-spec-explore/SKILL.md)
* **Next Stage:** [meric-spec-verify](../meric-spec-verify/SKILL.md)
