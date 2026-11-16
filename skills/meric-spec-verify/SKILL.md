---
name: meric-spec-verify
description: Use this skill for Stage 4 (Confirmation & Verification) of the Meric-Spec workflow. Audits all applied files against every Proposal goal and Exploration checklist item, runs project formatter/lint/typecheck/test checks, writes a Traceability Matrix in 04-verification.md, and prompts the user to proceed to meric-spec-archive.
---

# Stage 4: Confirmation & Verification (`meric-spec-verify`)

## Role & Objective

You are executing **Stage 4 (`Verify`)** of the **Meric-Spec** workflow.

Your job is to act as an independent, skeptical verifier: prove with direct tool output and file inspection that **every requirement in `01-proposal.md`** and **every step in `02-exploration.md`** was completely implemented in `03-apply.md`, matches the repository's coding style, and passes objective verification checks—then invite the user to confirm archiving via **Stage 5 (`meric-spec-archive`)**.

---

## Strict Rules

1. **Evidence-Only Reporting:** NEVER state as fact any file edit, symbol name, formatter result, build output, or test pass that you did not directly observe in files read or tool outputs run *after* the final Stage 3 edit.
2. **100% Proposal-to-Code Traceability:** Every `- [ ] Goal` in `01-proposal.md` and every Step in `02-exploration.md` must have an explicit verification row in `04-verification.md`.
3. **Never Hide Failures or Skipped Checks:** If any requirement is missing, any linter/typecheck fails, or any unit test fails/is skipped, set `Overall Result: FAIL`, report exact findings, and offer to loop back to [`meric-spec-apply`](../meric-spec-apply/SKILL.md) rather than proceeding to Archive.
4. **Explicit Confirmation Before Archiving:** Once `Overall Result: PASS`, present the verification summary and give the user the choice to archive (when they reply **`archive`**, **`continue`**, **`next`**, or **`done`**, automatically invoke [`meric-spec-archive`](../meric-spec-archive/SKILL.md)). Never delete `specs/active/<session>/` until the user confirms.

---

## Step-by-Step Instructions

### 1. Cross-Check Proposal, Exploration, Apply & Actual Files
Read `01-proposal.md`, `02-exploration.md`, and `03-apply.md` inside `specs/active/<YYYY-MM-DD-HHmm>-<slug>/`. Then inspect each modified source/test/doc file on disk to confirm:
* Every requirement and boundary condition in `01-proposal.md` is satisfied.
* Every checklist item in `02-exploration.md` is `[x]` and matches actual code on disk.
* Formatting, spacing, EOF newlines, error handling, and scope rules were respected.

### 2. Run Objective Verification Commands
Execute the checks defined in `02-exploration.md` `## 4. Verification Plan`:
* Formatting & lint checks (e.g., `npm run prettier:verify`, `eslint`, `ruff check`, `gofmt`)
* Typecheck / build checks (e.g., `tsc --noEmit`, `npm run build`, `cargo check`)
* Unit / integration test suites (e.g., `npm test`, `pytest`, `go test ./...`, `sf apex run test`)

Record exact commands, exit codes, test counts (`passed / failed / skipped`), run IDs, and coverage metrics if printed.

### 3. Write `04-verification.md`
Create `specs/active/<YYYY-MM-DD-HHmm>-<slug>/04-verification.md`:

```markdown
# Verification Report: <Session Title>

- **Proposal Ref:** [`01-proposal.md`](./01-proposal.md)
- **Exploration Ref:** [`02-exploration.md`](./02-exploration.md)
- **Apply Ref:** [`03-apply.md`](./03-apply.md)
- **Verified At:** `<YYYY-MM-DD HH:mm>`
- **Overall Result:** `PASS` <!-- PASS | FAIL -->

## 1. End-to-End Traceability Matrix
| Proposal Goal | Exploration Step | Applied Implementation | Verification Evidence | Result |
| :--- | :--- | :--- | :--- | :--- |
| Goal 1 | Step 1 | `<path/file.ext>` (L10-L45) | Code inspected + check passed | `PASS` |
| Goal 2 | Step 2 | `<path/test.ext>` (L1-L78) | Test suite output observed | `PASS` |

## 2. Verification Commands & Observed Results
| Check Type | Command Executed | Result | Details |
| :--- | :--- | :--- | :--- |
| Formatting / Lint | `<command>` | `PASS` | `<exact observed output>` |
| Build / Typecheck | `<command>` | `PASS` | `<exact observed output>` |
| Tests | `<command>` | `PASS` | `<X/X passed, 0 failed, 0 skipped>` |

## 3. Deviations, Gaps, or Limitations
- *(None, or state exact unverified/mocked scopes honestly)*

## 4. Ready to Archive
- All Proposal goals and Exploration steps verified: **Yes / No**
- **Next Action:** Reply **`archive`** (or **`continue`**) to run `meric-spec-archive`, summarize all context into `specs/archived/<session>.md`, and clean up `specs/active/<session>/`.
```

### 4. Report Summary & Handle User Decision
* If `Overall Result` is `FAIL`: clearly explain what failed and ask the user whether to invoke [`meric-spec-apply`](../meric-spec-apply/SKILL.md) to resolve the gaps.
* If `Overall Result` is `PASS`: present the concise verification report and ask the user to type **`archive`** (or **`continue`** / **`next`**) to run Stage 5 ([`meric-spec-archive`](../meric-spec-archive/SKILL.md)). When they confirm, invoke `meric-spec-archive` immediately.

## Related Skills

* **Previous Stage:** [meric-spec-apply](../meric-spec-apply/SKILL.md)
* **Next Stage:** [meric-spec-archive](../meric-spec-archive/SKILL.md)
