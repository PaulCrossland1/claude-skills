---
name: 003-execute-tasks
description: Spawn a sub-agent using Claude, Gemini, or Codex CLI with selected model. Use when the user says "use /subagent to" followed by a task.
---

# Subagent Spawner

Spawn sub-agents using different AI CLI providers. Supports two modes:
1. **Ad-hoc tasks** — General purpose task execution
2. **Project tasks** — Execute tasks from `.claude/tasks.json` with completion protocol

---

## Mode Detection

**Project mode** if any of:
- User says "run task T005" or "run T005"
- User says "run next task" or "next task"
- User says "continue project" or "continue"
- Current directory has `.claude/tasks.json`

**Ad-hoc mode** otherwise.

---

## Ad-Hoc Mode (Simple Tasks)

For general tasks not part of a structured project.

### Step 1: Capture Task
Everything after "use /subagent to" is the TASK.

### Step 2: Provider Selection
```json
{
  "questions": [{
    "question": "Which AI provider?",
    "header": "Provider",
    "options": [
      {"label": "Claude (Recommended)", "description": "Anthropic Claude Code CLI"},
      {"label": "Gemini", "description": "Google Gemini CLI"},
      {"label": "Codex", "description": "OpenAI Codex CLI"}
    ],
    "multiSelect": false
  }]
}
```

### Step 3: Model Selection

**Claude:**
- sonnet (Recommended) — Balanced
- haiku — Fast, cheap
- opus — Most capable

**Gemini:** Default model (no selection)

**Codex:**
- gpt-5.2-codex-medium (Recommended)
- gpt-5.1-codex-mini-low — Lightweight
- gpt-5.1-codex-max-xhigh — Maximum

### Step 4: Permission Mode

**Claude:**
- Auto-approve edits → `--permission-mode acceptEdits`
- YOLO → `--dangerously-skip-permissions`

**Gemini:**
- Auto-approve edits → `--approval-mode auto_edit`
- YOLO → `-y`

**Codex:**
- Full-auto → `--full-auto`
- YOLO → `--dangerously-bypass-approvals-and-sandbox`

### Step 5: Execute

```bash
# Claude
claude --model MODEL --permission-mode acceptEdits -p "TASK"

# Gemini
gemini --approval-mode auto_edit "TASK"

# Codex
codex exec --skip-git-repo-check --full-auto --model MODEL "TASK"
```

---

## Project Mode (Structured Tasks)

For tasks from a `/002-setup-project` generated project.

### Step 1: Detect Project

Check for `.claude/tasks.json` in current or specified directory.

If not found:
```json
{
  "questions": [{
    "question": "No project found. What would you like to do?",
    "header": "Project",
    "options": [
      {"label": "Specify path", "description": "I'll provide the project path"},
      {"label": "Run ad-hoc", "description": "Execute without project context"}
    ],
    "multiSelect": false
  }]
}
```

### Step 2: Determine Task

If user specified task ID (e.g., "run T005"):
- Load that specific task

If user said "next task" or "continue":
- Find first task with `status: pending`
- Verify dependencies are `completed`

### Step 3: Display Task Summary

Output a concise table — no prose explanation:

```
┌──────────────────────────────────────────────────────────┐
│ T003 — Set up client with Vite and React                 │
├─────────────┬────────────────────────────────────────────┤
│ Phase       │ foundation                                 │
│ Complexity  │ simple                                     │
│ Depends on  │ T001 ✓, T002 ✓                             │
│ Outputs     │ client/, vite.config.ts, package.json      │
└─────────────┴────────────────────────────────────────────┘
```

Then immediately proceed to model selection.

### Step 4: Generate Task Prompt

Build prompt using template from [task-prompt-template.md](references/task-prompt-template.md):

1. Read `.claude/tasks.json` for task details
2. Read `.claude/CONTEXT.md` for project state
3. Substitute into template
4. Include completion signal instructions

### Step 5: Provider, Model & Permission Selection

Follow the full ad-hoc flow (Steps 2-4) with complexity-based recommendations.

**5a. Provider Selection:**
```json
{
  "questions": [{
    "question": "Task {TASK_ID} ({COMPLEXITY}). Which provider?",
    "header": "Provider",
    "options": [
      {"label": "Claude (Recommended)", "description": "Anthropic Claude Code CLI"},
      {"label": "Gemini", "description": "Google Gemini CLI"},
      {"label": "Codex", "description": "OpenAI Codex CLI"}
    ],
    "multiSelect": false
  }]
}
```

**5b. Model Selection** (based on provider):

Recommend based on task complexity:
| Complexity | Claude | Codex |
|------------|--------|-------|
| `trivial`, `simple` | haiku | gpt-5.1-codex-mini-low |
| `moderate` | sonnet | gpt-5.2-codex-medium |
| `complex` | opus | gpt-5.1-codex-max-xhigh |

(Gemini uses default model — skip this step)

**5c. Permission Mode:**
- Claude: `acceptEdits` or `dangerously-skip-permissions`
- Gemini: `auto_edit` or `-y`
- Codex: `full-auto` or `dangerously-bypass-approvals-and-sandbox`

### Step 6: Execute with Protocol

Run the subagent with the generated prompt.

**The prompt instructs the subagent to:**
1. Read CONTEXT.md first
2. Complete the task
3. Run success criteria
4. Update PROGRESS-NOTES.md
5. Update CONTEXT.md
6. Update tasks.json
7. Emit completion signal

See [project-protocol.md](references/project-protocol.md) for full protocol.

### Step 7: Parse Completion Signal

After subagent completes, find and parse:

```
--- TASK COMPLETION ---
task_id: T005
status: completed
...
next_task: T006
--- END COMPLETION ---
```

### Step 8: Sweep & Enhance Documentation

After subagent completes, perform a documentation sweep. You (in the main Claude session) have broader project context than the subagent, so actively review and enhance:

1. **Read files created/modified** by subagent
2. **Verify subagent updates** to CONTEXT.md, PROGRESS-NOTES.md, tasks.json
3. **Enhance if needed** — you have broader project context:

| File | Check | Enhance if... |
|------|-------|---------------|
| `.claude/CONTEXT.md` | Current state accurate? | Add context subagent missed, note dependency implications |
| `.claude/PROGRESS-NOTES.md` | Entry complete? | Add cross-references to related tasks, implementation notes |
| `.claude/tasks.json` | Status correct? | Update downstream task descriptions if scope changed |
| `.claude/ARCHITECTURE.md` | Still accurate? | Document new patterns that emerged |
| `.claude/DECISIONS.md` | New decisions made? | Log architectural choices subagent made |

4. **Skip sweep** only if task was trivial and completion signal confirms all updates made

### Step 9: Report & Continue

Report results to user:

```
✓ Task T005 completed successfully

Files created:
- src/models/User.ts

Success criteria: 3/3 passed

Next task: T006 — Create Genome model

Continue with next task?
```

If `status: blocked`:
```
⚠ Task T005 blocked

Blocker: Missing CLERK_SECRET_KEY environment variable

Required action:
1. Create Clerk account at clerk.dev
2. Add CLERK_SECRET_KEY to .env.local

See .claude/BLOCKERS.md for details.
```

---

## Completion Signal Format

Subagents MUST emit this at response end:

```yaml
--- TASK COMPLETION ---
task_id: T005
task_name: Create User model
status: completed | blocked | failed
duration_minutes: 15

files_created:
  - path/to/file

files_modified:
  - path/to/file

success_criteria:
  - [PASS] file_exists: src/models/User.ts
  - [PASS] command_succeeds: npx tsc --noEmit

blocker: none | "description"

notes: |
  Summary of work done

context_updated: true
progress_notes_updated: true
tasks_json_updated: true

next_task: T006 | null
--- END COMPLETION ---
```

---

## Quick Reference: Commands

```bash
# Claude (recommended for most tasks)
claude --model sonnet --permission-mode acceptEdits -p "PROMPT"
claude --model opus --dangerously-skip-permissions -p "PROMPT"

# Gemini
gemini --approval-mode auto_edit "PROMPT"
gemini -y "PROMPT"

# Codex
codex exec --skip-git-repo-check --full-auto --model gpt-5.2-codex-medium "PROMPT"
```

---

## References

- **[project-protocol.md](references/project-protocol.md)** — Completion signal spec, file update requirements
- **[task-prompt-template.md](references/task-prompt-template.md)** — Template for project task prompts
