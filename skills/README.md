# Meric-Spec Skills Catalog

[![skills.sh](https://skills.sh/b/masaner/meric-spec)](https://www.skills.sh/masaner/meric-spec)

This folder contains **Meric-Spec**'s [skills.sh](https://skills.sh) skill catalog—a universal, language-agnostic **5-stage Spec-Driven Engineering Workflow** (`Propose → Explore → Apply → Verify → Archive`) for **Antigravity** ([skills.sh/agent/antigravity](https://www.skills.sh/agent/antigravity)), Claude Code, Cursor, GitHub Copilot, Codex, Gemini CLI, and other `skills.sh`-compatible AI agents.

See [`docs/how-to-use.md`](../docs/how-to-use.md) for a step-by-step walkthrough and example prompts.

## Installing These Skills

```bash
# Install all 5 workflow skills into your current repo (./.agents/skills/)
npx skills add masaner/meric-spec

# Install globally for Antigravity across every workspace on your machine (~/.agents/skills/)
npx skills add masaner/meric-spec -g --agent antigravity --skill '*' -y

# Preview skills without installing
npx skills add masaner/meric-spec --list
```

## Skills (`Propose → Explore → Apply → Verify → Archive`)

| Stage | Skill | Responsibility & Generated Artifact |
| :--- | :--- | :--- |
| **1. Propose** | [`meric-spec-propose`](./meric-spec-propose/SKILL.md) | Listens to user intent, initializes `specs/active/<YYYY-MM-DD-HHmm>-<slug>/01-proposal.md`, runs multi-round clarifying Q&A, and auto-transitions to **Explore** when confirmed. |
| **2. Explore** | [`meric-spec-explore`](./meric-spec-explore/SKILL.md) | Performs a strict zero-hallucination audit of relevant files & connected environments, records exact spacing/newline/style conventions, writes an ordered checklist in `02-exploration.md`, supports Q&A confirmation, and auto-transitions to **Apply**. |
| **3. Apply** | [`meric-spec-apply`](./meric-spec-apply/SKILL.md) | Executes every checklist item from `02-exploration.md` sequentially matching the codebase's exact coding style & conventions, writes evidence in `03-apply.md`, and auto-transitions to **Verify**. |
| **4. Verify** | [`meric-spec-verify`](./meric-spec-verify/SKILL.md) | Cross-checks every Proposal goal and Explore step against modified files & objective linter/test runs, writes a Traceability Matrix in `04-verification.md`, and invites the user to confirm **Archive**. |
| **5. Archive** | [`meric-spec-archive`](./meric-spec-archive/SKILL.md) | Verifies `PASS`, distills all 4 working files into one self-contained knowledge file at `specs/archived/<YYYY-MM-DD-HHmm>-<slug>.md` for future AI agents, deletes the active session folder, and updates `specs/README.md`. |

## Publishing & Contributing

`skills.sh` indexes this repository directly from [github.com/masaner/meric-spec](https://github.com/masaner/meric-spec) and uses [`skills.sh.json`](../skills.sh.json) to organize the catalog page. Every push to `main` runs [`.github/workflows/ci.yml`](../.github/workflows/ci.yml) to verify `skills.sh.json`, `SKILL.md` frontmatter, and relative Markdown links.
