# Project Protocol — Subagent Communication

This document defines how subagents interact with projects created via `/002-setup-project`.

---

## Project Structure (Standard)

**All project documentation lives under `.claude/`** — single source of truth:

```
project-name/
├── .claude/                    # All project metadata & documentation
│   ├── PRD.md                  # Product requirements (from 001)
│   ├── ARCHITECTURE.md         # Technical blueprint
│   ├── DECISIONS.md            # Architecture decisions
│   ├── ENV-SETUP.md            # Environment requirements
│   ├── tasks.json              # Sequential task breakdown
│   ├── CONTEXT.md              # Current state (READ FIRST)
│   ├── PROGRESS-NOTES.md       # Append-only work log
│   └── BLOCKERS.md             # Human intervention needed
└── [project source files]
```

---

## Subagent Execution Protocol

### 1. Orientation (Always First)

Read `.claude/CONTEXT.md` to understand:
- What the project is
- What's been built
- Current state
- Key decisions made

### 2. Task Loading

Read the specific task from `.claude/tasks.json`:
```json
{
  "id": "T005",
  "name": "Task name",
  "description": "What to do",
  "context_files": ["files to read"],
  "output_files": ["files to create/modify"],
  "success_criteria": [...]
}
```

### 3. Context Loading

Read all files listed in `context_files`:
- PRD sections if referenced
- Architecture docs if referenced
- Existing code files if referenced

### 4. Task Execution

Complete the work as described in the task:
- Create files listed in `output_files`
- Follow patterns from ARCHITECTURE.md
- Stay within task scope (don't do extra work)

### 5. Success Verification

Run all `success_criteria` checks:
- Execute commands
- Verify files exist
- Confirm tests pass

### 6. Documentation Updates

**Update `.claude/PROGRESS-NOTES.md`** (append):
```markdown
---

### [T005] Task Name

**Status**: Completed ✓
**Completed**: 2024-01-15T14:30:00Z

**Actions Taken**:
- Created User model
- Added Prisma schema

**Files Created**:
- `src/models/User.ts`

**Files Modified**:
- `prisma/schema.prisma`

**Issues**: None

**Notes**: [Any relevant context]

---
```

**Update `.claude/CONTEXT.md`**:
- Update "What's Been Built" section
- Update "Current Task" to next task
- Update progress counter
- Add any new decisions made

**Update `.claude/tasks.json`**:
- Set task `status`: "completed"
- Set `completed_at`: timestamp
- Add `notes` if relevant

### 7. Emit Completion Signal

At the END of response, emit structured signal:

```
--- TASK COMPLETION ---
task_id: T005
task_name: Create User model
status: completed
duration_minutes: 15

files_created:
  - src/models/User.ts
  - prisma/migrations/001_user.sql

files_modified:
  - prisma/schema.prisma
  - package.json

success_criteria:
  - [PASS] file_exists: src/models/User.ts
  - [PASS] file_contains: prisma/schema.prisma → "model User"
  - [PASS] command_succeeds: npx prisma validate

blocker: none

notes: |
  Created User model with all fields from PRD.
  Added email unique constraint.
  Migration ready to run.

context_updated: true
progress_notes_updated: true
tasks_json_updated: true

simplification_requested: true

next_task: T006
--- END COMPLETION ---

Please verify the work and run the code simplifier across the modified files.
```

---

## Completion Signal Schema

```yaml
--- TASK COMPLETION ---
task_id: string          # T001, T002, etc.
task_name: string        # Human readable name
status: enum             # completed | blocked | failed
duration_minutes: number # Approximate time spent

files_created:           # New files created
  - path/to/file

files_modified:          # Existing files changed
  - path/to/file

success_criteria:        # Results of verification
  - [PASS|FAIL] criterion_type: target

blocker: string | none   # If blocked, describe why

notes: string            # Free-form notes about the work

context_updated: boolean        # Did you update CONTEXT.md?
progress_notes_updated: boolean # Did you update PROGRESS-NOTES.md?
tasks_json_updated: boolean     # Did you update tasks.json?

simplification_requested: boolean  # Request code simplification pass

next_task: string | null # Next task ID, or null if done/blocked
--- END COMPLETION ---
```

---

## Status Values

| Status | Meaning | Next Action |
|--------|---------|-------------|
| `completed` | Task done, all criteria pass | Proceed to next_task |
| `blocked` | Cannot proceed, needs human | Stop, review blocker |
| `failed` | Attempted but criteria failed | Review, may retry |

---

## Blocker Handling

If a task cannot be completed:

1. **Document the blocker** in `.claude/BLOCKERS.md`:
```markdown
### [B001] Missing API Key

**Severity**: High
**Blocking Tasks**: T005, T006
**Discovered**: 2024-01-15T14:30:00Z

**Description**:
Cannot proceed with auth integration - CLERK_SECRET_KEY not set.

**Required Action**:
- [ ] User must create Clerk account
- [ ] User must add CLERK_SECRET_KEY to .env.local
```

2. **Update task status** to `blocked` with `blocked_reason`

3. **Emit completion signal** with `status: blocked`

---

## Completion Signal Parsing

You (the human, via 003-execute-tasks) should:

1. **Find the completion signal** by searching for `--- TASK COMPLETION ---`
2. **Parse YAML content** between delimiters
3. **Verify updates** were made (check booleans)
4. **Decide next action**:
   - `completed` → Run next task when ready
   - `blocked` → Resolve blocker before continuing
   - `failed` → Review and decide how to proceed

---

## Example: Full Subagent Response

```markdown
I'll complete task T005: Create User model.

## Reading Context

[Reads CONTEXT.md, understands project state]

## Task Details

Creating User model with fields:
- id (UUID)
- email (unique)
- created_at
- last_login

## Implementation

[Creates files, shows code]

## Verification

Running success criteria:
✓ file_exists: src/models/User.ts
✓ prisma validate passes

## Updates

Updated PROGRESS-NOTES.md with task log.
Updated CONTEXT.md with new state.
Updated tasks.json to mark T005 complete.

--- TASK COMPLETION ---
task_id: T005
task_name: Create User model
status: completed
duration_minutes: 12

files_created:
  - src/models/User.ts

files_modified:
  - prisma/schema.prisma

success_criteria:
  - [PASS] file_exists: src/models/User.ts
  - [PASS] command_succeeds: npx prisma validate

blocker: none

notes: |
  Created User model per PRD spec.
  Added unique constraint on email.

context_updated: true
progress_notes_updated: true
tasks_json_updated: true

next_task: T006
--- END COMPLETION ---
```
