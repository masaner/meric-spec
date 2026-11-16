---
name: meric-spec-explore
description: Use this skill for Stage 2 (Exploration) of the Meric-Spec workflow. Performs a strict zero-hallucination audit of the entire relevant codebase and connected environment, captures exact spacing/newline/style/syntax conventions, writes an ordered checklist in 02-exploration.md, supports confirmation Q&A, and automatically transitions to meric-spec-apply.
---

# Stage 2: Exploration (`meric-spec-explore`)

## Role & Objective

You are executing **Stage 2 (`Explore`)** of the **Meric-Spec** workflow, reading `01-proposal.md` in `specs/active/<YYYY-MM-DD-HHmm>-<slug>/` and writing `02-exploration.md`.

Your goal is to replace guesswork with verified facts before a single source line is changed:
1. Inspect every relevant file, module, caller, test, dependency manifest, and connected service/environment mentioned or implied by `01-proposal.md`.
2. Capture an exact **Codebase Style, Spacing & Architecture Fingerprint** so every line written in Stage 3 (`meric-spec-apply`) respects indentation, blank lines, trailing newlines, quotes, naming, error handling, and idiomatic patterns of that project.
3. Produce a **step-by-step ordered implementation checklist** tracing 100% of the goals from `01-proposal.md` to exact files and symbols.

---

## Strict Rules

1. **Zero Hallucinations Allowed:** NEVER invent file paths, class/function names, types, CLI flags, environment variables, database columns, or package versions. Every item recorded in `02-exploration.md` **must** come from direct file searches (`rg` / `grep`), `read_file`, or read-only environment inspection commands. If something does not exist or cannot be verified, state that explicitly.
2. **Read-Only Exploration:** Do not edit production source code during Stage 2; write **only** `specs/active/<YYYY-MM-DD-HHmm>-<slug>/02-exploration.md`.
3. **Style, Spacing & Newline Precision:** Always inspect project config files (`.prettierrc*`, `.eslintrc*`, `eslint.config.*`, `biome.json`, `pyproject.toml`, `ruff.toml`, `.editorconfig`, `rustfmt.toml`, `.clang-format`, `tsconfig.json`, `package.json`, CI workflows) **and** existing neighboring source files to record:
   * Tab vs. spaces and indent width (2 spaces, 4 spaces, tabs)
   * Quote style, semicolons, trailing commas, line width
   * Line endings (`LF` vs. `CRLF`), spacing between blocks/methods, and EOF trailing newline convention
   * Architectural patterns (error/exception conventions, state/config lifecycle, logging, sharing/auth checks, typing/docstrings)
   * Test framework, folder structure, mocking/fixture conventions, and test/build/lint commands
4. **Proposal Traceability:** Every `- [ ] Goal` in `01-proposal.md` must map to concrete steps in `02-exploration.md`.
5. **Multi-Round Confirmation & Auto-Transition:** Present findings and any technical decisions/questions to the user. Support multiple rounds of Q&A and update `02-exploration.md` after each round. When the user confirms (e.g., types **`continue`**, **`next`**, **`proceed`**, or **`apply`**), set `Status: CONFIRMED` in `02-exploration.md` and **immediately invoke [`meric-spec-apply`](../meric-spec-apply/SKILL.md)**.

---

## Step-by-Step Instructions

### 1. Read the Active Proposal
Open `specs/active/<YYYY-MM-DD-HHmm>-<slug>/01-proposal.md` and extract every confirmed goal, scope rule, and Q&A decision.

### 2. Audit the Relevant Codebase Thoroughly
1. Search across the repository for relevant entry points, callers, types/schemas, tests, and build/CI definitions.
2. Read the target sections of every relevant file and record exact file paths, line ranges, and symbol signatures.
3. Verify existing helper utilities or shared abstractions so Stage 3 reuses existing project helpers instead of duplicating logic.
4. Where applicable (e.g., databases, cloud environments, Salesforce orgs, APIs), inspect schema/runtime state using read-only commands without mutating state.

### 3. Capture the Style, Syntax & Tooling Fingerprint
Record concrete observed rules from config files and surrounding code so Stage 3 has an unambiguous style contract.

### 4. Write `02-exploration.md`
Create `specs/active/<YYYY-MM-DD-HHmm>-<slug>/02-exploration.md`:

```markdown
# Exploration: <Session Title>

- **Proposal Ref:** [`01-proposal.md`](./01-proposal.md)
- **Explored At:** `<YYYY-MM-DD HH:mm>`
- **Status:** `PENDING_CONFIRMATION` <!-- PENDING_CONFIRMATION | IN_QA | CONFIRMED -->

## 1. Verified Codebase & Environment Audit (Observed Only)
| Artifact Path | Symbols & Lines Observed | Existing Behavior & Constraints |
| :--- | :--- | :--- |
| `<exact/path/file.ext>` | `symbolName` (L12-L48) | <Observed facts only> |

* **Dependencies / Tooling / Connected Env Observed:** <Verified versions, scripts in `package.json` / `pyproject.toml`, connected org/DB notes, or "Local repository only">

## 2. Codebase Style, Spacing & Architecture Fingerprint
- **Formatter / Linter Config:** <e.g., `.prettierrc` / `ruff` / `gofmt` / exact CLI scripts>
- **Indentation & Spacing:** <e.g., 2 spaces, single blank line between functions, trailing newline at EOF, `LF` line endings>
- **Syntax & Architectural Conventions:** <Type annotations, docstrings, error handling, auth/permissions, existing helpers to reuse>
- **Testing Conventions:** <Test runner, fixture patterns, directory placement, CI workflows>

## 3. Proposal Traceability & Step-by-Step Implementation Checklist
- [ ] **Step 1 — `<exact/path/file.ext>` (`Proposal Goal #1`):** <Exact change, signature, helper reuse, style notes>
- [ ] **Step 2 — `<exact/path/test.ext>` (`Proposal Goal #2`):** <Exact unit/integration tests and assertions to add>
- [ ] **Step 3 — Documentation / Config (`Proposal Goal #3`):** <Docs, types, migrations, or config updates in scope>

## 4. Verification Plan
- **Format / Lint Commands:** `<exact commands observed in repo>`
- **Typecheck / Build / Test Commands:** `<exact commands observed in repo>`

## 5. Technical Questions / Confirmations Needed
- *(None, or list specific technical choices for the user to confirm before Apply runs)*
```

### 5. User Confirmation & Auto-Transition to `meric-spec-apply`
Present a concise summary of observed files, the coding style fingerprint, the ordered checklist, and any open questions. Update `02-exploration.md` through any additional Q&A rounds.

Once the user confirms (`continue`, `next`, `proceed`, `apply`, or `approved`):
1. Update `- **Status:**` in `02-exploration.md` to `CONFIRMED`.
2. Immediately load and execute [`meric-spec-apply`](../meric-spec-apply/SKILL.md) on the active session folder.

## Related Skills

* **Previous Stage:** [meric-spec-propose](../meric-spec-propose/SKILL.md)
* **Next Stage:** [meric-spec-apply](../meric-spec-apply/SKILL.md)
