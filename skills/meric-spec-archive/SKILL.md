---
name: meric-spec-archive
description: Use this skill for Stage 5 (Archive) of the Meric-Spec workflow. Consolidates 01-proposal.md, 02-exploration.md, 03-apply.md, and 04-verification.md into a single self-contained file under specs/archived/, cleans up the temporary specs/active/ session folder, and updates specs/README.md so future AI agents immediately have full context.
---

# Stage 5: Archive (`meric-spec-archive`)

## Role & Objective

You are executing **Stage 5 (`Archive`)**—the final stage of the **Meric-Spec** workflow.

Your mission is to turn a verified, completed active spec folder (`specs/active/<YYYY-MM-DD-HHmm>-<slug>/` containing `01-proposal.md`, `02-exploration.md`, `03-apply.md`, and `04-verification.md`) into **one clean, self-contained permanent Markdown record** under `specs/archived/<YYYY-MM-DD-HHmm>-<slug>.md`, clean up the temporary `specs/active/<session>/` folder, and update `specs/README.md`—so that any future AI agent (or engineer) can read **one single file** and immediately have the exact context, rationale, conventions, file changes, and verification know-how of what was done.

---

## Strict Rules

1. **Require Passing Verification First:** Read `04-verification.md` before archiving and ensure `Overall Result: PASS`. If verification failed or `04-verification.md` does not exist, stop and run [`meric-spec-verify`](../meric-spec-verify/SKILL.md) first.
2. **Zero-Loss Knowledge Distillation:** Consolidate cleanly without losing critical facts: preserve exact file paths, added/changed symbols, user Q&A decisions, style/architecture conventions applied, test/build verification numbers, and gotchas for future agents.
3. **Clean Active Session Only (Preserve Workspace Markers):** Delete **only** the completed subfolder `specs/active/<YYYY-MM-DD-HHmm>-<slug>/` (keeping `specs/active/`, `specs/active/.gitkeep`, and any other unrelated active spec sessions untouched).
4. **Always Update `specs/README.md`:** Add a row to the `Archived Specifications Index` table pointing to `./archived/<YYYY-MM-DD-HHmm>-<slug>.md`.

---

## Step-by-Step Instructions

### 1. Read All Four Active Spec Files
Read from `specs/active/<YYYY-MM-DD-HHmm>-<slug>/`:
1. `01-proposal.md`
2. `02-exploration.md`
3. `03-apply.md`
4. `04-verification.md`

Confirm `04-verification.md` has `Overall Result: PASS`.

### 2. Write the Consolidated Archive File
Create `specs/archived/<YYYY-MM-DD-HHmm>-<slug>.md`:

```markdown
# Archived Spec: <Session Title>

- **Session ID:** `<YYYY-MM-DD-HHmm>-<slug>`
- **Proposed:** `<YYYY-MM-DD HH:mm>`
- **Archived:** `<YYYY-MM-DD HH:mm>`
- **Final Status:** `ARCHIVED & VERIFIED`

---

## 1. Executive Summary & User Intent
<Why this change was made, original proposal goals, scope boundaries, and key user Q&A decisions from 01-proposal.md.>

## 2. Codebase Exploration & Style Conventions Followed
- **Files & Subsystems Audited:** <Key files/callers verified in 02-exploration.md>
- **Style & Syntax Fingerprint Applied:** <Exact indentation, spacing, EOF newlines, patterns/helpers reused>

## 3. Exact Implementation Summary (What Was Built)
| File / Component | Symbols / Changes Applied | Rationale |
| :--- | :--- | :--- |
| `<exact/path/file.ext>` | `<symbolName>` (L10-L45) | <Summary of behavior implemented> |

## 4. Verification Proof & Traceability
- **Traceability Matrix:** <All N proposal goals verified `PASS`>
- **Formatting / Lint:** `<exact command & observed result>`
- **Build / Tests:** `<exact command, passed/failed/skipped counts, coverage/run ID if printed>`

## 5. Knowledge & Know-How for Future AI Agents
- **Entry Points & Architecture Notes:** <Where future changes should hook in>
- **Invariants & Gotchas to Preserve:** <Side effects, cleanup rules, edge-case guards, or config dependencies>
```

### 3. Register in `specs/README.md`
Update the `Archived Specifications Index` table in `specs/README.md` (replacing the initial placeholder row if this is the first archived spec):
```markdown
| [`<YYYY-MM-DD-HHmm>-<slug>.md`](./archived/<YYYY-MM-DD-HHmm>-<slug>.md) | `<YYYY-MM-DD>` | <Concise one-line summary> | `ARCHIVED & VERIFIED` |
```

### 4. Clean Up Active Session Folder
Delete `specs/active/<YYYY-MM-DD-HHmm>-<slug>/` (all four active staging files are now safely captured in `specs/archived/<YYYY-MM-DD-HHmm>-<slug>.md`). Verify `specs/active/.gitkeep` and `specs/archived/.gitkeep` remain in place, then report the exact path to the newly created archive file.

## Related Skills

* **Previous Stage:** [meric-spec-verify](../meric-spec-verify/SKILL.md)
* **Start New Spec Cycle:** [meric-spec-propose](../meric-spec-propose/SKILL.md)
* **Specs Directory Overview:** [`specs/README.md`](../../specs/README.md)
