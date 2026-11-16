---
name: meric-spec-propose
description: Use this skill to start Stage 1 (Proposal) of a spec-driven workflow for any codebase. Captures user intent, scaffolds specs/active/<timestamp>-<slug>/01-proposal.md, runs multi-round clarifying Q&A, updates the proposal on each answer, and automatically transitions to meric-spec-explore when the user confirms.
---

# Stage 1: Proposal (`meric-spec-propose`)

## Role & Objective

You are executing **Stage 1 (`Propose`)** of the universal **Meric-Spec** engineering workflow:

`Propose (01-proposal.md)` → `Explore (02-exploration.md)` → `Apply (03-apply.md)` → `Verify (04-verification.md)` → `Archive (specs/archived/<session>.md)`

This workflow works for **any language, framework, or platform** (TypeScript, React/Next/Astro, Python, Go, Rust, Java, C#, Salesforce Apex/LWC, SQL, DevOps/CI). Your job in Stage 1 is to listen carefully to the user's intent, define concrete goals and boundaries, resolve ambiguities through one or more rounds of clarifying Q&A, and prepare a crisp, unambiguous `01-proposal.md` before codebase exploration begins.

---

## Strict Rules

1. **Zero Hallucinations:** Never claim a file, symbol, endpoint, database schema, or config option exists unless you have read it directly on disk. Leave deep codebase auditing to Stage 2 (`meric-spec-explore`), doing at most a quick sanity check if needed to ask sharper clarifying questions.
2. **Do Not Modify Production Code Yet:** Stage 1 writes **only** inside `specs/` (`specs/README.md`, `specs/active/.gitkeep`, `specs/archived/.gitkeep`, and `specs/active/<YYYY-MM-DD-HHmm>-<slug>/01-proposal.md`).
3. **Multi-Round Clarifying Q&A:** Anticipate multiple rounds of questions. Whenever the user answers or refines requirements, update `01-proposal.md` with their exact decisions before asking follow-up questions or concluding.
4. **Automatic Transition:** Once all open questions are answered *and* the user confirms or says **`continue`**, **`next`**, **`proceed`**, or **`explore`**, mark `Status: CONFIRMED` in `01-proposal.md` and **immediately invoke [`meric-spec-explore`](../meric-spec-explore/SKILL.md)** on the active session folder without waiting for a separate command.

---

## Step-by-Step Instructions

### 1. Ensure `specs/` Workspace Structure Exists
If `specs/` does not yet exist in the target repository, initialize cleanly:
* `specs/active/.gitkeep`
* `specs/archived/.gitkeep`
* `specs/README.md` (with an `Archived Specifications Index` table)

Check `specs/active/` to see if the user is resuming an existing active proposal or starting a new one.

### 2. Create the Timestamped Session Folder & `01-proposal.md`
Generate a time-coded, subject-named folder using current wall-clock time and a short kebab-case slug:
`specs/active/<YYYY-MM-DD-HHmm>-<subject-slug>/`

Create `specs/active/<YYYY-MM-DD-HHmm>-<subject-slug>/01-proposal.md`:

```markdown
# Proposal: <Clear, Concise Title>

- **Session ID:** `<YYYY-MM-DD-HHmm>-<subject-slug>`
- **Created At:** `<YYYY-MM-DD HH:mm>`
- **Status:** `IN_QA` <!-- DRAFT | IN_QA | CONFIRMED -->
- **Stack / Domain:** <e.g., TypeScript + Astro / Python FastAPI / Salesforce Apex / Full-Stack>

## 1. User Intent & Problem Statement
<Accurate summary of what the user wants to build, fix, or refactor and why.>

## 2. Proposed Goals & Success Criteria
- [ ] <Goal 1 — concrete, testable requirement>
- [ ] <Goal 2 — concrete, testable requirement>

## 3. Scope Boundaries
- **In Scope:** <Target features, modules, docs, tests, deployments>
- **Out of Scope:** <Explicit non-goals to prevent scope creep>

## 4. Candidate Target Areas (Unverified Until Explore)
- <Directories, services, endpoints, components, or tools mentioned by the user>

## 5. Clarifying Q&A Log
### Round 1
- **Q1:** <Question>
  - **Answer:** *(Pending)*
```

### 3. Run Clarifying Q&A (1 or More Rounds)
Ask concise, high-signal questions covering decisions that could branch implementation—such as:
* Functional edge cases, error/fallback behavior, backward compatibility, or API contracts
* Target runtime constraints, dependencies, auth/security requirements, or connected environments
* Verification expectations (unit tests, integration tests, build/lint commands, live environment checks)

Each time the user replies:
* Record answers under `## 5. Clarifying Q&A Log` (`### Round 1`, `### Round 2`, ...).
* Refine Sections 1–3 (`Goals`, `Scope Boundaries`) to lock in every confirmed decision.
* Ask follow-up questions if ambiguity remains; once everything is clear, present the finalized Proposal summary and tell the user to reply **`continue`** (or **`next`**) to run **Stage 2: Exploration (`meric-spec-explore`)**.

### 4. Auto-Transition to `meric-spec-explore`
When the user replies **`continue`**, **`next`**, **`proceed`**, **`explore`**, or confirms the proposal:
1. Update `- **Status:**` in `01-proposal.md` to `CONFIRMED`.
2. Immediately load and execute [`meric-spec-explore`](../meric-spec-explore/SKILL.md) on `specs/active/<YYYY-MM-DD-HHmm>-<subject-slug>/`.

## Related Skills

* **Next Stage:** [meric-spec-explore](../meric-spec-explore/SKILL.md) — Stage 2 codebase & style audit.
* **Overview:** [skills/README.md](../README.md) & [How-To Guide](../../docs/how-to-use.md).
