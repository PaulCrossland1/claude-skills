# Discovery Question Phases — Adaptive by Project Type

Iterative questioning phases to produce a zero-ambiguity blueprint.
Use AskUserQuestion tool for each phase. Ask 2-4 questions per turn maximum.

**Adapt questions based on project type:**
- 🆕 **New Product/Feature** — Full discovery, choose technologies
- 🔧 **Refactor/Improvement** — Document current state, define target state
- 🐛 **Bug Fix** — Reproduction, root cause, affected areas
- 🔒 **Security Audit** — Threat actors, attack surface, vulnerabilities
- ⚡ **Performance** — Bottlenecks, metrics, profiling
- 🔗 **Integration/Migration** — Systems mapping, data flows, cutover

---

## Phase 1: Executive Context (The "Why")

**Goal**: Establish foundation, ownership, and motivation

### Questions

1. **Document Control**
   - "Who owns this work?" (Product Manager, Tech Lead, Security Team, etc.)
   - "Who are the key stakeholders/reviewers?"
   - "What's the target completion date?"

2. **Problem Statement** (adapt by type)
   - 🆕 **New Product/Feature**: "What user pain point or market gap are we solving?"
   - 🔧 **Refactor**: "What's wrong with the current implementation? What pain does it cause?"
   - 🐛 **Bug Fix**: "What's the user-facing impact? How severe is it?"
   - 🔒 **Security**: "What triggered this audit? (Incident, compliance, proactive)"
   - ⚡ **Performance**: "What performance issues are users experiencing?"
   - 🔗 **Integration**: "Why do these systems need to connect? What's the business driver?"

3. **Context & Priority**
   - "Why is this work important NOW?"
   - "What's the impact of NOT doing this?"
   - "Any relevant history or previous attempts?"

---

## Phase 2: Personas & Stakeholders

**Goal**: Define who's affected by this work

### Questions (adapt by type)

**🆕 New Product/Feature — User Personas:**
1. **Primary Persona**
   - "Describe the primary user" (name, context, motivation, tech level)
   - "What's their context when using this?"
2. **Secondary Personas** — Other user types affected
3. **Anti-Personas** — Who is this NOT for?

**🔒 Security Audit — Threat Actors:**
1. **External Threats**
   - "What types of attackers are we defending against?" (Script kiddies, organized crime, nation-state, insider)
   - "What are their motivations?" (Financial, data theft, disruption, espionage)
2. **Internal Risks**
   - "Any insider threat concerns?" (Malicious employees, compromised accounts)
3. **Attack Surface Awareness**
   - "What assets are most valuable to attackers?"

**🔧 Refactor / ⚡ Performance / 🐛 Bug Fix — Stakeholders:**
1. **Affected Users**
   - "Which user segments are impacted?"
   - "How are they affected?" (Blocked, degraded experience, workarounds)
2. **Internal Stakeholders**
   - "Who requested this work?"
   - "Who needs to approve changes?"
3. **Downstream Dependencies**
   - "What teams/systems depend on this code?"

**🔗 Integration/Migration — Systems & Owners:**
1. **Source System** — Owner, capabilities, constraints
2. **Target System** — Owner, capabilities, constraints
3. **Data Owners** — Who owns the data being moved/connected?

---

## Phase 3: Success Metrics (The "Scoreboard")

**Goal**: Define how we measure success unambiguously

### Questions (adapt by type)

**🆕 New Product/Feature:**
1. **North Star Metric** — Single metric that defines success (e.g., D1 Retention > 20%)
2. **Secondary Metrics** — Supporting health metrics (DAU, conversion, NPS)
3. **Guardrail Metrics** — What must NOT get worse (cost, error rate)
4. **Instrumentation** — Analytics events to fire

**🔒 Security Audit:**
1. **Coverage Metrics** — % of codebase reviewed, endpoints tested
2. **Finding Metrics** — Vulnerabilities by severity (Critical/High/Medium/Low)
3. **Remediation Metrics** — Time to fix, % resolved before deadline
4. **Compliance** — Standards to verify against (OWASP Top 10, SOC2, etc.)

**⚡ Performance:**
1. **Baseline Metrics** — Current state (p50, p95, p99 latency; throughput; resource usage)
2. **Target Metrics** — What "good" looks like (e.g., p95 < 200ms)
3. **Guardrails** — What must not regress (memory, CPU, error rate)
4. **Load Profile** — Expected traffic patterns, peak load

**🐛 Bug Fix:**
1. **Resolution Verification** — How do we know it's fixed? (Specific test, user confirmation)
2. **Regression Prevention** — Tests to add to prevent recurrence
3. **Impact Confirmation** — Affected users can now complete their task

**🔧 Refactor:**
1. **Before/After Comparison** — Measurable improvement (lines of code, complexity, test coverage)
2. **Behavior Preservation** — All existing tests still pass
3. **Non-Regression** — No performance degradation

**🔗 Integration/Migration:**
1. **Data Integrity** — 100% of records migrated correctly
2. **Downtime Budget** — Maximum acceptable outage
3. **Rollback Criteria** — When to abort and restore

---

## Phase 4: Scope & Scenarios

**Goal**: Define what's being done and the key scenarios

### Questions (adapt by type)

**🆕 New Product/Feature — User Stories:**
1. **Core User Stories** — "As a [persona], I want [action], so that [benefit]"
2. **User Flows** — Happy path from entry to value
3. **Entry Points** — How users discover/arrive

**🐛 Bug Fix — Reproduction & Impact:**
1. **Reproduction Steps**
   - "Exact steps to reproduce the bug"
   - "Environment details" (browser, OS, account type)
   - "Frequency" (always, sometimes, specific conditions)
2. **Expected vs Actual** — What should happen vs what does happen
3. **Impact Scope** — Which users affected, how severely

**🔒 Security — Attack Scenarios:**
1. **Attack Vectors to Test**
   - "What attack types are in scope?" (Injection, XSS, CSRF, auth bypass, etc.)
   - "Which endpoints/features are highest risk?"
2. **Threat Scenarios** — Specific attack stories to validate against
3. **Assets at Risk** — What could be compromised if attack succeeds

**⚡ Performance — Bottleneck Identification:**
1. **Slow Operations** — Which specific operations are slow?
2. **User-Facing Symptoms** — What do users experience?
3. **Profiling Data** — Any existing measurements, flame graphs, traces?

**🔧 Refactor — Change Scope:**
1. **Current State** — What does the code look like now?
2. **Target State** — What should it look like after?
3. **Change Boundaries** — What's in scope to change, what's off-limits?

**🔗 Integration/Migration — Data Flows:**
1. **Data to Move/Connect** — What entities, what volume?
2. **Transformation Rules** — How does data map between systems?
3. **Sync Requirements** — One-time, ongoing, real-time?

---

## Phase 5: Requirements & Scope Details

**Goal**: Define what needs to be done in detail

### Questions (adapt by type)

**🆕 New Product/Feature — Functional Requirements:**
1. **Feature Inventory** — List features, group by priority (Core, Important, Nice-to-have)
2. **Feature Details** — For each: inputs, outputs, interaction model
3. **Data Requirements** — Entities, relationships, storage

**🐛 Bug Fix — Root Cause Analysis:**
1. **Hypothesis** — What do you think is causing the bug?
2. **Affected Code** — Which files/functions are likely involved?
3. **Related Changes** — Any recent deployments that might be related?

**🔒 Security — Audit Scope:**
1. **Components to Audit**
   - "Which codebases/repos are in scope?"
   - "Which are explicitly out of scope?"
2. **Vulnerability Categories**
   - "Priority vulnerabilities to check" (OWASP Top 10, specific concerns)
3. **Access Required**
   - "What access levels will you test?" (Anonymous, user, admin)
   - "Need test accounts created?"

**⚡ Performance — Optimization Targets:**
1. **Hot Paths** — Which code paths need optimization?
2. **Resource Constraints** — CPU, memory, network, database limits
3. **Caching Opportunities** — What can be cached?

**🔧 Refactor — Current vs Target:**
1. **Current Implementation** — Describe what exists
2. **Pain Points** — What's wrong with it?
3. **Target Architecture** — What should it look like?

**🔗 Integration — Endpoints & Contracts:**
1. **Source APIs** — Available endpoints, auth, rate limits
2. **Target APIs** — Available endpoints, auth, rate limits
3. **Data Mapping** — Field-by-field mapping between systems

---

## Phase 6: Logic & Rules

**Goal**: Define business rules, algorithms, state machines

**Applies to**: 🆕 New Product/Feature, 🔧 Refactor, 🔗 Integration
**Skip for**: 🐛 Bug Fix, 🔒 Security (unless auditing specific logic), ⚡ Performance

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

**🔗 Integration Note**: Document transformation rules here — how data converts between systems.

---

## Phase 7: Edge Cases & Failure Modes

**Goal**: Handle unhappy paths and failure scenarios

**Applies to**: 🆕 New Product/Feature, 🔧 Refactor
**Alternative framing for**: 🔒 Security, ⚡ Performance, 🔗 Integration
**Skip for**: 🐛 Bug Fix

### Questions (adapt by type)

**🆕 New Product/Feature — Edge Cases:**
1. **User Edge Cases** — Disconnects, empty state, gaming the system
2. **Data Edge Cases** — Missing data, malformed input, race conditions
3. **System Edge Cases** — Service failures, overload, degradation strategy

**🔒 Security — Exploit Scenarios:**
1. **Input Manipulation** — What happens with malicious input?
2. **Authentication Bypass** — Session hijacking, token theft scenarios
3. **Authorization Escalation** — Can users access others' data?
4. **Rate Limit Evasion** — How could limits be circumvented?

**⚡ Performance — Load Scenarios:**
1. **Peak Load** — What happens at 10x normal traffic?
2. **Degradation Behavior** — How should system degrade under load?
3. **Recovery** — How quickly does system recover after spike?
4. **Cold Start** — Cache miss, connection pool exhaustion scenarios

**🔗 Integration/Migration — Failure Modes:**
1. **Partial Failure** — What if migration fails halfway?
2. **Data Conflicts** — How to handle conflicting records?
3. **Rollback Scenario** — Can you reverse the migration?
4. **Sync Failures** — What happens when sync breaks?

---

## Phase 8: UX & Design — Screens & States

**Goal**: Define every screen and its states

**Applies to**: 🆕 New Product/Feature, 🔧 Refactor (if UI changes)
**Skip for**: 🐛 Bug Fix, 🔒 Security, ⚡ Performance, 🔗 Integration (unless UI involved)

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

**Applies to**: 🆕 New Product/Feature (especially games, interactive apps)
**Skip for**: 🐛 Bug Fix, 🔒 Security, ⚡ Performance, 🔗 Integration, most 🔧 Refactors

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

**Goal**: Define or document primary technology choices

### Questions (adapt by type)

**🆕 New Product — Choose Stack:**
1. **Frontend** — Framework (React, Next.js, Vue), component library, TypeScript?
2. **Backend** — Runtime (Node, Python, Go), architecture (monolith, microservices, serverless)
3. **API Style** — REST, GraphQL, tRPC, WebSocket?

**All Other Types — Document Existing Stack:**
1. **Current Stack**
   - "What's the existing tech stack?" (Frontend, backend, database)
   - "What version are we on?"
   - "Any known tech debt or outdated dependencies?"
2. **Constraints**
   - "Any technology constraints we must work within?"
   - "Frozen dependencies or locked versions?"
3. **Integration Points**
   - "What systems does this code interact with?"

---

## Phase 11: Technical Stack — Data Layer

**Goal**: Define or document data infrastructure

### Questions (adapt by type)

**🆕 New Product — Choose Data Stack:**
1. **Primary Database** — Type (PostgreSQL, MongoDB), hosting (Supabase, Neon), ORM (Prisma, Drizzle)
2. **Caching** — Redis, Memcached, in-memory?
3. **File Storage** — S3, R2, Cloudinary?
4. **Search** — PostgreSQL FTS, Algolia, Meilisearch?

**All Other Types — Document Existing:**
1. **Current Data Infrastructure**
   - "What databases are in use?"
   - "What's the data model/schema?"
   - "Current caching strategy?"
2. **Data Volumes**
   - "How much data are we dealing with?"
   - "Growth rate?"
3. **Known Data Issues**
   - "Any known data quality problems?"
   - "Performance bottlenecks in data layer?"

**🔗 Integration/Migration — Source & Target Data:**
1. **Source Data** — Schema, volume, access method
2. **Target Data** — Schema, constraints, validation rules
3. **Data Quality** — Cleanup needed? Duplicates?

---

## Phase 12: Technical Stack — Auth & Identity

**Goal**: Define or audit authentication and authorization

### Questions (adapt by type)

**🆕 New Product/Feature — Choose Auth:**
1. **Auth Requirement** — User accounts, admin only, public, optional?
2. **Auth Provider** — Clerk, Auth0, Supabase, NextAuth, custom JWT?
3. **Login Methods** — Email/password, magic link, OAuth, SSO?
4. **Authorization Model** — Simple, RBAC, team-based?
5. **Sessions** — JWT, database, Redis? Duration?

**🔒 Security Audit — Assess Auth:**
1. **Current Auth Implementation**
   - "How is authentication implemented?"
   - "How are sessions managed?"
   - "Where are credentials stored?"
2. **Known Auth Concerns**
   - "Any suspected auth vulnerabilities?"
   - "Recent auth-related incidents?"
3. **Auth Testing Scope**
   - "Test password reset flow?"
   - "Test OAuth integrations?"
   - "Test session management?"

**All Other Types — Document Existing:**
1. **Current Auth** — What's in place? Any changes needed?
2. **Auth Constraints** — Must preserve existing auth? Backwards compatibility?

---

## Phase 13: Technical Stack — Infrastructure

**Goal**: Define or document hosting, CI/CD, environments

### Questions (adapt by type)

**🆕 New Product — Choose Infrastructure:**
1. **Hosting** — Vercel, Railway, AWS, GCP? Region requirements?
2. **Environments** — Dev, staging, production? PR previews?
3. **CI/CD** — GitHub Actions, Vercel built-in? What runs on PR?
4. **Domain & SSL** — Domain name, DNS provider, SSL handling?

**All Other Types — Document Existing:**
1. **Current Infrastructure**
   - "Where is this deployed?"
   - "What's the CI/CD pipeline?"
   - "How do deployments work?"
2. **Environment Access**
   - "Which environments can we test in?"
   - "How to access staging/dev?"
3. **Deployment Constraints**
   - "Deployment windows?"
   - "Approval process?"

**🔒 Security Audit — Infrastructure Assessment:**
1. **Secrets Management** — How are secrets stored and rotated?
2. **Network Security** — VPCs, firewalls, WAF?
3. **Access Controls** — Who has deploy access?

---

## Phase 14: Technical Stack — Third-Party Services

**Goal**: Identify or document external service dependencies

### Questions (adapt by type)

**🆕 New Product — Choose Services:**
1. **Communication** — Email (Resend, SendGrid), push, SMS?
2. **Payments** — Stripe, Paddle? Pricing model?
3. **Analytics & Monitoring** — PostHog, Mixpanel? Sentry? Datadog?
4. **Other Services** — Feature flags? Other APIs?

**All Other Types — Document Existing:**
1. **Current Integrations**
   - "What third-party services are in use?"
   - "Which are relevant to this work?"
2. **API Constraints**
   - "Rate limits to be aware of?"
   - "Cost implications?"

**🔒 Security Audit — Third-Party Risk:**
1. **Vendor Assessment** — Which vendors have access to sensitive data?
2. **API Key Security** — How are third-party API keys stored?
3. **Data Sharing** — What data is sent to third parties?

---

## Phase 15: Architecture & Affected Areas

**Goal**: Define or document system architecture and affected areas

### Questions (adapt by type)

**🆕 New Product/Feature — Design Architecture:**
1. **System Architecture** — Client/server model, real-time needs, background jobs
2. **API Contract Design** — Endpoints, methods, payloads
3. **Database Schema** — Entities, fields, relationships, indexes

**🐛 Bug Fix — Affected Areas:**
1. **Code Areas** — Which modules/files are affected?
2. **Dependencies** — What code depends on the affected area?
3. **Test Coverage** — Existing tests for this area?

**🔒 Security Audit — Attack Surface:**
1. **Entry Points** — All external-facing endpoints
2. **Authentication Points** — Where auth is checked
3. **Data Flows** — How sensitive data moves through the system
4. **Trust Boundaries** — Where do we trust input vs validate?

**⚡ Performance — Performance Profile:**
1. **Current Architecture** — How does data flow?
2. **Hot Paths** — Which code paths are performance-critical?
3. **Database Queries** — Slow queries identified?
4. **Caching** — Current caching strategy? Opportunities?

**🔗 Integration — Integration Points:**
1. **System A Interface** — API endpoints, auth, data format
2. **System B Interface** — API endpoints, auth, data format
3. **Middleware Needs** — Transformation, validation, error handling

---

## Phase 16: Performance & Security

**Goal**: Define non-functional requirements and security posture

### Questions (adapt by type)

**🆕 New Product/Feature — Define Requirements:**
1. **Performance Budgets** — Bundle size, TTI, API response time, Core Web Vitals
2. **Security Requirements** — Compliance (GDPR, SOC2), sensitive data types, rate limiting
3. **Platform Compatibility** — Browsers, devices, minimum versions

**🔒 Security Audit — DEEP DIVE (Primary Focus):**
1. **Vulnerability Categories**
   - "Focus areas?" (OWASP Top 10, specific concerns)
   - "Previous findings to verify remediation?"
2. **Compliance Requirements**
   - "Standards to audit against?" (SOC2, PCI-DSS, HIPAA)
   - "Specific controls to verify?"
3. **Sensitive Data Inventory**
   - "Where is PII stored?"
   - "Where is financial data processed?"
   - "Encryption at rest and in transit?"
4. **Access Controls**
   - "Review admin access patterns?"
   - "Audit logging in place?"
5. **Dependency Security**
   - "Scan dependencies for vulnerabilities?"
   - "Review third-party code?"

**⚡ Performance Optimization — DEEP DIVE (Primary Focus):**
1. **Current Baselines**
   - "What are current metrics?" (p50, p95, p99)
   - "Profiling data available?"
2. **Target Improvements**
   - "What's the target state?"
   - "Which metrics matter most?"
3. **Constraints**
   - "Budget for infrastructure changes?"
   - "Code change restrictions?"
4. **Testing Approach**
   - "Load testing environment?"
   - "Performance regression tests?"

**All Other Types — Document Constraints:**
1. **Existing Performance Requirements** — Any SLAs to maintain?
2. **Security Constraints** — Compliance requirements in place?

---

## Phase 17: Operational Requirements

**Goal**: Define operational needs and ongoing maintenance

**Applies to**: 🆕 New Product/Feature (full), others as relevant
**Skip for**: 🐛 Bug Fix

### Questions (adapt by type)

**🆕 New Product/Feature — Full Operational Planning:**
1. **Localization (i18n)** — Languages needed? Translation scope?
2. **Accessibility (a11y)** — WCAG level? Keyboard nav? Screen readers?
3. **Admin Tools** — User management, moderation, dashboards?
4. **Data Management** — Backup, retention, GDPR compliance?

**🔒 Security Audit — Operational Security:**
1. **Logging & Monitoring** — Security event logging in place?
2. **Incident Response** — Runbook for security incidents?
3. **Access Review** — Process for reviewing access permissions?

**⚡ Performance — Monitoring:**
1. **Performance Monitoring** — Metrics being tracked?
2. **Alerting** — Alerts for performance degradation?
3. **Capacity Planning** — How is scaling handled?

**🔗 Integration/Migration — Ongoing Operations:**
1. **Sync Monitoring** — How to detect sync failures?
2. **Data Reconciliation** — Process for finding mismatches?
3. **Support Runbooks** — How to troubleshoot integration issues?

---

## Phase 18: Rollout & Delivery

**Goal**: Plan how changes will be released

**Skip for**: 🐛 Bug Fix (usually goes direct to prod after testing)

### Questions (adapt by type)

**🆕 New Product/Feature — Go-to-Market:**
1. **Release Phases** — Alpha → Beta → Canary → GA?
2. **Marketing Assets** — Screenshots, trailer, press kit?
3. **Launch Checklist** — Go/No-Go criteria?
4. **Rollback Plan** — Triggers, speed, communication?

**🔒 Security Audit — Remediation Plan:**
1. **Finding Prioritization** — How will findings be prioritized?
2. **Remediation Timeline** — SLAs by severity (Critical: 24h, High: 7d, etc.)?
3. **Verification Process** — How will fixes be verified?
4. **Communication** — Who receives the report? Disclosure timeline?

**⚡ Performance — Rollout Plan:**
1. **Staged Rollout** — Canary deployment? % traffic?
2. **Metrics Monitoring** — What to watch during rollout?
3. **Rollback Triggers** — When to rollback?
4. **Success Criteria** — How to know optimization worked?

**🔧 Refactor — Migration Plan:**
1. **Phased Approach** — All at once or incremental?
2. **Feature Flags** — Can old code run alongside new?
3. **Rollback Strategy** — How to revert if needed?

**🔗 Integration/Migration — Cutover Plan:**
1. **Migration Waves** — What order? Batches?
2. **Downtime Window** — Acceptable outage?
3. **Rollback Procedure** — How to reverse?
4. **Verification Checks** — How to confirm success?

---

## Phase 19: Scope Boundaries

**Goal**: Define what's in and what's out — applies to ALL project types

### Questions (universal, adapt language)

1. **In Scope (Must Do)**
   - 🆕 "What's the absolute minimum for v1?"
   - 🐛 "What needs to be fixed in this effort?"
   - 🔒 "What systems/code are being audited?"
   - ⚡ "What needs to be optimized?"
   - 🔗 "What data/systems are being migrated?"

2. **Deferred (Later)**
   - "What's explicitly deferred to a follow-up?"
   - "Why deferred?" (Time, complexity, dependencies)

3. **Out of Scope (Not This Work)**
   - "What are we explicitly NOT touching?"
   - "What's someone else's responsibility?"

4. **Open Questions**
   - "What decisions are still unresolved?"
   - "What needs more research?"

5. **Risks**
   - "What are the biggest risks?"
   - "What's the mitigation strategy?"
   - 🔒 "What if we find critical vulnerabilities?"
   - 🔗 "What if migration data is corrupt?"

---

## Phase 20: Implementation & Deliverables

**Goal**: Define how work will be done and what will be delivered

### Questions (adapt by type)

**🆕 New Product/Feature — Implementation Preferences:**
1. **Code Organization** — Folder structure, naming conventions
2. **Patterns** — Patterns to follow/avoid, reference code
3. **Testing** — Unit, integration, E2E? Framework? Coverage target?
4. **Documentation** — API docs (OpenAPI), architecture diagrams?

**🐛 Bug Fix — Fix Approach:**
1. **Fix Strategy** — Quick patch or proper fix?
2. **Testing Requirements** — Regression tests to add?
3. **Verification** — How to verify fix works?

**🔒 Security Audit — Deliverables:**
1. **Report Format** — What format? (PDF, Markdown, JIRA tickets)
2. **Finding Detail Level** — POC required? Screenshots?
3. **Remediation Guidance** — Include fix recommendations?
4. **Retesting** — Will you verify fixes?

**⚡ Performance — Deliverables:**
1. **Analysis Report** — Profiling data, bottleneck identification
2. **Recommendations** — Prioritized list of optimizations
3. **Benchmarks** — Before/after measurements

**🔗 Integration/Migration — Deliverables:**
1. **Runbooks** — Migration procedure documentation
2. **Rollback Procedure** — Documented rollback steps
3. **Validation Scripts** — How to verify success

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

### Adaptive Rules by Project Type

**🆕 New Product/Feature:**
- Full discovery, all phases applicable
- Consolidate tech phases (10-14) if stack is known

**🔧 Refactor/Improvement:**
- Skip UX phases (8-9) unless UI changes
- Tech phases = document existing, not choose
- Skip GTM (18), use simple rollout plan

**🐛 Bug Fix:**
- Minimal phases: 1, 3, 4 (repro), 5 (root cause), 15, 19-20
- Skip UX, tech stack, GTM phases

**🔒 Security Audit:**
- Replace personas (2) with threat actors
- Phase 16 is primary focus
- Replace features (5) with audit scope
- Replace GTM (18) with remediation plan

**⚡ Performance:**
- Replace features (5) with optimization targets
- Phase 16 is primary focus
- Replace edge cases (7) with load scenarios
- Skip UX phases (8-9)

**🔗 Integration/Migration:**
- Replace personas (2) with systems & owners
- Replace features (5) with data mapping
- Replace GTM (18) with cutover plan
- Focus on Phase 7 failure modes

### Between Phases

After each phase, briefly summarize what was captured before moving on.
Example: "Got it — PostgreSQL on Supabase with Prisma, Redis caching for game state. Moving to Auth..."
