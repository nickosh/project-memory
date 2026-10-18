# project-memory

Reusable GitHub template and reference layout for evidence-based project memory in agent-assisted repositories.

## Layout

```text
.
├── .agents/
│   └── skills/
│       └── project-closeout/
│           └── SKILL.md     # Evidence-based session/milestone closeout skill
├── docs/
│   ├── PRODUCT.md           # Vision, target users, core invariants, non-goals
│   ├── PLAN.md              # Authoritative task, slice/milestone sequence, and acceptance ledger
│   ├── DECISIONS.md         # Numbered ADR-style design and owner decisions (D01, D02, ...)
│   ├── EDGE_CASES.md        # Boundary-case resolution ledger (ADR, fix, doc, PARTIAL, OPEN)
│   └── JOURNAL.md           # Newest-first cross-session progress log (2–5 bullets per entry)
├── AGENTS.md                # Repository-wide agent instructions, verification, and Git rules
├── CLAUDE.md -> AGENTS.md   # Symlink for Claude Code compatibility
└── LICENSE                  # MIT
```

## Core principles

1. **Evidence over claims:** Tasks in `docs/PLAN.md` are marked complete only when implementation and verification evidence exist. Unrun or blocked checks stay explicit.
2. **Specs are hypotheses:** When implementation or owner review changes behavior, update the matching specification or contract in the same change as the code.
3. **Append-only decision & edge-case ledgers:** New decisions allocate the next `Dxx` ID and explicitly supersede older decisions rather than rewriting history. Edge cases (`ECxx`) remain `OPEN` until behavior and tests land—never "resolved by documentation."
4. **Clean separation from delivery bookkeeping:** Project memory tracks product behavior, engineering decisions, verified outcomes, blockers, and the next concrete technical action. Branch names, commit SHAs, PR states, CI run IDs, and publication dates stay in Git history and GitHub Releases/tags.
5. **Proportional verification & structured commits:** Every coherent change is verified (`git diff --check` for docs; test/lint/typecheck suites for code), reconciled through `.agents/skills/project-closeout/SKILL.md`, and committed using Conventional Commits with a factual body.

## Initializing a new project

1. **Create or copy:** Use this repository as a GitHub template or copy `AGENTS.md`, `CLAUDE.md`, `docs/`, and `.agents/` into the target repository root.
2. **Replace placeholders:**
   - Replace `<PROJECT_NAME>` across `AGENTS.md` and `docs/*.md` with the repository name.
   - Replace `<YYYY-MM-DD>` in `docs/PRODUCT.md`, `docs/PLAN.md`, `docs/DECISIONS.md`, and `docs/JOURNAL.md` with the initialization date.
3. **Confirm workflow decisions in `docs/DECISIONS.md`:**
   - `D01` sets the default **Hybrid layout** (`PRODUCT.md`, `PLAN.md`, `DECISIONS.md`, `EDGE_CASES.md`, `JOURNAL.md`).
   - `D02` sets the default **Local auto-commit workflow** (auto-commit locally after verified changes and closeout; require explicit permission for push/tag/PR). If you prefer manual commit authorization on a project, edit `D02`, `AGENTS.md`, and `.agents/skills/project-closeout/SKILL.md` accordingly.
4. **Define the project (`M0.2`):** Populate `docs/PRODUCT.md` (one-liner, problem, target users, core invariants, non-goals), add architecture and verification commands to `AGENTS.md`, and replace this `README.md` with the project's public documentation.

## Adapting the layout to project scale

- **Lean profile** (small utilities, skill bundles, libraries): Drop `docs/PRODUCT.md` and `docs/EDGE_CASES.md` if `AGENTS.md` and `docs/PLAN.md` cover product scope and boundary cases directly; remove their rows from `AGENTS.md` and `.agents/skills/project-closeout/SKILL.md`.
- **Full specification profile** (engines, multi-component systems, strict compliance): Add domain specification files under `docs/`, plus optional ledgers:
  - `docs/REQUIREMENTS.md` — numbered functional/non-functional requirements (`FR-1xx`, `NFR-xx`) traced to specs and ticked only in the change that lands their test.
  - `docs/RELEASING.md` — versioning scheme, pre-release checkpoints, dry-run gates, and tag-driven publishing rules.
