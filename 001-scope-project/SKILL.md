---
name: 001-scope-project
description: Comprehensive project scoping through iterative discovery. Guides users through structured questioning phases to capture every detail needed for software work — whether building new products, adding features, auditing security, optimizing performance, fixing bugs, or migrating systems. Use when user wants to plan any software project or needs help structuring requirements before implementation.
---

# Start Project — Gold Standard Discovery

Create a zero-ambiguity requirements document by iteratively gathering all relevant details through structured phases. The goal: produce a blueprint so complete that any competent team could execute it without asking questions.

**Works for:** New products, features, refactors, bug fixes, security audits, performance optimization, integrations, and migrations.

## Workflow

### 1. Open with Project Type

Start with AskUserQuestion:

```json
{
  "questions": [{
    "question": "What type of work is this?",
    "header": "Project Type",
    "options": [
      {"label": "New product", "description": "Building from scratch (greenfield)"},
      {"label": "New feature", "description": "Adding capability to existing product"},
      {"label": "Improvement/refactor", "description": "Enhancing or restructuring existing code"},
      {"label": "Bug fix/investigation", "description": "Diagnosing and fixing issues"}
    ],
    "multiSelect": false
  },
  {
    "question": "Any specialized focus?",
    "header": "Focus Area",
    "options": [
      {"label": "General development", "description": "Standard feature/product work"},
      {"label": "Security audit", "description": "Vulnerability assessment and hardening"},
      {"label": "Performance optimization", "description": "Speed, efficiency, resource usage"},
      {"label": "Integration/migration", "description": "Connecting systems or moving platforms"}
    ],
    "multiSelect": false
  }]
}
```

The combination of **Project Type** + **Focus Area** determines which phases apply and how questions are framed.

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
| **21** | Code Standards | Conventions, style, formatting, quality rules |

### Phase Applicability by Project Type

Not all phases apply to all project types. Use this matrix:

| Phase | New Product | New Feature | Refactor | Bug Fix | Security | Performance | Integration |
|-------|:-----------:|:-----------:|:--------:|:-------:|:--------:|:-----------:|:-----------:|
| 1. Executive Context | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 2. Personas/Stakeholders | ✓ | ✓ | lite | lite | threat actors | lite | ✓ |
| 3. Success Metrics | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 4. User Stories/Scope | ✓ | ✓ | change scope | repro steps | attack vectors | bottlenecks | data flows |
| 5. Functional Reqs | ✓ | ✓ | current vs target | root cause | vulnerabilities | hot paths | endpoints |
| 6. Logic & Rules | ✓ | ✓ | ✓ | ✗ | ✗ | ✗ | ✓ |
| 7. Edge Cases | ✓ | ✓ | ✓ | ✗ | exploit scenarios | load scenarios | failure modes |
| 8-9. UX/Design | ✓ | ✓ | if UI changes | ✗ | ✗ | ✗ | ✗ |
| 10-14. Tech Stack | choose | document existing | document existing | document existing | audit existing | audit existing | map systems |
| 15. API/Architecture | ✓ | ✓ | current state | affected areas | attack surface | performance profile | integration points |
| 16. Perf & Security | ✓ | ✓ | ✓ | ✗ | **primary focus** | **primary focus** | ✓ |
| 17. Operational | ✓ | lite | lite | ✗ | compliance | monitoring | ✓ |
| 18. Go-to-Market | ✓ | ✓ | rollout plan | ✗ | remediation plan | rollout plan | migration plan |
| 19. Scope Boundaries | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 20-21. Implementation | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

**Legend:** ✓ = full phase | lite = abbreviated | ✗ = skip | *text* = alternative framing

### Phase Execution Rules

**Per Phase:**
1. Ask 2-4 targeted questions using AskUserQuestion
2. Summarize understanding after responses
3. Dive deeper if answers reveal complexity
4. Move to next phase when complete

**Adaptive Skipping:**
- Skip UX phases (8-9) for backend-only, security audits, performance work
- Skip Auth (12) if no authentication needed
- Skip Payments (14) if no monetization
- Skip i18n (17) if English-only v1
- Skip GTM (18) for internal tools or bug fixes

**Project-Type Adaptations:**
- **Security audits**: Replace personas with threat actors, features with vulnerabilities
- **Performance**: Focus on bottlenecks, metrics, profiling results
- **Bug fixes**: Emphasize reproduction steps, root cause, affected areas
- **Existing codebases**: Tech stack phases become "document current state" not "choose"

**Consolidation:**
- Tech phases (10-14) can be 2-3 rounds if documenting existing stack
- Simple projects can combine phases 5-7
- Bug fixes may only need phases 1, 3, 4, 5, 15, 19-21

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
