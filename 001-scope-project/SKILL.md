---
name: 001-scope-project
description: Comprehensive PRD creation through iterative discovery. Guides users through structured questioning phases to capture every detail needed for software development. Use when user wants to plan a new project, create a PRD, define requirements, start building something new, or needs help structuring a software idea before implementation.
---

# Start Project — Gold Standard PRD Discovery

Create a zero-ambiguity Product Requirements Document by iteratively gathering all requirements through 20 structured phases. The goal: produce a blueprint so complete that any competent team could build it without asking questions.

## Workflow

### 1. Open with Project Type

Start with AskUserQuestion:

```json
{
  "questions": [{
    "question": "What are you trying to build?",
    "header": "Project Type",
    "options": [
      {"label": "New product from scratch", "description": "Greenfield development"},
      {"label": "New feature", "description": "Adding to existing product"},
      {"label": "Improvement/refactor", "description": "Enhancing existing functionality"},
      {"label": "Integration", "description": "Connecting with external systems"}
    ],
    "multiSelect": false
  }]
}
```

### 2. Execute Discovery Phases

Work through all 20 phases from [question-phases.md](references/question-phases.md).

| # | Phase | Goal |
|---|-------|------|
| **1** | Executive Context | Problem, strategic alignment, ownership |
| **2** | User Personas | Primary, secondary, anti-personas |
| **3** | Success Metrics | North star, secondary, guardrails, instrumentation |
| **4** | User Stories & Journeys | Stories, flows, entry points |
| **5** | Functional Requirements | Features, inputs/outputs, data entities |
| **6** | Logic & Algorithms | Formulas, business rules, state machines |
| **7** | Edge Cases | User, data, and system "what ifs" |
| **8** | UX: Screens & States | Screen inventory, 4 states per screen |
| **9** | UX: Interactions | Micro-interactions, animations, sound/haptics |
| **10** | Tech Stack: Core | Frontend, backend, API style |
| **11** | Tech Stack: Data | Database, ORM, caching, storage, search |
| **12** | Tech Stack: Auth | Provider, methods, OAuth, roles, sessions |
| **13** | Tech Stack: Infra | Hosting, CI/CD, environments, DNS/SSL |
| **14** | Tech Stack: Services | Email, payments, analytics, monitoring |
| **15** | API Contracts | Architecture, endpoints, schema, indexes |
| **16** | Performance & Security | Budgets, compliance, platform compatibility |
| **17** | Operational | i18n, a11y, admin tools, data management |
| **18** | Go-to-Market | Release phases, marketing, rollback plan |
| **19** | Scope Boundaries | v1/v2, exclusions, risks, open questions |
| **20** | Implementation | File structure, patterns, testing, docs |

### Phase Execution Rules

**Per Phase:**
1. Ask 2-4 targeted questions using AskUserQuestion
2. Summarize understanding after responses
3. Dive deeper if answers reveal complexity
4. Move to next phase when complete

**Adaptive Skipping:**
- Skip Auth (12) if no authentication needed
- Skip Payments (14) if no monetization
- Skip Sound/Haptics (9) if not a game/interactive
- Skip i18n (17) if English-only v1
- Skip GTM (18) for internal tools

**Consolidation:**
- Tech phases (10-14) can be 2-3 rounds if user knows their stack
- Simple projects can combine phases 5-7

### 3. Confirm Completeness

Before generating, summarize all gathered information:

```
"I've captured:
- [Summary of each major section]

Before I generate the full PRD, anything to add or change?"
```

### 4. Generate PRD

Use [prd-template.md](references/prd-template.md) to produce the Gold Standard document.

Output as markdown: `PRD-[project-name].md`

---

## AskUserQuestion Examples

**Metrics (Phase 3):**
```json
{
  "questions": [
    {
      "question": "What single metric defines success for this project?",
      "header": "North Star",
      "options": [
        {"label": "Retention", "description": "D1, D7, or D30 retention rate"},
        {"label": "Engagement", "description": "DAU, session length, actions per session"},
        {"label": "Conversion", "description": "Signup rate, purchase rate"},
        {"label": "Revenue", "description": "MRR, ARPU, LTV"}
      ],
      "multiSelect": false
    },
    {
      "question": "What must NOT get worse?",
      "header": "Guardrails",
      "options": [
        {"label": "Cost per user", "description": "Server costs stay under $X"},
        {"label": "Error rate", "description": "Crashes/errors below X%"},
        {"label": "Load time", "description": "Performance stays fast"},
        {"label": "Support tickets", "description": "No increase in complaints"}
      ],
      "multiSelect": true
    }
  ]
}
```

**Logic & Algorithms (Phase 6):**
```json
{
  "questions": [
    {
      "question": "Are there calculations, scoring, or game mechanics that need exact formulas?",
      "header": "Algorithms",
      "options": [
        {"label": "Yes, core mechanics", "description": "Need precise formulas defined"},
        {"label": "Yes, secondary", "description": "Some calculations but not core"},
        {"label": "No formulas", "description": "Standard CRUD operations"}
      ],
      "multiSelect": false
    }
  ]
}
```

**UI States (Phase 8):**
```json
{
  "questions": [
    {
      "question": "For each screen, we need to define 4 states. Let's start with the main screen. What should the EMPTY state show?",
      "header": "Empty State",
      "options": [
        {"label": "Onboarding prompt", "description": "Guide user to first action"},
        {"label": "Sample data", "description": "Show examples of what it could look like"},
        {"label": "Blank with CTA", "description": "Simple 'Get Started' button"},
        {"label": "Tutorial overlay", "description": "Interactive walkthrough"}
      ],
      "multiSelect": false
    }
  ]
}
```

**Go-to-Market (Phase 18):**
```json
{
  "questions": [
    {
      "question": "What's the release strategy?",
      "header": "Release Plan",
      "options": [
        {"label": "Alpha → Beta → GA", "description": "Internal, then waitlist, then public"},
        {"label": "Soft launch", "description": "Ship quietly, iterate, then announce"},
        {"label": "Big bang", "description": "Full public launch immediately"},
        {"label": "Feature flag", "description": "Ship dark, enable for % of users"}
      ],
      "multiSelect": false
    },
    {
      "question": "What triggers a rollback?",
      "header": "Rollback",
      "options": [
        {"label": "Error rate > 1%", "description": "Automated rollback on errors"},
        {"label": "Crash rate spike", "description": "App stability issues"},
        {"label": "Negative feedback", "description": "User complaints threshold"},
        {"label": "Manual only", "description": "Human decision required"}
      ],
      "multiSelect": true
    }
  ]
}
```

---

## Session State

Track across all phases:
- **Locked**: Confirmed decisions (don't re-ask)
- **Open**: Needs follow-up
- **Assumed**: Validate before generating

Between phases, briefly summarize:
> "Got it — D1 Retention > 20% as North Star, with server cost guardrails. Moving to User Stories..."
