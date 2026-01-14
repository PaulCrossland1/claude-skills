---
name: 000-install
description: Setup and validation skill for the project automation suite. Checks for required directories, CLI tools, and skill dependencies. Run this first in any new environment or to diagnose issues. Use when user says "install skills", "setup environment", "check dependencies", or "diagnose setup".
---

# Environment Setup & Validation

Bootstrap the project automation environment by checking and installing required dependencies.

---

## When to Use

- **First time setup** — New machine or environment
- **Troubleshooting** — Skills not working as expected
- **Validation** — Verify environment is correctly configured
- **Updates** — After updating skills, verify compatibility

---

## Setup Flow

### Step 1: Environment Detection

Detect current environment:

```bash
# Check OS
uname -s  # Darwin, Linux, Windows

# Check shell
echo $SHELL  # /bin/zsh, /bin/bash

# Check working directory
pwd
```

Display environment summary:

```
╔═══════════════════════════════════════════════════════════════╗
║ ENVIRONMENT SETUP                                             ║
╠═══════════════════════════════════════════════════════════════╣
║ OS: macOS (Darwin 24.1.0)                                     ║
║ Shell: zsh                                                    ║
║ Working Dir: /Users/user/projects/my-app                      ║
║ Home: /Users/user                                             ║
╚═══════════════════════════════════════════════════════════════╝
```

### Step 2: Check CLI Tools

Verify required CLI tools are installed:

| Tool | Command | Required For |
|------|---------|--------------|
| Claude CLI | `claude --version` | 003-execute-tasks (Claude provider) |
| Gemini CLI | `gemini --version` | 003-execute-tasks (Gemini provider) |
| Codex CLI | `codex --version` | 003-execute-tasks (Codex provider) |
| Node.js | `node --version` | Many project types |
| npm | `npm --version` | Package management |
| Git | `git --version` | Version control |
| Python | `python3 --version` | Script execution |

Display results:

```
CLI Tools:
  ✓ claude    v1.0.0
  ✓ node      v20.10.0
  ✓ npm       v10.2.3
  ✓ git       v2.43.0
  ✓ python3   v3.12.0
  ✗ gemini    Not installed (optional)
  ✗ codex     Not installed (optional)
```

**If Claude CLI not installed:**
```
⚠ Claude CLI is required but not installed.

Install with:
  npm install -g @anthropic-ai/claude-code

Or see: https://docs.anthropic.com/claude-code
```

### Step 3: Check Skills Directory

Verify skills are installed in `~/.claude/skills/`:

```bash
ls -la ~/.claude/skills/
```

Required skills:
| Skill | Directory | Status |
|-------|-----------|--------|
| 001-scope-project | `~/.claude/skills/001-scope-project/` | Required |
| 002-setup-project | `~/.claude/skills/002-setup-project/` | Required |
| 003-execute-tasks | `~/.claude/skills/003-execute-tasks/` | Required |

Display results:

```
Installed Skills:
  ✓ 001-scope-project
  ✓ 002-setup-project
  ✓ 003-execute-tasks
```

**If skills missing, offer to install:**
```json
{
  "questions": [{
    "question": "Some skills are missing. Install them now?",
    "header": "Install",
    "options": [
      {"label": "Yes, install all (Recommended)", "description": "Copy all skills to ~/.claude/skills/"},
      {"label": "No, skip", "description": "Continue without installing"}
    ],
    "multiSelect": false
  }]
}
```

### Step 4: Check Project Structure

If in a project directory, verify expected structure.

**All project files live under `.claude/`** — single source of truth:

```
Project Structure:
  ✓ .claude/                    Project metadata directory
  ✓ .claude/PRD.md              Requirements (from 001, if saved)
  ✓ .claude/ARCHITECTURE.md     Technical blueprint (from 002)
  ✓ .claude/DECISIONS.md        Architecture decisions
  ✓ .claude/ENV-SETUP.md        Environment requirements
  ✓ .claude/tasks.json          Task definitions
  ✓ .claude/CONTEXT.md          Current project state
  ✓ .claude/PROGRESS-NOTES.md   Progress log
  ✓ .claude/BLOCKERS.md         Blocked task tracking
```

### Step 5: Create Missing Directories

If user approves, create missing directories:

```bash
# Create .claude directory (all project files go here)
mkdir -p .claude

# Initialize empty files if needed
touch .claude/CONTEXT.md
touch .claude/PROGRESS-NOTES.md
touch .claude/BLOCKERS.md
```

### Step 6: Validate Skill Configuration

Check each skill has required files:

```
Skill Validation:
  001-scope-project:
    ✓ SKILL.md exists
    ✓ Valid frontmatter

  002-setup-project:
    ✓ SKILL.md exists
    ✓ Valid frontmatter
    ✓ references/task-template.md exists

  003-execute-tasks:
    ✓ SKILL.md exists
    ✓ Valid frontmatter
    ✓ references/project-protocol.md exists
    ✓ references/task-prompt-template.md exists
```

### Step 7: Test Subagent Execution

Verify Claude CLI can spawn subagents:

```bash
# Quick test
claude --model haiku -p "Say 'test passed' and nothing else" 2>&1
```

Expected output: `test passed`

If fails:
```
⚠ Claude CLI test failed.

Possible issues:
1. API key not configured - run: claude auth login
2. Network issues - check internet connection
3. Rate limiting - wait and retry
```

### Step 8: Summary Report

Display final setup summary:

```
╔═══════════════════════════════════════════════════════════════╗
║ SETUP COMPLETE                                                ║
╠═══════════════════════════════════════════════════════════════╣
║ Environment: Ready                                            ║
║ CLI Tools: 5/7 installed                                      ║
║ Skills: 3/3 installed                                         ║
║ Project Structure: Initialized                                ║
╠═══════════════════════════════════════════════════════════════╣
║ Optional (not installed):                                     ║
║   • gemini CLI - Install for Gemini provider support          ║
║   • codex CLI - Install for Codex provider support            ║
╠═══════════════════════════════════════════════════════════════╣
║ Ready to use:                                                 ║
║   /001-scope-project  - Create a new PRD                      ║
║   /002-setup-project  - Generate project scaffold             ║
║   /003-execute-tasks  - Execute tasks (human-directed)        ║
╚═══════════════════════════════════════════════════════════════╝
```

---

## Installation Commands

### Install All Skills

Copy skills from source to `~/.claude/skills/`:

```bash
# From the skills repository
SKILLS_SOURCE="/Users/paulcrossland/Documents/claude-skills"

# Install each skill
for skill in 001-scope-project 002-setup-project 003-execute-tasks; do
  if [ -f "$SKILLS_SOURCE/$skill.skill" ]; then
    unzip -o "$SKILLS_SOURCE/$skill.skill" -d ~/.claude/skills/
  elif [ -d "$SKILLS_SOURCE/$skill" ]; then
    cp -r "$SKILLS_SOURCE/$skill" ~/.claude/skills/
  fi
done
```

### Install Single Skill

```bash
# From .skill file
unzip -o /path/to/003-execute-tasks.skill -d ~/.claude/skills/

# From directory
cp -r /path/to/003-execute-tasks ~/.claude/skills/
```

### Uninstall Skills

```bash
# Remove all project automation skills
rm -rf ~/.claude/skills/001-scope-project
rm -rf ~/.claude/skills/002-setup-project
rm -rf ~/.claude/skills/003-execute-tasks
```

---

## Troubleshooting

### "Skill not found" errors

```bash
# Verify skill location
ls ~/.claude/skills/

# Check SKILL.md exists
cat ~/.claude/skills/003-execute-tasks/SKILL.md | head -10
```

### Claude CLI hangs on complex prompts

Use temp file approach instead of inline prompts:
```bash
# Write prompt to file
cat > /tmp/prompt.txt << 'EOF'
Your complex prompt here
EOF

# Execute with file
claude --model sonnet -p "$(cat /tmp/prompt.txt)"
```

### Subagent not receiving configuration

When spawning subagents, configuration must be passed explicitly in the prompt. Subagents cannot see the parent's AskUserQuestion responses.

### Permission errors

```bash
# Check ~/.claude/skills permissions
chmod -R 755 ~/.claude/skills/
```

---

## Quick Reference

```bash
# Full environment check
/000-install

# Check specific component
/000-install --check cli
/000-install --check skills
/000-install --check project

# Install missing components
/000-install --fix

# Verbose output
/000-install --verbose
```
