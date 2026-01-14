# Task Prompt Template

This template is used to generate prompts for project task execution.

---

## Template Structure

```markdown
# Project Task: {TASK_ID} — {TASK_NAME}

You are a development agent working on **{PROJECT_NAME}**.

## Your Mission

Complete task **{TASK_ID}**: {TASK_NAME}

{TASK_DESCRIPTION}

---

## Project Context

{CONTEXT_MD_CONTENTS}

---

## Task Specification

**Task ID**: {TASK_ID}
**Category**: {CATEGORY}
**Phase**: {PHASE}
**Complexity**: {COMPLEXITY}
**Depends On**: {DEPENDS_ON}

### Files to Read First
{CONTEXT_FILES_LIST}

### Files to Create/Modify
{OUTPUT_FILES_LIST}

### Success Criteria
{SUCCESS_CRITERIA_LIST}

---

## Execution Requirements

1. **Read the context files** listed above before starting
2. **Follow patterns** from .claude/ARCHITECTURE.md
3. **Stay within scope** — only do what this task requires
4. **Verify your work** by running the success criteria
5. **Update documentation**:
   - Append to `.claude/PROGRESS-NOTES.md`
   - Update `.claude/CONTEXT.md` with new state
   - Mark task complete in `.claude/tasks.json`

---

## Completion Signal

When finished, emit this EXACT format at the END of your response:

```
--- TASK COMPLETION ---
task_id: {TASK_ID}
task_name: {TASK_NAME}
status: [completed|blocked|failed]
duration_minutes: [estimated minutes spent]

files_created:
  - [list each file created]

files_modified:
  - [list each file modified]

success_criteria:
  - [PASS|FAIL] [criterion description]

blocker: [none OR description of blocker]

notes: |
  [Brief summary of what was done]

context_updated: [true|false]
progress_notes_updated: [true|false]
tasks_json_updated: [true|false]

next_task: [{NEXT_TASK_ID}|null]
--- END COMPLETION ---
```

This completion signal is REQUIRED for tracking progress.

---

## Important Rules

- DO NOT skip the completion signal
- DO NOT do work beyond this task's scope
- DO update all three documentation files
- DO run success criteria before marking complete
- If blocked, describe the blocker clearly and set status: blocked
```

---

## Variable Substitution

| Variable | Source |
|----------|--------|
| `{PROJECT_NAME}` | `tasks.json → project.name` |
| `{TASK_ID}` | `tasks.json → tasks[n].id` |
| `{TASK_NAME}` | `tasks.json → tasks[n].name` |
| `{TASK_DESCRIPTION}` | `tasks.json → tasks[n].description` |
| `{CATEGORY}` | `tasks.json → tasks[n].category` |
| `{PHASE}` | `tasks.json → tasks[n].phase` |
| `{COMPLEXITY}` | `tasks.json → tasks[n].estimated_complexity` |
| `{DEPENDS_ON}` | `tasks.json → tasks[n].depends_on` |
| `{CONTEXT_FILES_LIST}` | Bulleted list of `context_files` |
| `{OUTPUT_FILES_LIST}` | Bulleted list of `output_files` |
| `{SUCCESS_CRITERIA_LIST}` | Formatted success criteria |
| `{CONTEXT_MD_CONTENTS}` | Contents of `.claude/CONTEXT.md` |
| `{NEXT_TASK_ID}` | Next pending task ID |

---

## Example: Generated Prompt

```markdown
# Project Task: T005 — Create User model

You are a development agent working on **genetic-kart**.

## Your Mission

Complete task **T005**: Create User model

Define the User entity with Prisma schema and TypeScript interface. Include fields: id (UUID), email (unique string), created_at (timestamp), last_login (nullable timestamp).

---

## Project Context

# Genetic Kart — Current Context

**Last Updated**: 2024-01-15T10:00:00Z
**Current Task**: T005 Create User model
**Progress**: 4/25 tasks completed

## What's Been Built

### Completed
- [x] Project initialization (T001)
- [x] TypeScript configuration (T002)
- [x] Prisma setup (T003)
- [x] Supabase connection (T004)

### In Progress
- [ ] User model (T005) ← YOU ARE HERE

[... rest of CONTEXT.md ...]

---

## Task Specification

**Task ID**: T005
**Category**: data
**Phase**: data-layer
**Complexity**: simple
**Depends On**: T004

### Files to Read First
- .claude/PRD.md (section 4: Data Models)
- .claude/ARCHITECTURE.md (section: Data Models)
- prisma/schema.prisma

### Files to Create/Modify
- shared/types/User.ts
- prisma/schema.prisma

### Success Criteria
- `file_exists`: shared/types/User.ts
- `file_contains`: prisma/schema.prisma → "model User"
- `command_succeeds`: npx prisma validate
- `type_checks`: npx tsc --noEmit

---

## Execution Requirements
[... standard requirements ...]

## Completion Signal
[... signal format ...]
```

---

## Prompt Generation Function (Pseudocode)

```python
def generate_task_prompt(project_path: str, task_id: str) -> str:
    # Load project files
    tasks = load_json(f"{project_path}/.claude/tasks.json")
    context = read_file(f"{project_path}/.claude/CONTEXT.md")

    # Find the task
    task = find_task(tasks, task_id)
    if not task:
        raise Error(f"Task {task_id} not found")

    # Find next task
    next_task = find_next_pending(tasks, after=task_id)

    # Build context files list
    context_files = "\n".join([f"- {f}" for f in task.context_files])

    # Build output files list
    output_files = "\n".join([f"- {f}" for f in task.output_files])

    # Build success criteria list
    criteria = []
    for c in task.success_criteria:
        criteria.append(f"- `{c.type}`: {c.target or c.command}")
    success_criteria = "\n".join(criteria)

    # Substitute into template
    prompt = TEMPLATE.format(
        PROJECT_NAME=tasks.project.name,
        TASK_ID=task.id,
        TASK_NAME=task.name,
        TASK_DESCRIPTION=task.description,
        CATEGORY=task.category,
        PHASE=task.phase,
        COMPLEXITY=task.estimated_complexity,
        DEPENDS_ON=task.depends_on or "None",
        CONTEXT_FILES_LIST=context_files,
        OUTPUT_FILES_LIST=output_files,
        SUCCESS_CRITERIA_LIST=success_criteria,
        CONTEXT_MD_CONTENTS=context,
        NEXT_TASK_ID=next_task.id if next_task else "null"
    )

    return prompt
```

---

## Quick Prompt (For Simple Cases)

If full context isn't needed, use abbreviated prompt:

```markdown
Complete task {TASK_ID} for project {PROJECT_NAME}.

Read `.claude/CONTEXT.md` first.
Task details in `.claude/tasks.json`.

When done, emit completion signal per project protocol.
```

This relies on the agent reading files itself, reducing prompt size.
