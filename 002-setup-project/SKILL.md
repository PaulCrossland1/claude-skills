---
name: 002-setup-project
description: Transform a PRD into an executable project scaffold with sequential tasks. Generates tasks.json (task breakdown), ARCHITECTURE.md (technical blueprint), CONTEXT.md (agent briefing), and supporting docs. Use after /001-scope-project to prepare a project for AI-driven development. Invoke with /project-setup.
---

# Project Setup — PRD to Executable Tasks

Transform a completed PRD into an executable project structure with sequential tasks that subagents can complete.

## What This Skill Generates

```
project-name/
├── .claude/                    # AI orchestration
│   ├── tasks.json              # Sequential task breakdown
│   ├── CONTEXT.md              # Current state (agent reads first)
│   ├── PROGRESS-NOTES.md       # Append-only work log
│   └── BLOCKERS.md             # Human intervention needed
├── docs/
│   ├── PRD.md                  # Original PRD
│   ├── ARCHITECTURE.md         # Technical blueprint
│   ├── ENV-SETUP.md            # Environment requirements
│   └── DECISIONS.md            # Architecture decisions
└── [empty project structure]
```

## Workflow

### 1. Locate PRD

Ask user for PRD location if not obvious:
```json
{
  "questions": [{
    "question": "Where is the PRD file?",
    "header": "PRD Location",
    "options": [
      {"label": "In current directory", "description": "PRD.md or similar in cwd"},
      {"label": "Specify path", "description": "I'll provide the path"}
    ],
    "multiSelect": false
  }]
}
```

### 2. Confirm Project Directory

```json
{
  "questions": [{
    "question": "Where should the project be created?",
    "header": "Project Path",
    "options": [
      {"label": "Current directory", "description": "Create here"},
      {"label": "New subdirectory", "description": "Create project-name/ folder"},
      {"label": "Specify path", "description": "I'll provide the path"}
    ],
    "multiSelect": false
  }]
}
```

### 3. Generate Architecture Document

Read PRD and generate `docs/ARCHITECTURE.md`:
- Extract tech stack decisions
- Map data models
- Document API design
- Create file structure plan

Use template from [document-templates.md](references/document-templates.md).

### 4. Generate Task Breakdown

Read PRD and generate `.claude/tasks.json`:

**Follow methodology in [task-generation.md](references/task-generation.md)**:

1. **Identify phases** from PRD sections
2. **Extract components** per phase
3. **Order by dependency** (foundation → data → core → api → ui → test)
4. **Write success criteria** (every task must be verifiable)

**Use schema from [task-schema.md](references/task-schema.md)**.

Typical project has 20-40 tasks across phases:
- foundation: 3-5 tasks
- data-layer: 3-5 tasks
- core: 5-10 tasks
- api: 3-5 tasks
- ui: 5-10 tasks
- testing: 2-4 tasks

### 5. Generate Supporting Documents

Create remaining docs using templates from [document-templates.md](references/document-templates.md):

- `.claude/CONTEXT.md` — Initial state summary
- `.claude/PROGRESS-NOTES.md` — Empty log ready for entries
- `.claude/BLOCKERS.md` — Empty blockers file
- `docs/ENV-SETUP.md` — Environment requirements from PRD
- `docs/DECISIONS.md` — Initial architecture decisions

### 6. Create Project Structure

Create empty directories matching ARCHITECTURE.md file structure.

### 7. Output Summary

Present what was created:
```
✓ Created project structure at /path/to/project

Generated:
- tasks.json: [X] tasks across [Y] phases
- ARCHITECTURE.md: Technical blueprint
- CONTEXT.md: Initial agent briefing
- PROGRESS-NOTES.md: Ready for logging
- ENV-SETUP.md: Environment requirements

Next steps:
1. Review tasks.json and adjust if needed
2. Set up environment per ENV-SETUP.md
3. Run first task with: [next skill/command]
```

---

## Task Generation Rules

### Atomicity
Each task completable in single agent session (~15-30 min).

**Too big**: "Build authentication system"
**Right size**: "Create User model and Prisma schema"

### Verifiability
Every task has automated success criteria:
- `file_exists` — Check file/directory
- `command_succeeds` — Run command, check exit 0
- `type_checks` — TypeScript compiles
- `test_passes` — Specific tests pass

See [task-schema.md](references/task-schema.md) for all criteria types.

### Sequential Ordering
Tasks execute in order. Each task's `depends_on` references prior tasks.

```
T001 (setup) → T002 (types) → T003 (models) → T004 (api) → T005 (ui)
```

### Complexity Estimation
| Complexity | Duration | Example |
|------------|----------|---------|
| trivial | <5 min | Config file change |
| simple | 5-15 min | Single model/component |
| moderate | 15-30 min | Feature with multiple files |
| complex | 30-60 min | Integration, significant logic |

---

## CONTEXT.md Purpose

**This is the most important file for agent continuity.**

Each subagent starts fresh. CONTEXT.md tells it:
- What the project is
- What's been built
- What files exist
- Current task
- Key decisions made

Update CONTEXT.md after each task completion.

---

## References

- **[task-schema.md](references/task-schema.md)** — JSON schema, success criteria types
- **[document-templates.md](references/document-templates.md)** — Templates for all generated docs
- **[task-generation.md](references/task-generation.md)** — PRD-to-tasks methodology
