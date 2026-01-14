# PRD Template — Gold Standard

Use this template to generate the final PRD document. Fill every section.

---

# [PROJECT_NAME] — Product Requirements Document

**Version:** v1.0
**Status:** Draft | In Review | Approved
**Owner:** [Name, Role]
**Reviewers:** [Name, Name]
**Last Updated:** [Date]

---

## 1. Executive Context (The "Why")

### Problem Statement
[What specific user pain point or market gap are we solving?]

| Aspect | Answer |
|--------|--------|
| **The Problem** | [What's broken?] |
| **Who Has It** | [Which users?] |
| **Current Workaround** | [How do they cope today?] |
| **Why Now** | [Why is this the right time?] |

### Strategic Alignment
| Company Goal | How This Contributes |
|--------------|---------------------|
| [OKR/Goal] | [Contribution] |

### Opportunity Cost
[What happens if we DON'T build this?]

---

## 2. User Personas

### Primary Persona: [Name]
| Attribute | Description |
|-----------|-------------|
| **Name** | [e.g., "Bored at Work Bill"] |
| **Context** | [When/where they use this] |
| **Motivation** | [What drives them] |
| **Technical Level** | [Novice/Intermediate/Advanced] |
| **Key Quote** | ["I wish I could..."] |

### Secondary Persona: [Name] (if applicable)
| Attribute | Description |
|-----------|-------------|
| **Name** | [Name] |
| **Context** | [Context] |
| **Motivation** | [Motivation] |

### Anti-Personas (Who This Is NOT For)
- [Type] — [Why not]

---

## 3. Success Metrics (The "Scoreboard")

### North Star Metric
| Metric | Target | Rationale |
|--------|--------|-----------|
| [e.g., D1 Retention] | [e.g., > 20%] | [Why this metric matters] |

### Secondary Metrics
| Metric | Target | Purpose |
|--------|--------|---------|
| [DAU] | [X] | [Health indicator] |
| [Avg Session Length] | [X min] | [Engagement] |
| [Conversion Rate] | [X%] | [Monetization] |

### Guardrail Metrics (Must NOT Get Worse)
| Metric | Threshold | Alert Trigger |
|--------|-----------|---------------|
| Server Cost per User | < $[X] | > $[X] |
| Crash Rate | < [X%] | > [X%] |
| Error Rate | < [X%] | > [X%] |

### Instrumentation Plan
| Event Name | Properties | Trigger |
|------------|------------|---------|
| `[event_name]` | `{ prop1, prop2 }` | [When fired] |
| `[event_name]` | `{ prop1, prop2 }` | [When fired] |

---

## 4. User Stories & Journeys

### Core User Stories

**Must Have (P0):**
```
AS A [persona]
I WANT TO [action]
SO THAT [benefit]

Acceptance Criteria:
- [ ] [Criterion 1]
- [ ] [Criterion 2]
```

**Should Have (P1):**
```
AS A [persona]
I WANT TO [action]
SO THAT [benefit]
```

### Primary User Flow
```
[Entry] → [Step 1] → [Step 2] → [Step 3] → [Core Value]
              ↓
         [Alt Path]
```

### Entry Points
| Source | First Screen | Expected % |
|--------|--------------|------------|
| [Direct link] | [Landing] | [X%] |
| [Referral] | [Invite page] | [X%] |

---

## 5. Functional Requirements

### Feature Hierarchy
```
[Product]
├── [Core Feature 1]
│   ├── [Sub-feature]
│   └── [Sub-feature]
├── [Core Feature 2]
│   ├── [Sub-feature]
│   └── [Sub-feature]
└── [Core Feature 3]
```

### Feature Specifications

#### [Feature Name]
| Aspect | Specification |
|--------|---------------|
| **Input** | [What it takes] |
| **Output** | [What it produces] |
| **Interaction** | [How user interacts] |
| **Priority** | P0/P1/P2 |

### Data Entities
| Entity | Description | Key Fields |
|--------|-------------|------------|
| [User] | [Description] | id, email, created_at |
| [Item] | [Description] | id, name, owner_id |

---

## 6. Logic & Algorithms

### Calculations & Formulas
```
[Formula Name]:
[Variable] = [Expression]

Example:
Top_Speed = Base_Speed + (Engine_Level * 1.5)
Acceleration = Base_Accel - (Weight * 0.2)
Score = (Wins * 10) + (Races * 2)
```

### Business Rules
```
RULE: [Rule Name]
IF [condition]
THEN [action]
ELSE [alternative]

Example:
RULE: Race Placement Reward
IF placement == 1 THEN coins += 100
IF placement == 2 THEN coins += 75
IF placement == 3 THEN coins += 50
ELSE coins += 10
```

### State Machine
```
[State Diagram]

         ┌─────────────────────────────────────┐
         ↓                                     │
    ┌────────┐    ┌─────────────┐    ┌────────────┐    ┌─────────┐
    │  Idle  │───→│ Matchmaking │───→│   Lobby    │───→│ Racing  │
    └────────┘    └─────────────┘    └────────────┘    └─────────┘
         ↑              │                   │               │
         │              ↓                   ↓               ↓
         │         [Timeout]           [Player Left]   ┌─────────┐
         │              │                   │          │ Results │
         │              ↓                   ↓          └─────────┘
         └──────────[Return to Idle]───────┴───────────────┘
```

---

## 7. Edge Cases (The "What Ifs")

### User Edge Cases
| Scenario | Expected Behavior |
|----------|-------------------|
| User disconnects mid-race | [Behavior] |
| User is new (no data) | [Show empty state] |
| User tries to cheat | [Validation + ban] |

### Data Edge Cases
| Scenario | Expected Behavior |
|----------|-------------------|
| Missing required field | [Error message] |
| Two events at exact same time | [Tiebreaker logic] |
| Max limit exceeded | [Error + prevent] |

### System Edge Cases
| Scenario | Expected Behavior |
|----------|-------------------|
| Database unavailable | [Graceful degradation] |
| Third-party API down | [Fallback/cache] |
| Load spike (10x normal) | [Queue/throttle] |

---

## 8. UX & Design

### Screen Inventory
| Screen | Purpose | Primary Action |
|--------|---------|----------------|
| [Landing] | [First impression] | [Start Playing] |
| [Lobby] | [Wait for match] | [Ready Up] |
| [Game] | [Core gameplay] | [Play] |
| [Results] | [Show outcome] | [Play Again] |

### UI States (Per Screen)

#### [Screen Name]
| State | Description | Design Notes |
|-------|-------------|--------------|
| **Ideal** | [Populated with data] | [Layout notes] |
| **Empty** | [First time user] | [Onboarding CTA] |
| **Loading** | [Fetching data] | [Skeleton/spinner] |
| **Error** | [Failed to load] | [Retry button] |

### Wireframes/Mockups
- Figma: [link]
- Design System: [link]

### Interactions & Feedback
| Element | Interaction | Feedback |
|---------|-------------|----------|
| [Button] | Click | [Animation/sound] |
| [Card] | Hover | [Highlight effect] |
| [Form] | Submit | [Loading → Success/Error] |

### Sound & Haptics (if applicable)
| Trigger | Sound | Haptic |
|---------|-------|--------|
| [Race start] | [Engine rev] | [Short vibrate] |
| [Win] | [Celebration fanfare] | [Long vibrate] |
| [Collision] | [Bump sound] | [Medium vibrate] |

---

## 9. Technical Stack

### 9.1 Core Stack
| Layer | Technology | Version/Notes |
|-------|------------|---------------|
| **Frontend** | [React/Next.js/Vue] | [version] |
| **UI Library** | [shadcn/ui/MUI/Tailwind] | [approach] |
| **Backend** | [Node.js/Python/Go] | [framework] |
| **Language** | [TypeScript/JavaScript] | [strict mode] |
| **API Style** | [REST/GraphQL/tRPC/WebSocket] | [versioning] |

### 9.2 Data Layer
| Component | Technology | Provider | Purpose |
|-----------|------------|----------|---------|
| **Primary DB** | [PostgreSQL] | [Supabase] | [Main data] |
| **Cache** | [Redis] | [Upstash] | [Sessions, state] |
| **File Storage** | [S3/R2] | [AWS/Cloudflare] | [User uploads] |
| **Search** | [Algolia/PG FTS] | [Provider] | [What's searchable] |
| **ORM** | [Prisma/Drizzle] | — | [Query layer] |

### 9.3 Authentication & Authorization
| Aspect | Decision | Details |
|--------|----------|---------|
| **Provider** | [Clerk/Auth0/Supabase] | [Why chosen] |
| **Methods** | [Email, OAuth, Magic Link] | [All supported] |
| **OAuth** | [Google, GitHub, Discord] | [Which ones] |
| **Authorization** | [RBAC/Simple/Team-based] | [Model] |
| **Sessions** | [JWT/Database/Redis] | [Duration: Xd] |

#### Roles & Permissions
| Role | Permissions |
|------|-------------|
| [Admin] | [Full access] |
| [User] | [CRUD own, read shared] |
| [Guest] | [Read-only public] |

### 9.4 Infrastructure
| Component | Choice | Configuration |
|-----------|--------|---------------|
| **Hosting** | [Vercel/Railway/AWS] | [Region] |
| **Environments** | [Dev/Staging/Prod] | [PR previews: Y/N] |
| **CI/CD** | [GitHub Actions/Vercel] | [On PR: lint, test, build] |
| **Domain** | [example.com] | [DNS: Cloudflare] |
| **SSL** | [Platform/Cloudflare] | [Auto-renewal] |
| **CDN** | [Cloudflare/Vercel Edge] | [What's cached] |

### 9.5 Third-Party Services
| Category | Service | Purpose | Tier |
|----------|---------|---------|------|
| **Email** | [Resend] | [Transactional] | [Free/Pro] |
| **Payments** | [Stripe] | [Subscriptions] | [Standard] |
| **Analytics** | [PostHog] | [Product events] | [Free] |
| **Errors** | [Sentry] | [Error tracking] | [Free] |
| **Logging** | [BetterStack] | [App logs] | [Free] |
| **Feature Flags** | [PostHog] | [Gradual rollout] | [Free] |

### 9.6 Real-time & Background
| Feature | Technology | Details |
|---------|------------|---------|
| **Real-time** | [WebSockets/SSE] | [Use case] |
| **Jobs** | [BullMQ/Cron] | [Job types] |
| **Queues** | [Redis/SQS] | [What's queued] |

---

## 10. API Contracts

### System Architecture
```
[Architecture Diagram]

┌──────────┐     ┌──────────┐     ┌──────────┐
│  Client  │────→│   API    │────→│    DB    │
│ (Browser)│←────│ (Server) │←────│ (Postgres)│
└──────────┘     └──────────┘     └──────────┘
      │               │
      │               ↓
      │          ┌──────────┐
      └─────────→│  Cache   │
                 │ (Redis)  │
                 └──────────┘
```

### Endpoint Specifications
```
[METHOD] /api/v1/[resource]
Auth: Required | Optional | None
Rate Limit: [X] req/min

Request:
{
  "field": "type — description"
}

Response (200):
{
  "field": "type — description"
}

Errors:
- 400: [Validation cases]
- 401: [Unauthorized]
- 403: [Forbidden cases]
- 404: [Not found cases]
- 429: [Rate limited]
```

### Database Schema
```
[Entity] {
  id: UUID (PK)
  [field]: [type] [constraints]
  [fk]: UUID (FK → OtherEntity)
  created_at: timestamp
  updated_at: timestamp
}
```

### Indexes
| Table | Column(s) | Type | Purpose |
|-------|-----------|------|---------|
| [table] | [columns] | [btree/gin] | [Why needed] |

---

## 11. Performance & Security

### Performance Budgets
| Metric | Target | Hard Limit |
|--------|--------|------------|
| Initial Bundle Size | < [X] MB | [X] MB |
| Time to Interactive | < [X] s | [X] s |
| LCP (Largest Contentful Paint) | < [X] s | [X] s |
| API Response (p95) | < [X] ms | [X] ms |
| FPS (if game) | [60] | [30] |

### Security Requirements
| Requirement | Implementation |
|-------------|----------------|
| Input Validation | [All endpoints, Zod schemas] |
| CSRF Protection | [Token-based] |
| XSS Prevention | [CSP headers, sanitization] |
| SQL Injection | [Parameterized queries/ORM] |
| Rate Limiting | [X req/min on auth endpoints] |
| Secrets Management | [Env vars, never committed] |
| Anti-cheat (if game) | [Server-authoritative state] |

### Compliance
| Standard | Requirements | Status |
|----------|--------------|--------|
| [GDPR] | [Data deletion, export] | [Planned] |
| [HIPAA] | [N/A] | — |

### Platform Compatibility
| Platform | Support | Min Version |
|----------|---------|-------------|
| Chrome | Full | [X] |
| Firefox | Full | [X] |
| Safari | Full | [X] |
| Edge | Full | [X] |
| Mobile Safari | Full | [iOS X] |
| Mobile Chrome | Full | [Android X] |

---

## 12. Operational Requirements (The "After")

### Localization (i18n)
| Aspect | Requirement |
|--------|-------------|
| **v1 Languages** | [English only / + Spanish, etc.] |
| **Translation Scope** | [UI, Emails, Docs] |
| **i18n Framework** | [next-intl, i18next, etc.] |

### Accessibility (a11y)
| Requirement | Standard |
|-------------|----------|
| **WCAG Level** | [AA / AAA / Best effort] |
| **Keyboard Navigation** | [Full / Partial] |
| **Screen Reader** | [Yes / No] |
| **Color Contrast** | [4.5:1 minimum] |

### Admin & Support Tools
| Tool | Purpose | Priority |
|------|---------|----------|
| [User Management] | [View, edit, delete users] | P0 |
| [Content Moderation] | [Flag, remove content] | P1 |
| [Refund Processing] | [Issue refunds] | P1 |
| [Analytics Dashboard] | [Key metrics view] | P1 |

### Data Management
| Aspect | Policy |
|--------|--------|
| **Backup Strategy** | [Daily automated / PITR] |
| **Retention** | [X days / forever] |
| **User Data Export** | [GDPR: Yes] |
| **User Data Deletion** | [GDPR: Yes, within X days] |

---

## 13. Go-to-Market Strategy

### Release Phases
| Phase | Audience | Criteria to Advance |
|-------|----------|---------------------|
| **Alpha** | Internal team | [Core loop works] |
| **Beta** | Waitlist (N users) | [Stability, feedback positive] |
| **Canary** | 5% of traffic | [Metrics meet targets] |
| **GA** | 100% | [All criteria met] |

### Marketing Assets Required
| Asset | Owner | Status |
|-------|-------|--------|
| Screenshots (X) | [Name] | [Not started] |
| Trailer/Demo | [Name] | [Not started] |
| Social Copy | [Name] | [Not started] |
| Press Kit | [Name] | [Not started] |

### Launch Checklist
- [ ] All P0 features complete
- [ ] Performance budgets met
- [ ] Security audit passed
- [ ] Analytics instrumented
- [ ] Support documentation ready
- [ ] Rollback plan tested

### Rollback Plan
| Trigger | Action | Timeline |
|---------|--------|----------|
| [Crash rate > X%] | [Revert deploy] | [< 5 min] |
| [Error rate > X%] | [Feature flag off] | [< 2 min] |
| [Negative feedback spike] | [Assess + communicate] | [< 1 hr] |

---

## 14. Scope & Boundaries

### v1 Scope (Must Ship)
- [ ] [Feature 1]
- [ ] [Feature 2]
- [ ] [Feature 3]

### v2 Scope (Deferred)
| Feature | Reason | Target |
|---------|--------|--------|
| [Feature] | [Why deferred] | v2 |
| [Feature] | [Why deferred] | v2 |

### Out of Scope (Not Building)
- [Feature] — [Why not / whose problem]
- [Feature] — [Why not / whose problem]

### Open Questions
- [ ] [Unresolved decision]
- [ ] [Needs more research]

### Risks & Mitigations
| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| [Risk] | H/M/L | H/M/L | [Strategy] |

---

## 15. Implementation Guidance

### Project Structure
```
[project-name]/
├── src/
│   ├── app/              # [Routes/Pages]
│   ├── components/       # [Shared UI]
│   ├── features/         # [Feature modules]
│   │   └── [feature]/
│   │       ├── components/
│   │       ├── hooks/
│   │       ├── api/
│   │       └── types.ts
│   ├── lib/              # [Utilities]
│   └── types/            # [Shared types]
├── prisma/               # [DB schema]
├── public/               # [Static assets]
└── tests/                # [Test files]
```

### Coding Patterns
| Pattern | Use | Avoid |
|---------|-----|-------|
| [Pattern] | [When to use] | [Anti-pattern] |

### Testing Strategy
| Type | Framework | Coverage |
|------|-----------|----------|
| Unit | [Vitest] | [X%] |
| Integration | [Vitest] | [Critical paths] |
| E2E | [Playwright] | [Happy paths] |

### Documentation Requirements
- [ ] README with setup instructions
- [ ] API docs (OpenAPI/Swagger)
- [ ] Architecture diagram
- [ ] Deployment runbook

---

## Appendix

### Glossary
| Term | Definition |
|------|------------|
| [Term] | [Definition] |

### References
- [Design files]
- [Technical docs]
- [Competitor analysis]
- [User research]

---

*Generated by Claude Code — Start Project Skill (Gold Standard)*
