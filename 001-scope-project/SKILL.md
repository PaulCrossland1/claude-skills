---
name: 001-scope-project
description: Comprehensive project scoping through iterative discovery. Guides users through structured questioning phases to capture every detail needed for software work — whether building new products, adding features, auditing security, optimizing performance, fixing bugs, or migrating systems. Use when user wants to plan any software project or needs help structuring requirements before implementation.
---

# Scope Project — Iterative Discovery

Capture everything needed to execute software work through iterative questioning. Keep asking until you have a complete, unambiguous specification.

---

## Step 1: Understand the Work

Start by understanding what type of work this is:

```json
{
  "questions": [{
    "question": "What type of work is this?",
    "header": "Work Type",
    "options": [
      {"label": "New product/feature", "description": "Building something new"},
      {"label": "Bug fix", "description": "Something's broken"},
      {"label": "Refactor/improvement", "description": "Making existing code better"},
      {"label": "Security/performance", "description": "Audit, hardening, or optimization"}
    ],
    "multiSelect": false
  }]
}
```

This shapes what information you need to gather.

---

## Step 2: Iterative Questioning Loop

**Keep asking questions until you have captured all required information.**

Use AskUserQuestion with 2-4 questions per turn. After each response:
1. Acknowledge what you learned
2. Identify what's still unclear or missing
3. Ask follow-up questions
4. Repeat until complete

### Questioning Principles

- **Follow threads** — When an answer reveals complexity, dive deeper
- **Be specific** — "What authentication?" not "Tell me about security"
- **Offer options** — Use multiple choice when reasonable defaults exist
- **Confirm assumptions** — State what you're assuming and ask if correct
- **Track state** — Remember what's been decided, don't re-ask

### Example Flow

```
Turn 1: "What are you building?" → "A task management app"
Turn 2: "Who uses it? What's the core workflow?" → "Teams, kanban-style boards"
Turn 3: "How do teams collaborate? Real-time or async?" → "Real-time, like Trello"
Turn 4: "What's the tech stack? Any constraints?" → "React, Node, PostgreSQL"
Turn 5: "Authentication approach? Roles?" → "Google OAuth, admin/member roles"
... continue until complete ...
```

---

## Step 3: Required Outcomes

**Do not generate the document until you have captured ALL of the following:**

### For ALL project types:

| Category | What to Capture |
|----------|-----------------|
| **The Why** | Problem being solved, who's affected, why now |
| **Success Criteria** | How we know it's done/working, metrics if applicable |
| **Scope Boundaries** | What's in, what's out, what's deferred |
| **Constraints** | Timeline, budget, technical limitations, dependencies |
| **Risks** | What could go wrong, mitigation strategies |

### Additional for new products/features:

| Category | What to Capture |
|----------|-----------------|
| **Users** | Who uses it, their context and motivations |
| **Functionality** | What it does, inputs/outputs, key workflows |
| **Tech Stack** | Frontend, backend, database, hosting, services |
| **Data Model** | Key entities and relationships |
| **Auth/Roles** | Who can do what |
| **UX** | Screens, states, key interactions (if UI involved) |

### Additional for bug fixes:

| Category | What to Capture |
|----------|-----------------|
| **Reproduction** | Exact steps to reproduce |
| **Expected vs Actual** | What should happen vs what happens |
| **Affected Areas** | Which code, which users |
| **Root Cause Hypothesis** | What we think is wrong |

### Additional for security/performance:

| Category | What to Capture |
|----------|-----------------|
| **Current State** | Baseline measurements or known issues |
| **Target State** | What "good" looks like |
| **Scope** | What systems/code to audit or optimize |
| **Methodology** | Approach to testing/measuring |

### Additional for refactors:

| Category | What to Capture |
|----------|-----------------|
| **Current State** | What the code looks like now |
| **Target State** | What it should look like after |
| **Migration Path** | How to get there safely |

### Code Standards (if implementation involved):

| Category | What to Capture |
|----------|-----------------|
| **Patterns** | Coding style, conventions, formatting |
| **Quality** | Testing requirements, documentation expectations |

---

## Step 4: Completeness Check

Before generating, summarize everything you've captured:

```
"Here's what I've gathered:

**Problem**: [summary]
**Users**: [summary]
**Core Features**: [summary]
**Tech Stack**: [summary]
**Success Criteria**: [summary]
**Scope**: [in/out]

Anything to add or change before I generate the document?"
```

Only proceed when the user confirms.

---

## Step 5: Generate Document

Use [prd-template.md](references/prd-template.md) to produce the final document.

**Naming convention**: `[TYPE]-[project-name].md`
- `PRD-taskflow.md` — New product
- `BUGFIX-login-timeout.md` — Bug fix
- `SECURITY-api-audit.md` — Security audit
- `REFACTOR-auth-module.md` — Refactor

Save to `.claude/` directory.

---

## Key Behaviors

1. **Never assume** — If you're not sure, ask
2. **Never skip** — All required outcomes must be captured
3. **Never rush** — Better to ask one more question than miss something
4. **Always confirm** — Summarize understanding before moving on
5. **Stay focused** — Don't ask about UI for a backend refactor

---

## Example AskUserQuestion Patterns

**Multi-choice for common decisions:**
```json
{
  "questions": [{
    "question": "What authentication approach?",
    "header": "Auth",
    "options": [
      {"label": "OAuth (Google, GitHub)", "description": "Social login"},
      {"label": "Email + Password", "description": "Traditional auth"},
      {"label": "Magic Link", "description": "Passwordless email"},
      {"label": "SSO/SAML", "description": "Enterprise single sign-on"}
    ],
    "multiSelect": true
  }]
}
```

**Open-ended with context:**
```json
{
  "questions": [{
    "question": "Describe the core user workflow from start to finish",
    "header": "Workflow",
    "options": [
      {"label": "I'll describe it", "description": "Let me explain the flow"},
      {"label": "Show me examples first", "description": "Reference similar products"}
    ],
    "multiSelect": false
  }]
}
```

**Confirming assumptions:**
```json
{
  "questions": [{
    "question": "I'm assuming PostgreSQL for the database and Prisma as ORM. Sound right?",
    "header": "Data Layer",
    "options": [
      {"label": "Yes, that works", "description": "Proceed with Postgres + Prisma"},
      {"label": "Different database", "description": "I have other preferences"},
      {"label": "No preference", "description": "You decide"}
    ],
    "multiSelect": false
  }]
}
```
