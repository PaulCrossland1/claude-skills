# Discovery Question Phases — Gold Standard PRD

Iterative questioning phases to produce a zero-ambiguity blueprint.
Use AskUserQuestion tool for each phase. Ask 2-4 questions per turn maximum.

---

## Phase 1: Executive Context (The "Why")

**Goal**: Establish strategic foundation and ownership

### Questions

1. **Document Control**
   - "Who owns this PRD?" (Product Manager, Tech Lead, Founder)
   - "Who are the key reviewers/stakeholders?"
   - "What's the target approval date?"

2. **Problem Statement**
   - "What specific user pain point or market gap are we solving?"
   - "How are users solving this today? What's broken about that?"
   - "Why is NOW the right time to build this?"

3. **Strategic Alignment**
   - "What company OKR or goal does this support?"
   - "How does this fit into the broader product roadmap?"
   - "What's the opportunity cost of NOT building this?"

---

## Phase 2: User Personas

**Goal**: Define exactly who we're building for

### Questions

1. **Primary Persona**
   - "Give this persona a name and describe them" (e.g., "Bored at Work Bill")
   - "What's their context when using this?" (At desk, on commute, etc.)
   - "What's their motivation?" (Kill time, compete, relax, learn)
   - "What's their technical sophistication?"

2. **Secondary Personas** (if applicable)
   - "Are there other distinct user types?"
   - For each: name, context, motivation, tech level

3. **Anti-Personas**
   - "Who is this explicitly NOT for?"
   - "What user behaviors would indicate misfit?"

---

## Phase 3: Success Metrics (The "Scoreboard")

**Goal**: Define how we measure success unambiguously

### Questions

1. **North Star Metric**
   - "What single metric defines success?"
   - "What's the target?" (e.g., "D1 Retention > 20%", "Time to value < 30s")

2. **Secondary Metrics**
   - "What supporting health metrics matter?"
   - Examples: DAU, Avg session length, Conversion rate, NPS

3. **Guardrail Metrics**
   - "What must NOT get worse?"
   - Examples: Server cost per user < $X, Crash rate < X%, Error rate < X%

4. **Instrumentation Plan**
   - "What analytics events need to be fired?"
   - For each event: name, properties, trigger condition
   - Example: `race_start { kart_type, lobby_id, player_count }`

---

## Phase 4: User Stories & Journeys

**Goal**: Map the complete user experience

### Questions

1. **Core User Stories**
   - "List the key user stories in format: As a [persona], I want [action], so that [benefit]"
   - Prioritize: Must-have vs Nice-to-have

2. **User Flows**
   - "Walk through the primary user journey step by step"
   - "What's the happy path from first touch to core value?"
   - "What are the key decision points?"

3. **Entry Points**
   - "How do users discover/arrive at this?"
   - "What's the first thing they see?"

---

## Phase 5: Functional Requirements — Core Features

**Goal**: Define what the system does in detail

### Questions

1. **Feature Inventory**
   - "List every feature/capability needed for v1"
   - Group into: Core (must ship), Important (should ship), Nice-to-have

2. **Feature Details**
   - For each core feature:
     - "What inputs does it take?"
     - "What outputs does it produce?"
     - "What's the user interaction model?"

3. **Data Requirements**
   - "What data entities exist?" (Users, Items, Sessions, etc.)
   - "What are the relationships between them?"

---

## Phase 6: Functional Requirements — Logic & Algorithms

**Goal**: Define the math and business rules precisely

### Questions

1. **Calculations & Formulas**
   - "Are there any calculations, scoring, or algorithms?"
   - "Write out the actual formulas"
   - Example: `Top_Speed = Base_Speed + (Engine_Level * 1.5)`

2. **Business Rules**
   - "What rules govern behavior?"
   - "What conditions trigger what outcomes?"
   - Format: `IF [condition] THEN [action]`

3. **State Machines**
   - "What are the possible states an entity can be in?"
   - "What triggers transitions between states?"
   - Example: `Idle → Matchmaking → Lobby → Racing → Results → Idle`

---

## Phase 7: Edge Cases (The "What Ifs")

**Goal**: Handle every unhappy path

### Questions

1. **User Edge Cases**
   - "What if user disconnects mid-action?"
   - "What if user has no data/is new?"
   - "What if user tries to game the system?"

2. **Data Edge Cases**
   - "What if data is missing or malformed?"
   - "What if two events happen at the exact same time?"
   - "What are the max/min limits?"

3. **System Edge Cases**
   - "What if a dependent service fails?"
   - "What if load exceeds expectations?"
   - "What's the graceful degradation strategy?"

---

## Phase 8: UX & Design — Screens & States

**Goal**: Define every screen and its states

### Questions

1. **Screen Inventory**
   - "List every screen/view in the product"
   - For each: primary purpose, primary action

2. **UI States** (for each key screen)
   - "What does the Ideal State look like?" (Populated with data)
   - "What does the Empty State look like?" (First time user)
   - "What does the Loading State look like?" (Spinners, skeletons)
   - "What does the Error State look like?" (Failed to load)

3. **Wireframes/Mockups**
   - "Do you have existing designs?" (Figma/Sketch links)
   - "What's the design fidelity needed?" (Wireframe, Mockup, Polished)

---

## Phase 9: UX & Design — Interactions & Feedback

**Goal**: Define micro-interactions and sensory design

### Questions

1. **Interaction Patterns**
   - "What happens on click/tap/hover for key elements?"
   - "Any drag-and-drop, swipe, or gesture interactions?"
   - "Keyboard shortcuts needed?"

2. **Animations & Transitions**
   - "What transitions between states/screens?"
   - "Any celebratory animations?" (Success, achievement, win)

3. **Sound & Haptics** (if applicable)
   - "Does this need sound effects? What triggers them?"
   - "Background music? Loops?"
   - "Haptic feedback on mobile?"

---

## Phase 10: Technical Stack — Core

**Goal**: Lock down primary technology choices

### Questions

1. **Frontend**
   - "What frontend framework?" (React, Next.js, Vue, Svelte, Vanilla)
   - "UI component library?" (shadcn/ui, MUI, Tailwind only)
   - "TypeScript or JavaScript?"

2. **Backend**
   - "What backend runtime/framework?" (Node/Express, Python/FastAPI, Go, etc.)
   - "Monolith or microservices?"
   - "Serverless or traditional?"

3. **API Style**
   - "REST, GraphQL, tRPC, gRPC, or WebSocket-primary?"
   - "API versioning strategy?"

---

## Phase 11: Technical Stack — Data Layer

**Goal**: Define database, caching, storage, search

### Questions

1. **Primary Database**
   - "What database type?" (PostgreSQL, MySQL, MongoDB, Redis, SQLite)
   - "What hosting provider?" (Supabase, Neon, PlanetScale, Atlas, Upstash)
   - "ORM choice?" (Prisma, Drizzle, TypeORM, Raw SQL)

2. **Caching**
   - "Do you need caching?" (Redis, Memcached, In-memory, None)
   - "What will be cached?" (Sessions, API responses, Game state)

3. **File Storage**
   - "Will users upload files?" (S3, R2, Supabase Storage, Cloudinary, None)
   - "File types and size limits?"

4. **Search**
   - "Need search?" (PostgreSQL FTS, Algolia, Meilisearch, Typesense, None)

---

## Phase 12: Technical Stack — Auth & Identity

**Goal**: Define authentication and authorization completely

### Questions

1. **Auth Requirement**
   - "Does this need auth?" (User accounts, Admin only, Public, Anonymous+Optional)

2. **Auth Provider** (if needed)
   - "Which provider?" (Clerk, Auth0, Supabase Auth, NextAuth, Firebase, Custom JWT)
   - "Login methods?" (Email+Password, Magic Link, OAuth, SSO/SAML)
   - "Which OAuth providers?" (Google, GitHub, Apple, Discord, etc.)

3. **Authorization**
   - "What's the authorization model?" (Simple, RBAC, Team-based, Permission-based)
   - "Define roles and permissions"

4. **Sessions**
   - "Session strategy?" (JWT, Database, Redis, Provider-managed)
   - "Session duration?"

---

## Phase 13: Technical Stack — Infrastructure

**Goal**: Define hosting, CI/CD, environments

### Questions

1. **Hosting**
   - "Where will this be hosted?" (Vercel, Railway, Render, Fly.io, AWS, GCP)
   - "Region requirements?"

2. **Environments**
   - "What environments?" (Dev, Staging, Production, Multi-region)
   - "PR preview deployments?"

3. **CI/CD**
   - "What CI/CD?" (GitHub Actions, Vercel built-in, CircleCI)
   - "What runs on PR?" (Lint, Test, Build, Preview)

4. **Domain & SSL**
   - "Domain name?"
   - "DNS provider?" (Cloudflare, Route53, Vercel)
   - "SSL handling?" (Platform, Cloudflare, Let's Encrypt)

---

## Phase 14: Technical Stack — Third-Party Services

**Goal**: Identify all external service dependencies

### Questions

1. **Communication**
   - "Email service?" (Resend, SendGrid, Postmark, SES, None)
   - "Push notifications?" (OneSignal, Firebase, None)
   - "SMS?" (Twilio, None)

2. **Payments** (if applicable)
   - "Payment processor?" (Stripe, Paddle, LemonSqueezy, None)
   - "Pricing model?" (One-time, Subscription, Usage-based, Freemium)

3. **Analytics & Monitoring**
   - "Product analytics?" (PostHog, Mixpanel, Amplitude, GA, None)
   - "Error tracking?" (Sentry, Bugsnag, None)
   - "Logging/monitoring?" (Datadog, BetterStack, CloudWatch, None)

4. **Other Services**
   - "Feature flags?" (PostHog, LaunchDarkly, Statsig, None)
   - "Any other third-party APIs?"

---

## Phase 15: API Contracts & System Architecture

**Goal**: Define technical contracts before coding

### Questions

1. **System Architecture**
   - "Client/Server model - what runs where?"
   - "Real-time requirements?" (WebSockets, SSE, Polling)
   - "Background job needs?" (Queues, Cron, Serverless scheduled)

2. **API Contract Design**
   - "For each major API endpoint, what are inputs and outputs?"
   - "What HTTP methods and status codes?"
   - "Request/response payload shapes?"

3. **Database Schema**
   - "What are the core entities and their fields?"
   - "What are the relationships?"
   - "What indexes are needed for performance?"

---

## Phase 16: Performance & Security

**Goal**: Define non-functional requirements with hard limits

### Questions

1. **Performance Budgets**
   - "Initial bundle size limit?" (e.g., < 2MB)
   - "Time to Interactive target?" (e.g., < 1.5s)
   - "API response time (p95)?" (e.g., < 500ms)
   - "Core Web Vitals targets?"

2. **Security**
   - "Compliance requirements?" (GDPR, HIPAA, SOC2, PCI-DSS, None)
   - "Sensitive data types?" (PII, Financial, Health)
   - "Anti-cheat/anti-abuse measures?"
   - "Rate limiting requirements?"

3. **Platform Compatibility**
   - "Browser support matrix?" (Chrome, Firefox, Safari, Edge)
   - "Device support?" (Desktop, Mobile, Tablet)
   - "Min browser versions?"

---

## Phase 17: Operational Requirements (The "After")

**Goal**: Define post-launch operational needs

### Questions

1. **Localization (i18n)**
   - "Multi-language support needed?"
   - "Which languages for v1?"
   - "What content needs translation?" (UI, Emails, Support docs)

2. **Accessibility (a11y)**
   - "Accessibility standard?" (WCAG AA, WCAG AAA, Best effort)
   - "Keyboard navigation required?"
   - "Screen reader support?"

3. **Admin & Support Tools**
   - "What admin capabilities are needed?"
   - Examples: User management, Content moderation, Refunds, Ban/kick
   - "What dashboards/reports for ops team?"

4. **Data Management**
   - "Backup strategy?"
   - "Data retention policy?"
   - "User data export/deletion (GDPR)?"

---

## Phase 18: Go-to-Market Strategy

**Goal**: Define release and rollback plan

### Questions

1. **Release Phases**
   - "What's the release strategy?"
   - Options: Alpha (Internal) → Beta (Waitlist) → Canary (5%) → GA (100%)
   - "Criteria for each phase advancement?"

2. **Marketing Assets**
   - "What marketing materials are needed?"
   - Examples: Screenshots, Trailer, Social copy, Press kit
   - "Who creates these?"

3. **Launch Checklist**
   - "What must be true before launch?"
   - "Go/No-Go criteria?"

4. **Rollback Plan**
   - "What's the specific trigger to rollback?"
   - "How fast can you rollback?"
   - "What's the communication plan if things break?"

---

## Phase 19: Scope Boundaries

**Goal**: Define what's in and what's out

### Questions

1. **v1 Scope (Must Ship)**
   - "What's the absolute minimum for v1?"
   - "What makes this a complete v1 vs a broken v0.5?"

2. **v2 Scope (Deferred)**
   - "What's explicitly deferred to v2?"
   - "Why deferred?"

3. **Out of Scope (Never/Not Us)**
   - "What are we explicitly NOT building?"
   - "Any related features that are someone else's problem?"

4. **Open Questions**
   - "What decisions are still unresolved?"
   - "What needs more research?"

5. **Risks**
   - "What are the biggest risks?"
   - "What's the mitigation strategy?"

---

## Phase 20: Implementation Preferences

**Goal**: Guide the actual build

### Questions

1. **Code Organization**
   - "Preferred folder structure?" (Feature-based, Layer-based, Domain-driven)
   - "Naming conventions?"

2. **Patterns**
   - "Patterns to follow?"
   - "Patterns to avoid?"
   - "Existing code to reference?"

3. **Testing**
   - "Testing requirements?" (Unit, Integration, E2E)
   - "Framework preference?" (Vitest, Jest, Playwright, Cypress)
   - "Coverage targets?"

4. **Documentation**
   - "What documentation is needed?"
   - "API docs?" (OpenAPI/Swagger)
   - "Architecture diagrams?"

---

## Phase 21: Code Standards & Conventions

**Goal**: Define coding standards that agents will follow during implementation

### Questions

1. **Function Style**
   - "Function declaration style?" (`function` keyword vs arrow functions)
   - "When to use each?" (Top-level = function, callbacks = arrow)

2. **Type Annotations**
   - "TypeScript strictness?" (Strict, Moderate, Loose)
   - "Explicit return types on functions?" (Always, Public only, Inferred)
   - "Interface vs Type preference?" (Interface for objects, Type for unions)

3. **Import Organization**
   - "Import sorting order?" (External → Internal → Relative)
   - "Named vs default exports?" (Prefer named, Default for components)
   - "Barrel files (index.ts)?" (Yes for modules, No for deep imports)

4. **Error Handling**
   - "Error handling pattern?" (Try/catch, Result types, Error boundaries)
   - "Logging conventions?" (Console, Logger service, Silent in prod)

5. **Naming Conventions**
   - "Variable/function naming?" (camelCase)
   - "Component naming?" (PascalCase)
   - "File naming?" (kebab-case, camelCase, PascalCase)
   - "Constants?" (SCREAMING_SNAKE_CASE, camelCase)

6. **Control Flow**
   - "Ternary usage?" (Simple only, Never nested, Prefer if/else)
   - "Early returns?" (Prefer early returns vs single return)
   - "Guard clauses?" (Yes, validate inputs first)

7. **Formatting & Linting**
   - "Formatter?" (Prettier, ESLint --fix, Biome)
   - "ESLint config?" (Strict, Recommended, Custom)
   - "Pre-commit hooks?" (Husky + lint-staged, None)

8. **Comments & Documentation**
   - "JSDoc on public functions?" (Required, Optional, None)
   - "Inline comments?" (Explain why, not what)
   - "TODO format?" (`// TODO(author): description`)

### Example AskUserQuestion

```json
{
  "questions": [
    {
      "question": "What's your preference for function declarations?",
      "header": "Functions",
      "options": [
        {"label": "function keyword (Recommended)", "description": "Top-level functions use function keyword"},
        {"label": "Arrow functions", "description": "All functions use arrow syntax"},
        {"label": "Mixed", "description": "function for top-level, arrow for callbacks"}
      ],
      "multiSelect": false
    },
    {
      "question": "How strict should TypeScript be?",
      "header": "TypeScript",
      "options": [
        {"label": "Strict (Recommended)", "description": "strict: true, explicit types"},
        {"label": "Moderate", "description": "Some any allowed, inferred types OK"},
        {"label": "Loose", "description": "Focus on functionality over types"}
      ],
      "multiSelect": false
    }
  ]
}
```

### Why This Matters

Code standards captured here flow into:
- `.claude/ARCHITECTURE.md` — Patterns section
- `.claude/DECISIONS.md` — ADRs for style choices
- **003-execute-tasks Step 8.5** — Code simplifier uses these standards

Without explicit standards, each subagent invents its own style, creating inconsistent code.

---

## Question Delivery Guidelines

### AskUserQuestion Tool Usage

- Maximum 4 questions per turn
- Use multiSelect when multiple answers valid
- Provide 2-4 options with descriptions
- Reference previous answers to show continuity

### Adaptive Rules

- **Skip phases** that don't apply:
  - Skip Auth (12) if no authentication
  - Skip Payments (14) if no monetization
  - Skip i18n (17) if English-only v1
  - Skip GTM (18) for internal tools

- **Consolidate phases** when user has clear preferences:
  - Tech stack phases (10-14) can be 2-3 rounds if stack is known

- **Dive deeper** when answers reveal complexity:
  - Complex algorithms need detailed formulas
  - Multi-tenant needs detailed role definitions

### Between Phases

After each phase, briefly summarize what was captured before moving on.
Example: "Got it — PostgreSQL on Supabase with Prisma, Redis caching for game state. Moving to Auth..."
