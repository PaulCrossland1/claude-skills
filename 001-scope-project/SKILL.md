---
name: 001-scope-project
description: Comprehensive project scoping through iterative discovery. Guides users through structured questioning phases to capture every detail needed for software work — whether building new products, adding features, auditing security, optimizing performance, fixing bugs, or migrating systems. Use when user wants to plan any software project or needs help structuring requirements before implementation.
---

# Scope Project — Iterative Discovery

Capture everything needed to execute software work through natural conversation and targeted questions.

---

## Step 1: Open with a Simple Prompt

**Do NOT use AskUserQuestion first.** Start with an open prompt:

> "What are we working on today?"

Or if context suggests they have something in mind:

> "Tell me about what you're trying to build/fix/improve."

**Let them describe it in their own words.** This could be:
- A full product idea
- A single feature
- A bug they encountered
- A refactor they're considering
- A vague notion they want to explore

Don't assume scope. Let them tell you.

---

## Step 2: Acknowledge and Start Drilling Down

After they describe their intent, acknowledge what you heard and start asking targeted questions using AskUserQuestion.

**Example flow:**

User: "I want to build a simple app that helps me track my reading habits"

You: "Got it — a reading tracker. Let me understand this better."

Then use AskUserQuestion to drill down:

```json
{
  "questions": [{
    "question": "What's the core thing you want to track?",
    "header": "Core Feature",
    "options": [
      {"label": "Books read", "description": "Track completed books"},
      {"label": "Reading progress", "description": "Track pages/chapters as you go"},
      {"label": "Reading time", "description": "Track how long you read"},
      {"label": "All of the above", "description": "Comprehensive tracking"}
    ],
    "multiSelect": false
  }]
}
```

---

## Step 3: Iterative Questioning

**Keep asking questions until you have everything needed.**

### Questioning Principles

- **React to their answers** — Each question should follow from what they just said
- **Follow threads** — When an answer reveals complexity, go deeper
- **Use AskUserQuestion for choices** — When there are reasonable options to pick from
- **Use open prompts for exploration** — When you need them to describe something
- **Confirm assumptions** — State what you're assuming and check
- **Don't over-question simple things** — A small script doesn't need a full PRD

### Adapt to Scope

**Small scope** (script, quick fix, simple feature):
- 2-5 questions might be enough
- Focus on: what it does, any constraints, how to know it works

**Medium scope** (feature, integration, refactor):
- 5-15 questions
- Add: who uses it, edge cases, tech approach

**Large scope** (new product, major system):
- Many questions across multiple turns
- Cover: users, workflows, tech stack, data model, auth, deployment, etc.

---

## Step 4: Required Outcomes

Before generating a document, ensure you've captured what's needed for the scope:

### Always Capture (any size):

| What | Why |
|------|-----|
| **What it does** | Core functionality |
| **Success criteria** | How we know it works |
| **Constraints** | Limitations, requirements |

### Also Capture (medium+ scope):

| What | Why |
|------|-----|
| **Who uses it** | Target users/personas |
| **Key workflows** | How people use it |
| **Tech approach** | Stack, architecture |
| **Edge cases** | What could go wrong |

### Also Capture (large scope):

| What | Why |
|------|-----|
| **Data model** | Entities, relationships |
| **Auth/permissions** | Who can do what |
| **Integrations** | External systems |
| **Deployment** | Where/how it runs |
| **Rollout plan** | How to release safely |

---

## Step 5: Completeness Check

Before generating, briefly summarize what you've gathered:

> "Here's what I've got:
> - [Core functionality]
> - [Key decisions]
> - [Technical approach]
>
> Anything to add before I write this up?"

For small things, this might be 3 bullet points.
For large projects, this might be a full summary.

---

## Step 6: Generate Document

**Match the document to the scope:**

| Scope | Output |
|-------|--------|
| Tiny (script, one-liner) | Maybe no document needed — just do it |
| Small (quick feature, bug fix) | Brief spec in chat or short markdown |
| Medium (feature, integration) | Focused requirements doc |
| Large (new product, major system) | Full PRD with all sections |

Use [prd-template.md](references/prd-template.md) as a guide, but only include sections that are relevant.

**Saving:**
- Tiny/Small: May not need a file — just proceed to implementation
- Medium+: Save as `.claude/PRD.md` — this becomes input for `/002-setup-project`

---

## Key Behaviors

1. **Start open** — Let them describe intent before structuring
2. **Match their energy** — Small ask = simple questions. Big vision = thorough discovery.
3. **Follow the thread** — Each question reacts to what they just said
4. **Don't over-engineer** — A 10-line script doesn't need a PRD
5. **Use AskUserQuestion strategically** — For choices, not for open exploration

---

## Example: Small Scope

**User**: "I need a script that renames files in a folder based on their creation date"

**You**: "Simple enough. A few quick questions:"

```json
{
  "questions": [{
    "question": "What format for the new names?",
    "header": "Format",
    "options": [
      {"label": "2024-01-15-filename.txt", "description": "Date prefix"},
      {"label": "filename-2024-01-15.txt", "description": "Date suffix"},
      {"label": "2024/01/15/filename.txt", "description": "Date folders"}
    ]
  }]
}
```

Then maybe one more question about handling duplicates, and you're done. No PRD needed.

---

## Example: Large Scope

**User**: "I want to build a marketplace for freelance developers"

**You**: "That's a substantial project. Let me understand the vision."

Then many rounds of AskUserQuestion covering:
- Target users (who's buying, who's selling)
- Core workflows (finding work, hiring, payments)
- Differentiators (what makes this different from Upwork)
- Tech preferences
- MVP scope vs full vision
- And so on...

This warrants a full PRD with all sections.

---

## AskUserQuestion Patterns

**Drilling into specifics:**
```json
{
  "question": "You mentioned user authentication. What approach?",
  "options": [
    {"label": "Email + password", "description": "Traditional"},
    {"label": "OAuth only", "description": "Google, GitHub, etc."},
    {"label": "Magic link", "description": "Passwordless"},
    {"label": "Not sure yet", "description": "Help me decide"}
  ]
}
```

**Confirming understanding:**
```json
{
  "question": "So the core flow is: user uploads file → system processes → user downloads result. Right?",
  "options": [
    {"label": "Yes, exactly", "description": "Move on"},
    {"label": "Close but...", "description": "Small correction"},
    {"label": "Not quite", "description": "Let me clarify"}
  ]
}
```

**Gauging scope:**
```json
{
  "question": "How big is this project in your mind?",
  "options": [
    {"label": "Quick thing", "description": "Hour or less of work"},
    {"label": "Small feature", "description": "A day or two"},
    {"label": "Significant feature", "description": "A week+"},
    {"label": "Full product", "description": "Major undertaking"}
  ]
}
```
