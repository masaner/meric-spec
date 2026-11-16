# Specifications Workspace (`specs/`)

This directory structure demonstrates how **Meric-Spec** manages in-progress work and permanent project memory across **any** codebase:

```text
specs/
├── README.md                              # Index of active and archived specifications
├── active/                                # In-progress sessions (created per proposal timestamp & subject)
│   ├── .gitkeep
│   └── <YYYY-MM-DD-HHmm>-<slug>/
│       ├── 01-proposal.md                 # Stage 1: Intent, goals, scope & Q&A decisions (meric-spec-propose)
│       ├── 02-exploration.md              # Stage 2: Zero-hallucination audit, style fingerprint & checklist (meric-spec-explore)
│       ├── 03-apply.md                    # Stage 3: Step-by-step execution log & command outputs (meric-spec-apply)
│       └── 04-verification.md             # Stage 4: Traceability matrix & test verification evidence (meric-spec-verify)
└── archived/                              # Permanent single-file summaries for future AI agents
    ├── .gitkeep
    └── <YYYY-MM-DD-HHmm>-<slug>.md        # Stage 5: Consolidated knowledge & know-how (meric-spec-archive)
```

---

## Folder Lifecycle

1. **`specs/active/<YYYY-MM-DD-HHmm>-<slug>/`** holds the four active Markdown artifacts (`01-proposal.md` through `04-verification.md`) while work is being clarified, explored, implemented, and verified.
2. **`specs/archived/<YYYY-MM-DD-HHmm>-<slug>.md`** stores the single consolidated archive file produced by `meric-spec-archive` once verification passes—removing the temporary `specs/active/<session>/` folder while preserving exact know-how for future AI agent sessions.

---

## Archived Specifications Index

| Archive File | Date | Subject / Intent | Status |
| :--- | :--- | :--- | :--- |
| *(None yet — start a session in your repo with `meric-spec-propose`)* | — | — | — |
