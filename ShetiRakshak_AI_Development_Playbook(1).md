# ShetiRakshak — AI Development Playbook

**Master Operating Manual for Antigravity**  
**Version:** 1.1  
**Status:** Human Approval Required Before Phase Execution  
**Product:** ShetiRakshak / शेतीरक्षक  
**Primary Market:** Maharashtra  
**Primary Language:** Marathi  
**Primary Crop:** Cotton  
**Core Product Idea:** The Watch — पहारा

> **Product philosophy:** समजतं. करता येतं. साथ आहे.  
> **Development philosophy:** Do one thing properly. Verify it. Document it. Then move to the next thing.

---

## 0. HOW ANTIGRAVITY MUST USE THIS PLAYBOOK

This document is an **operational engineering manual**, not a product implementation.

Antigravity MUST:

1. Read the source documents before beginning work.
2. Work on exactly one phase at a time.
3. Inspect the current repository before changing it.
4. Build only the scope of the current phase.
5. Verify implementation with evidence.
6. Update documentation and status.
7. Stop at a human approval gate when required.
8. Never silently change locked architecture, product behavior, or brand rules.

### Language of obligation

- **MUST / MUST NOT** — mandatory.
- **SHOULD / SHOULD NOT** — default unless a reason is recorded.
- **MAY** — optional and reversible.
- **LOCKED** — source-approved; do not change without human approval.
- **PLAYBOOK DEFAULT** — this document's default where source documents are silent.
- **PROPOSED CHANGE — REQUIRES HUMAN APPROVAL** — not approved until a human explicitly approves it.
- **UNVERIFIED — HUMAN REQUIRED** — cannot be honestly marked PASS by an AI agent alone.
- **BLOCKED** — work cannot safely continue without clarification, dependency, or approval.

---

# 1. EXECUTIVE OVERVIEW

ShetiRakshak is a Maharashtra-first, Marathi-first, voice-first, cotton-first agricultural decision-support application delivered as a PWA.

It is not merely:

- a weather app,
- a government portal,
- a chatbot,
- a crop-diagnosis engine,
- or a market-price screen.

Its role is to keep **पहारा — the Watch** over important farming decision moments.

The product should help a farmer answer:

1. **काय होतंय?** — What is happening?
2. **याचा अर्थ काय?** — What does it mean for my crop?
3. **आता काय करू?** — What should I do next?
4. **किती खात्री आहे?** — How confident is the system?
5. **माहिती कुठून आली?** — Where did it come from and how fresh is it?
6. **गरज पडली तर कोणाकडे जाऊ?** — Who can help if the system reaches its limit?

### Core promise

> **Understand. Know your next step. Know where to get help.**

### Product philosophy

Technology serves farmer judgment. It must never pretend to replace expert judgment.

Protection means:

> **Early awareness + clear next step + human backup**

It does **not** mean guaranteed prevention, diagnosis, profit, yield, treatment success, scheme approval, or market outcome.

---

# 2. SOURCE-OF-TRUTH HIERARCHY

When requirements conflict, Antigravity MUST follow this order:

| Priority | Source | Authority |
|---|---|---|
| 1 | Explicit human decision recorded in `docs/DECISION_LOG.md` | Highest |
| 2 | ShetiRakshak Brand Bible | Product, UX, language, visual identity, trust, accessibility, AI behavior |
| 3 | ShetiRakshak Technology Stack Specification | Technology and architecture |
| 4 | This AI Development Playbook | Sequencing, verification, execution rules |
| 5 | Current repository documentation | Implementation detail |
| 6 | Agent judgment | Only for small, reversible choices not covered above |

### Conflict rules

If Brand Bible and Technology Stack conflict:

**STOP. Do not choose one. Report the conflict.**

If the Playbook conflicts with a source document:

**Source document wins.**

If information is absent:

- Small and reversible → make a conservative decision and log it.
- Architectural, security, data, brand, or safety impact → STOP and request approval.

### Source-document preservation

At project initialization, copy the approved source documents into:

```text
docs/source/
├── BRAND_BIBLE.md
└── TECH_STACK.md
```

These files are reference snapshots and MUST NOT be silently edited.

The Brand Bible explicitly states that agronomy, scheme, market-price, and similar factual examples are illustrative. Never ship those examples as live facts without verification.

---

# 3. NON-NEGOTIABLE PRODUCT PRINCIPLES

## 3.1 The Watch — पहारा

The Watch is the permanent product concept.

It must appear through:

- the Watchline,
- the Rakhan visual language,
- decision-oriented information,
- visible uncertainty,
- a clear next step,
- and human escalation.

Do not turn the product into a generic dashboard.

## 3.2 Ten UX principles

1. One screen, one decision.
2. Next step before more detail.
3. Marathi first, English second.
4. Voice when typing is difficult.
5. Make uncertainty visible.
6. Name the source and date.
7. A human is always one tap away.
8. Work on weak networks and show last-known data.
9. Calm over clever.
10. Never promise what the system cannot control.

## 3.3 Home hierarchy

The home screen MUST preserve this order:

1. **Today's One Thing** — large hero/watch card.
2. **Persistent Voice button** — bottom-centre, “बोला”.
3. **Crop Watch strip** — only after crop is configured.
4. **Next 3 Days** — minimal Watchline.
5. **Relevant deadlines** — maximum 1–2.
6. **Get Help** — expert/Krushi Seva Kendra access.

Do not add feeds, long tables, directories, promotional cards, or unrelated features to the home screen.

## 3.4 Answer anatomy

Important answers should follow:

```text
What is happening?
        ↓
What does it mean?
        ↓
What should I do next?
        ↓
How confident are we?
        ↓
Where did the information come from?
        ↓
Can I reach a human?
```

## 3.5 Trust Strip

Important information MUST expose:

```text
Source
Freshness
Confidence
Human help
```

Example structure:

```text
स्रोत: <real source>
अद्ययावत: <timestamp>
विश्वास: <confidence>
[तज्ज्ञांकडून तपासा]
```

Never invent a source name.

## 3.6 Confidence

Use three practical states:

| Internal | Farmer-facing intent |
|---|---|
| High | `ही शक्यता जास्त आहे` |
| Medium | `ही एक शक्यता आहे` |
| Low | `खात्री नाही; तज्ज्ञांना विचारा` |

Confidence is not decoration. It changes behavior.

Low confidence MUST trigger appropriate escalation.

## 3.7 Human escalation

Escalate when:

- confidence is low,
- symptoms are severe or spreading,
- treatment dosage is requested,
- the farmer explicitly asks for a human,
- information is insufficient for a responsible answer.

The system should pass relevant context rather than forcing the farmer to repeat everything.

---

# 4. LOCKED TECHNOLOGY DIRECTION

The following stack is LOCKED unless a human approves a change.

| Layer | Technology |
|---|---|
| Frontend | React |
| Build tool | Vite |
| Styling | Tailwind CSS |
| Icons | Lucide React |
| Backend | Node.js + Express |
| Database | Supabase PostgreSQL |
| Authentication | Supabase Auth |
| File storage | Supabase Storage |
| Weather | WeatherAPI.com |
| AI | Gemini API |
| Speech input | Web Speech API |
| Speech output | Browser SpeechSynthesis |
| Location | Browser Geolocation API |
| Offline | PWA + IndexedDB |
| Frontend hosting | Vercel |
| Backend hosting | Render |
| Version control | Git + GitHub |
| Programming language | JavaScript |

### Explicit MVP non-goals

Do not introduce unless a future requirement explicitly proves the need:

- Microservices
- Kubernetes
- Kafka
- Redis
- Vector databases
- LangChain-style orchestration
- Python AI services
- Custom authentication
- Custom file storage
- Custom voice infrastructure
- Expert marketplace
- Event-driven distributed architecture
- Complex infrastructure-as-code

If one becomes necessary:

> **PROPOSED CHANGE — REQUIRES HUMAN APPROVAL**

---

# 5. TARGET ARCHITECTURE

Use one frontend, one backend, one database, and a small number of external providers.

```text
                         FARMER
                           |
                    React + Vite + PWA
                           |
                +----------+----------+
                |                     |
             Supabase             Express API
          Auth / Storage              |
             + RLS                    +------ WeatherAPI
                                      |
                                      +------ Gemini
                                      |
                                      +------ Supabase
```

## 5.1 Frontend boundary

Frontend is responsible for:

- rendering,
- interaction,
- local preferences,
- voice UI,
- PWA behavior,
- IndexedDB last-known data,
- Supabase Auth,
- user-owned Storage operations where RLS permits.

Frontend MUST NOT hold:

- Gemini secret keys,
- WeatherAPI secret keys,
- Supabase service-role keys,
- server-only credentials.

## 5.2 Backend boundary

Express owns:

- business rules,
- recommendation logic,
- confidence rules,
- escalation rules,
- external API calls,
- AI orchestration,
- server-side authorization,
- protected data operations,
- validation,
- rate limiting,
- source metadata normalization.

## 5.3 External API boundary

Only the backend calls:

- WeatherAPI
- Gemini

Never call them directly from browser code when secret credentials are required.

## 5.4 Deterministic Watch

The Watch engine MUST work with Gemini disabled.

Weather and Watch logic should follow:

```text
Provider data
  ↓
Normalize
  ↓
Pure application rules
  ↓
Marathi response template
  ↓
Trust metadata
  ↓
UI / Voice
```

AI may explain verified information, but the core Watch must not depend on generative output.

---

# 6. REPOSITORY STRUCTURE

Default structure:

```text
/
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── features/
│   │   ├── pages/
│   │   ├── services/
│   │   ├── hooks/
│   │   ├── lib/
│   │   ├── i18n/
│   │   ├── styles/
│   │   └── main.jsx
│   ├── public/
│   ├── tests/
│   ├── package.json
│   └── vite.config.js
│
├── backend/
│   ├── src/
│   │   ├── routes/
│   │   ├── controllers/
│   │   ├── services/
│   │   ├── rules/
│   │   ├── middleware/
│   │   ├── validators/
│   │   ├── lib/
│   │   └── server.js
│   ├── tests/
│   └── package.json
│
├── supabase/
│   ├── migrations/
│   ├── seed/
│   └── config.toml
│
├── docs/
│   ├── source/
│   │   ├── BRAND_BIBLE.md
│   │   └── TECH_STACK.md
│   ├── DEVELOPMENT_STATUS.md
│   ├── ARCHITECTURE.md
│   ├── DECISION_LOG.md
│   ├── API.md
│   ├── DATABASE.md
│   ├── TESTING.md
│   ├── SECURITY.md
│   ├── AI_GUIDELINES.md
│   ├── VOICE.md
│   ├── OFFLINE.md
│   └── RELEASE.md
│
├── .env.example
├── .gitignore
├── .nvmrc
└── README.md
```

Do not create folders merely to satisfy this diagram. Keep the actual repository simple.

---

# 7. CODING RULES

## 7.1 Prefer

- Small components
- Small functions
- Clear names
- Feature-oriented modules
- Pure business rules
- Reusable utilities
- Explicit data shapes
- Early validation
- Simple control flow
- Consistent formatting

## 7.2 Avoid

- Giant components
- Giant files
- duplicated business logic
- deep abstraction layers
- clever one-liners
- premature optimization
- speculative architecture
- dead code
- unused imports
- unexplained hacks
- hidden side effects

## 7.3 JavaScript

JavaScript is the locked project language.

Use modern JavaScript and ES modules.

Do not migrate to TypeScript without:

> **PROPOSED CHANGE — REQUIRES HUMAN APPROVAL**

## 7.4 Component rule

A component should have one clear responsibility.

If a component starts owning:

- API calls,
- business rules,
- formatting,
- complex state,
- accessibility logic,
- and large rendering branches,

split responsibilities.

## 7.5 Dependency gate

Before adding a package, answer:

1. Do we actually need it?
2. Can the existing stack solve this?
3. Is it maintained?
4. Does it increase complexity?
5. Does it create security/privacy/performance risk?

If uncertain, do not add it.

Every new dependency must be recorded in `DECISION_LOG.md`.

## 7.6 No-overengineering rule

Do not build future architecture before future requirements exist.

The correct question is:

> “What is the smallest reliable solution for the current requirement?”

---

# 8. AI DEVELOPMENT RULES

These rules apply to Antigravity itself while coding.

## 8.1 Inspect before editing

Before changing a file:

1. Read the relevant code.
2. Understand its callers.
3. Check tests.
4. Check documentation.
5. Identify whether the behavior is relied upon elsewhere.

Do not rewrite working code merely because another implementation looks cleaner.

## 8.2 Minimal-change principle

Prefer the smallest safe change that satisfies the current phase.

Avoid unrelated refactors.

## 8.3 No speculative implementation

Do not implement:

- future crop types,
- future languages,
- future marketplaces,
- future expert networks,
- future analytics,
- future AI agents,

unless the current phase explicitly requires them.

## 8.4 Evidence, not assertion

Never report:

> “It should work.”

Report:

> “Build passed with command X. Test suite passed with Y tests. Manual verification covered Z.”

---

# 9. PRODUCT AI SAFETY ARCHITECTURE

Gemini is an assistant, not the source of truth.

Use:

```text
Verified context
      ↓
Application rules
      ↓
Gemini
      ↓
Structured output
      ↓
Schema validation
      ↓
Safety guards
      ↓
Confidence / escalation rules
      ↓
Trust Strip
      ↓
Farmer
```

## 9.1 AI must not

- invent sources,
- invent prices,
- invent schemes,
- invent weather,
- invent diagnoses,
- invent treatment doses,
- guarantee outcomes,
- hide uncertainty,
- fabricate expert approval,
- present generated content as official information.

## 9.2 Structured AI response

A practical response envelope may include:

```json
{
  "message": "...",
  "nextStep": "...",
  "confidence": "high|medium|low",
  "source": "...",
  "sourceUrl": "...",
  "needsExpert": true
}
```

The exact schema may evolve, but AI output MUST be schema-validated before reaching critical UI.

## 9.3 Confidence rule

Application logic owns final confidence.

Model-reported confidence can only lower the final confidence; it cannot override safety rules.

Photo-based analysis is capped at **Medium** until an explicitly approved human-reviewed policy changes that rule.

## 9.4 Treatment rule

Treatment advice remains at category level unless qualified, verified expert-reviewed content explicitly permits more detail.

Never generate or invent dosage instructions.

---

# 10. DATA, SOURCE, AND CONTENT GOVERNANCE

Important external information should carry provenance:

```text
source
source_url
retrieved_at
published_at (when available)
updated_at (when available)
confidence
kind = official | general
```

## 10.1 Official information

Official information must:

- identify the real issuing source,
- preserve the original URL where possible,
- show freshness,
- distinguish official information from general information.

## 10.2 Market information

Market information must include:

- market/location,
- source,
- date/time,
- price context,
- freshness.

Do not imply a displayed price is guaranteed to be the farmer's realized selling price.

## 10.3 Schemes

A scheme record should preserve:

- scheme name,
- official source,
- official URL,
- eligibility,
- deadline where applicable,
- required documents,
- last verified date.

If a government source cannot be verified, do not present the record as official.

## 10.4 Marathi governance

Marathi is the product language, not a post-processing translation.

Rules:

- Brand Bible strings are authoritative.
- New farmer-facing Marathi copy is a draft until native-speaker review.
- Do not machine-translate critical agriculture content and treat it as approved.
- Use plain, spoken, respectful Marathi.
- Prefer action verbs.
- Avoid bureaucratic or overly Sanskritized language.
- Preserve Marathi rendering on low-end devices.

---

# 11. ERROR AND STATE MODEL

Every important feature MUST explicitly support:

```text
Loading
Success
Empty
Error
Offline
Permission denied
Timeout
API unavailable
Invalid input
Unknown state
```

No feature is complete if only the happy path exists.

Example approved error style:

> `काहीतरी चुकलं. पुन्हा प्रयत्न करा.`

Example offline style:

> `इंटरनेट नाही. शेवटची माहिती दाखवत आहोत.`

Never silently display stale information as current.

---

# 12. EXTERNAL API FAILURE STRATEGY

All external requests should have:

- timeout,
- normalized errors,
- retry behavior where appropriate,
- last-known fallback where safe,
- freshness metadata.

Use:

```text
Request
  ↓
Success?
 ├── YES → normalize → use
 └── NO
      ↓
Valid last-known data?
 ├── YES → show stale + timestamp + retry
 └── NO → explain failure + retry + human help if relevant
```

Do not repeatedly retry aggressively on weak networks.

---

# 13. SECURITY RULES

## 13.1 Secrets

Never commit:

- API keys,
- service-role keys,
- passwords,
- tokens,
- private credentials.

Use environment variables.

## 13.2 Browser bundle

Never expose server-only secrets in frontend JavaScript.

## 13.3 Authentication

Use Supabase Auth.

Do not create a custom authentication system.

Anonymous/local usage may exist where explicitly designed, but account creation should be required only when persistence or protected workflows need it.

## 13.4 Authorization

Never trust a client-provided role.

Server-side authorization is required for protected operations.

Expert role should be server-controlled.

## 13.5 Database

Every user-owned table must have appropriate Row Level Security.

Policy intent must be documented.

Never assume frontend filtering is security.

## 13.6 Storage

Validate:

- file type,
- file size,
- upload authorization,
- ownership,
- access policy.

Photo uploads are user data and must not become publicly accessible by default.

## 13.7 Location privacy

Use only the precision required for the feature.

Default project rule:

> Round coordinates to approximately 2 decimal places before storage/provider calls unless a feature demonstrates a real need for greater precision.

## 13.8 Logging

Never log:

- passwords,
- auth tokens,
- secret keys,
- unnecessary personal data,
- full sensitive photos.

Logs should be useful without becoming a second personal-data store.

---

# 14. ACCESSIBILITY AND FARMER USABILITY

Brand requirements are implementation requirements.

Target:

- touch targets ≥ 56dp where practical, never below 48dp,
- body text ≥ 18px for core farmer-facing content,
- text contrast ≥ 4.5:1,
- UI contrast ≥ 3:1,
- icon + text + color for status,
- voice access to core tasks,
- audio replies repeat the next step,
- maximum three taps to a core task,
- clear error recovery,
- responsive layouts,
- low-bandwidth behavior,
- Marathi rendering,
- keyboard basics,
- screen-reader basics.

Do not use color alone to communicate status.

---

# 15. DESIGN SYSTEM RULES

Implement the Brand Bible tokens before building feature-specific styling.

The visual system must preserve:

- Ink + Haldi palette,
- Kapus/background language,
- calm visual rhythm,
- Watchline,
- signal arches,
- Rakhan visual language,
- rounded, approachable controls,
- spacious hierarchy.

## Core components

Build reusable primitives for:

- Primary button
- Secondary button
- Voice button
- Hero card
- Standard card
- Quiet help card
- Alert
- Status badge
- Trust Strip
- Watchline
- Loading state
- Error state
- Empty state
- Offline state

Critical actions must use icon + label, not icon-only controls.

Motion should be gentle and respect reduced-motion preferences.

---

# 16. TESTING STRATEGY

Testing must remain practical.

## 16.1 Unit tests

Use for:

- utility functions,
- weather normalization,
- Watch rules,
- confidence logic,
- escalation rules,
- source/freshness formatting,
- data transformations.

## 16.2 Integration tests

Use for:

- Express routes,
- authentication boundaries,
- Supabase interactions,
- WeatherAPI service,
- AI service,
- upload validation,
- escalation flow.

## 16.3 UI tests

Test:

- navigation,
- core forms,
- home hierarchy,
- voice states,
- loading/error/empty states,
- weather display,
- crop flow,
- expert request.

## 16.4 Manual tests

Required for:

- real Marathi rendering,
- real speech recognition,
- SpeechSynthesis,
- mobile browser behavior,
- low-end device behavior,
- weak network,
- real provider responses,
- permissions,
- camera/photo behavior,
- accessibility.

A test that was not actually run MUST NOT be reported as PASS.

---

# 17. TEST-FIRST FOR IMPORTANT LOGIC

For important business logic:

```text
Define expected behavior
        ↓
Write test
        ↓
Implement
        ↓
Run test
        ↓
Run edge cases
        ↓
Document
```

Prioritize:

- weather decision rules,
- confidence rules,
- escalation rules,
- authorization rules,
- data freshness,
- upload validation.

---

# 18. GIT STRATEGY

Use simple, traceable Git.

Recommended phase branches:

```text
phase/00-foundation
phase/01-design-system
phase/02-app-shell
...
```

For completed phases:

```text
Implement
  ↓
Test
  ↓
Review
  ↓
Commit
  ↓
Tag
```

Meaningful commit examples:

```text
feat: add application shell
feat: add weather service
feat: add cotton crop profile
feat: add voice interaction
fix: handle weather API timeout
test: add watch confidence rules
docs: update architecture
```

Do not create giant commits containing unrelated work.

---

# 19. DOCUMENTATION STRATEGY

Maintain only useful documentation.

Required:

```text
docs/
├── DEVELOPMENT_STATUS.md
├── ARCHITECTURE.md
├── DECISION_LOG.md
├── API.md
├── DATABASE.md
├── TESTING.md
├── SECURITY.md
├── AI_GUIDELINES.md
├── VOICE.md
├── OFFLINE.md
└── RELEASE.md
```

Update documentation in the same phase that changes the corresponding behavior.

Documentation must describe the implementation that actually exists.

---

# 20. DEVELOPMENT STATUS

`docs/DEVELOPMENT_STATUS.md` is the single progress tracker.

Use:

```text
NOT_STARTED
IN_PROGRESS
BLOCKED
READY_FOR_REVIEW
VERIFIED
COMPLETED
```

Track:

```text
Phase:
Status:
Completed tasks:
Tests:
Known issues:
Blockers:
Next action:
Last verified:
```

Never mark a phase COMPLETED merely because its files exist.

---

# 21. DECISION LOG

`docs/DECISION_LOG.md` records important decisions.

Each decision:

```text
ID:
Date:
Decision:
Reason:
Alternatives considered:
Impact:
Status:
Approval:
```

Record:

- architecture decisions,
- dependency additions,
- provider choices,
- schema decisions,
- security exceptions,
- source verification decisions,
- changes to locked behavior.

If an old decision is superseded, preserve the old record and add a new decision.

---

# 22. UNIVERSAL DEFINITION OF DONE

A task is done only when all applicable items are true:

- [ ] Implementation exists.
- [ ] Build succeeds.
- [ ] Relevant tests pass.
- [ ] No relevant console errors remain.
- [ ] Loading state exists.
- [ ] Error state exists.
- [ ] Empty state exists where applicable.
- [ ] Offline/permission state exists where applicable.
- [ ] Mobile behavior checked.
- [ ] Accessibility checked.
- [ ] Marathi checked.
- [ ] Brand compliance checked.
- [ ] Security implications checked.
- [ ] Documentation updated.
- [ ] Acceptance criteria satisfied.
- [ ] Git change is understandable.
- [ ] No unrelated feature was introduced.

---

# 23. STANDARD PHASE FORMAT

Every phase MUST use this structure in the agent's execution notes:

```text
PHASE X — NAME

Objective:
Why this phase exists:

Prerequisites:
Dependencies:

Scope:
Out of scope:

Files/modules affected:

Tasks:
1.
2.
3.

Technical constraints:

Brand requirements:

Security requirements:

Tests:

Manual verification:

Expected result:

Acceptance criteria:

Definition of Done:

Failure conditions:

Rollback/recovery:

Completion report:
```

---

# 24. COMPLETE DEVELOPMENT ROADMAP

The final build order is:

```text
Phase 0  Foundation & Rules
   ↓
Phase 1  Design System
   ↓
Phase 2  Application Shell
   ↓
Phase 3  Supabase Foundation
   ↓
Phase 4  Farmer & Farm Profile
   ↓
Phase 5  Weather
   ↓
Phase 6  Today's One Thing / Watchline
   ↓
Phase 7  Voice
   ↓
Phase 8  Bounded AI Assistance
   ↓
Phase 9  Crop Problem / Photo Flow
   ↓
Phase 10 Expert Help
   ↓
Phase 11 Schemes
   ↓
Phase 12 Market Information
   ↓
Phase 13 Offline / Weak Network
   ↓
Phase 14 Accessibility & Farmer Usability
   ↓
Phase 15 Security & Privacy Audit
   ↓
Phase 16 Full Integration
   ↓
Phase 17 QA / Release Candidate
   ↓
Phase 18 Production Deployment
   ↓
Phase 19 Final Product Audit
```

Do not build ahead.

---

# 25. PHASE 0 — PROJECT INITIALIZATION & RULES

## Objective

Create a clean, reproducible project foundation.

## Tasks

1. Initialize Git repository if required.
2. Create `frontend/` and `backend/`.
3. Initialize React/Vite frontend.
4. Initialize Node/Express backend.
5. Configure JavaScript ES modules.
6. Establish Node LTS version.
7. Create `.env.example`.
8. Create `.gitignore`.
9. Add source documents to `docs/source/`.
10. Create documentation skeleton.
11. Create status and decision logs.
12. Add baseline scripts for development, test, lint, and build where approved.
13. Confirm frontend and backend can start independently.

## Constraints

Do not build business features.

## Verification

- frontend starts,
- backend starts,
- build succeeds,
- Git status is clean after commit,
- secrets are ignored.

## Acceptance criteria

A new developer can clone the repository, configure environment variables, start both services, and understand the repository structure.

## Gate

**Gate 1 — Architecture Approval**

Human confirms:

- stack,
- repository layout,
- frontend/backend boundary,
- environment strategy,
- dependency baseline,
- development workflow.

---

# 26. PHASE 1 — DESIGN SYSTEM FOUNDATION

## Objective

Translate Brand Bible tokens into reusable UI primitives.

## Tasks

Implement:

- color tokens,
- typography,
- spacing,
- radius,
- buttons,
- cards,
- alerts,
- status badges,
- Trust Strip,
- Watchline,
- Voice button,
- loading/error/empty primitives.

## Constraints

Do not build real business flows.

Use approved Brand Bible language.

## Verification

Check:

- Marathi rendering,
- contrast,
- touch size,
- responsive behavior,
- reduced motion.

## Acceptance criteria

A feature developer can build future screens from the shared primitives without duplicating brand styling.

## Gate

**Gate 2 — Design System Approval**

Review:

- visual fidelity,
- Marathi typography,
- component consistency,
- accessibility basics.

---

# 27. PHASE 2 — APPLICATION SHELL

## Objective

Create the navigation and responsive application frame.

## Tasks

Implement:

- routing,
- app layout,
- responsive navigation,
- home placeholder,
- page loading,
- page error,
- empty states,
- basic PWA-ready metadata.

Do not implement external API business logic.

## Acceptance criteria

All planned MVP routes can render through the shell and remain usable on mobile and desktop.

---

# 28. PHASE 3 — SUPABASE FOUNDATION

## Objective

Establish database, auth, storage, and security foundations.

## Tasks

1. Create development Supabase project.
2. Create migrations.
3. Create only required MVP tables.
4. Enable RLS on user-owned tables.
5. Create storage buckets/policies where required.
6. Configure Supabase Auth.
7. Establish server-side authorization.
8. Document schema and policies.
9. Separate development and production credentials.

## Initial data domains

Likely domains:

```text
farmer/profile
farm
crop
crop_stage
expert_case
expert_response
scheme
market_record
weather_cache
```

Do not create tables without a current requirement.

## Gate

**Gate 3 — Database Approval**

Must verify:

- schema,
- migrations,
- RLS,
- storage policies,
- auth,
- authorization.

---

# 29. PHASE 4 — FARMER & FARM PROFILE

## Objective

Capture the minimum context required for useful decisions.

## Scope

- farmer identity,
- farm location,
- crop,
- crop stage,
- simple profile preferences.

## Rules

- Do not ask for unnecessary information.
- Do not force account creation before it is useful.
- Respect location consent.
- Store only required precision.

## Acceptance criteria

A farmer can create/update a cotton farm profile and the system can safely use that context in later phases.

---

# 30. PHASE 5 — WEATHER SYSTEM

## Objective

Create a reliable weather data service.

## Tasks

- geolocation permission flow,
- manual location fallback,
- WeatherAPI integration,
- current weather,
- forecast,
- normalization,
- timeout handling,
- source metadata,
- freshness metadata,
- last-known abstraction.

## Envelope

Every weather result should follow the shared data envelope:

```js
{
  status: "fresh|stale|expired|error",
  data: {},
  meta: {
    source,
    sourceUrl,
    kind,
    retrievedAt,
    publishedAt,
    updatedAt,
    confidence
  },
  error: {
    code,
    retryable
  }
}
```

## Critical rule

Do not show WeatherAPI data as if it came from another organization.

## Gate

**Gate 5 — Weather Verification**

Verify:

- current weather,
- forecast,
- timeout,
- provider failure,
- stale data,
- location denied,
- manual location,
- source/freshness labels.

---

# 31. PHASE 6 — TODAY'S ONE THING / WATCHLINE

## Objective

Build the core ShetiRakshak decision experience.

## Architecture

```text
Weather + crop stage + verified context
        ↓
Deterministic rules
        ↓
Today's One Thing
        ↓
Meaning
        ↓
One next step
        ↓
Trust Strip
```

## Rules

- no Gemini dependency,
- no unsupported agronomy claims,
- no alarmist wording,
- one primary action,
- uncertainty visible.

## Acceptance criteria

The farmer can understand:

> What is happening → what it means → what to do next.

The Watch continues to function if Gemini is unavailable.

---

# 32. PHASE 7 — VOICE INTERACTION

## Objective

Add voice as a first-class interaction.

## Tasks

- persistent voice button,
- microphone permission,
- listening state,
- recognition result,
- stop/cancel,
- speech output,
- speaking state,
- Marathi language selection,
- unsupported-browser fallback,
- permission-denied fallback,
- network failure handling.

## Rules

Voice output MUST repeat the next step when delivering important advice.

If Marathi speech recognition or speech output is unavailable, provide a clear text fallback.

## Gate

**Voice verification**

Human testing is required for real Marathi speech quality and browser/device coverage.

---

# 33. PHASE 8 — BOUNDED AI ASSISTANCE

## Objective

Introduce Gemini without giving it uncontrolled authority.

## AI responsibilities

Gemini may:

- explain verified information,
- simplify language,
- answer contextual questions,
- summarize known information,
- help interpret a user-provided crop problem.

Gemini may not:

- invent facts,
- invent sources,
- invent official status,
- override deterministic safety rules,
- claim certainty beyond evidence.

## Implementation

```text
Verified context
 ↓
Rules
 ↓
Gemini structured response
 ↓
Schema validation
 ↓
Safety guard
 ↓
Confidence adjustment
 ↓
Escalation
```

## Gate

**Gate 6 — AI Approval**

Verify:

- structured output,
- invalid-output handling,
- prompt injection resistance,
- hallucination guards,
- confidence rules,
- source preservation,
- escalation behavior,
- API failure behavior.

---

# 34. PHASE 9 — CROP PROBLEM / PHOTO FLOW

## Objective

Allow a farmer to submit a crop problem with photo and context.

## Tasks

- camera/photo selection,
- client-side validation,
- upload constraints,
- Supabase Storage,
- crop/stage context,
- AI-assisted analysis,
- confidence,
- expert escalation.

## Rules

Never label a generated image analysis as a confirmed diagnosis.

Photo analysis is capped at Medium confidence unless an approved human-reviewed policy changes this.

Low confidence or severe/spreading symptoms MUST escalate.

---

# 35. PHASE 10 — EXPERT HELP

## Objective

Make human escalation real and useful.

## Farmer flow

```text
Problem
 ↓
AI/Rule detects uncertainty or farmer asks
 ↓
Create case
 ↓
Attach photo + context
 ↓
Expert review
 ↓
Response
 ↓
Farmer notified / sees response
```

## Case data

Keep it minimal but useful:

- farmer reference,
- crop,
- crop stage,
- description,
- photo references,
- location context where consented,
- created time,
- status,
- expert response.

## Security

Farmers may see only their own cases.

Experts may access only cases they are authorized to handle.

---

# 36. PHASE 11 — SCHEMES

## Objective

Present verified agricultural schemes as actions, not bureaucratic documents.

## Required provenance

Each live record:

```text
name
officialSource
officialUrl
eligibility
deadline
documents
verifiedAt
status
```

## Rules

- official badge only when verified,
- source link required,
- stale records must be flagged or retired,
- no invented eligibility,
- no invented deadline.

---

# 37. PHASE 12 — MARKET INFORMATION

## Objective

Provide transparent market information without implying guaranteed selling outcomes.

## Required provenance

```text
market
location
price
unit
source
timestamp/date
freshness
```

## UX

Use:

> “आजचा भाव (स्रोत, तारीख). खरेदी केंद्रात विचारून निर्णय घ्या.”

where appropriate.

Never present a displayed price as a guaranteed realization.

---

# 38. PHASE 13 — OFFLINE / WEAK NETWORK

## Objective

Make the product useful when connectivity is poor.

## Tasks

- PWA manifest,
- service worker,
- IndexedDB,
- last-known store,
- cache policy,
- offline state,
- timestamp display,
- retry flow.

## Architecture

Use one abstraction:

```text
UI/service
   ↓
lastKnownStore
   ↓
current implementation: local storage where appropriate
   ↓
Phase 13: IndexedDB
```

Callers should not need to change when storage moves to IndexedDB.

## Rules

Never imply cached data is live.

---

# 39. PHASE 14 — ACCESSIBILITY & FARMER USABILITY

## Objective

Audit real-world usability.

## Verify

- touch targets,
- typography,
- contrast,
- Marathi glyph rendering,
- voice,
- screen reader basics,
- keyboard navigation,
- responsive layouts,
- low-end devices,
- reduced motion,
- three-tap core task rule,
- error recovery.

## Human review required

Native Marathi speaker and real-user/farmer testing should be recorded as:

`UNVERIFIED — HUMAN REQUIRED`

until completed.

---

# 40. PHASE 15 — SECURITY & PRIVACY AUDIT

## Objective

Perform a full security pass before integration freeze.

## Audit

### Secrets
- no keys in repository,
- no secret keys in bundle.

### Auth
- correct sessions,
- correct redirects,
- protected routes.

### Authorization
- server checks,
- role checks,
- ownership checks.

### Database
- RLS,
- no accidental public reads/writes.

### Storage
- file validation,
- ownership,
- access policies.

### AI
- prompt/data handling,
- output validation,
- rate limits,
- abuse controls.

### Privacy
- location consent,
- photo consent,
- data deletion,
- minimal collection.

---

# 41. PHASE 16 — FULL INTEGRATION

## Objective

Connect the core experience.

Verify:

```text
Home
 ↓
Weather
 ↓
Crop context
 ↓
Watch
 ↓
Voice
 ↓
AI explanation
 ↓
Photo problem
 ↓
Expert escalation
```

Also verify:

```text
Schemes
Market
Offline
Trust Strip
```

No module is considered integrated merely because navigation exists.

Data must flow correctly across boundaries.

---

# 42. PHASE 17 — QA / RELEASE CANDIDATE

Run:

- unit tests,
- integration tests,
- UI tests,
- API tests,
- accessibility checks,
- security review,
- responsive checks,
- mobile checks,
- weak-network tests,
- offline tests,
- provider failure tests,
- permission tests,
- Marathi review,
- AI safety tests.

## Release candidate rule

Any critical failure blocks release.

No known critical security, data-loss, or unsafe-AI issue may be waived silently.

---

# 43. PHASE 18 — PRODUCTION DEPLOYMENT

Target:

```text
Frontend → Vercel
Backend → Render
Database → Supabase
```

## Deployment checklist

- production environment variables,
- production Supabase project,
- production auth redirects,
- production storage policies,
- CORS configuration,
- HTTPS,
- provider keys,
- rate limits,
- health endpoint,
- error logging,
- build verification,
- rollback plan.

Development and production environments MUST remain separated.

---

# 44. PHASE 19 — FINAL PRODUCT AUDIT

Compare the implementation against the Brand Bible line-by-line.

## Product

- [ ] Farmer understands what is happening.
- [ ] Farmer understands the next step.
- [ ] Human help is accessible.

## Brand

- [ ] Watch / पहारा is clear.
- [ ] Rakhan visual language is present.
- [ ] Ink + Haldi system is consistent.
- [ ] Calm visual tone is preserved.
- [ ] Marathi-first communication is preserved.

## UX

- [ ] One decision per screen.
- [ ] Next step before detail.
- [ ] Voice is accessible.
- [ ] Home remains uncluttered.

## Trust

- [ ] Source.
- [ ] Freshness.
- [ ] Confidence.
- [ ] Human escalation.

## AI

- [ ] No guarantees.
- [ ] No invented facts.
- [ ] No invented sources.
- [ ] Confidence preserved.
- [ ] Low-confidence escalation works.

## Reliability

- [ ] Loading.
- [ ] Error.
- [ ] Empty.
- [ ] Offline.
- [ ] Permission denial.
- [ ] API failure.

## Security

- [ ] Secrets protected.
- [ ] Auth correct.
- [ ] Authorization correct.
- [ ] RLS verified.
- [ ] Storage policies verified.
- [ ] Privacy behavior verified.

## Performance

- [ ] Mobile performance acceptable.
- [ ] Low-end behavior checked.
- [ ] Images optimized.
- [ ] Network usage reasonable.

---

# 45. VERIFICATION GATES

## Gate 1 — Architecture

Must verify:

- locked stack,
- repository structure,
- frontend/backend boundaries,
- environment strategy,
- dependency policy,
- Git workflow.

## Gate 2 — Design System

Must verify:

- tokens,
- typography,
- components,
- Marathi,
- accessibility basics.

## Gate 3 — Database

Must verify:

- schema,
- migrations,
- RLS,
- storage,
- authentication,
- authorization.

## Gate 4 — Farmer Context

Must verify:

- profile,
- farm,
- crop,
- stage,
- location/privacy.

## Gate 5 — Weather / Watch

Must verify:

- provider integration,
- source/freshness,
- deterministic Watch,
- failure states.

## Gate 6 — AI

Must verify:

- structured output,
- validation,
- safety guards,
- confidence,
- escalation.

## Gate 7 — Expert Escalation

Must verify:

- case creation,
- ownership,
- photo/context transfer,
- expert access,
- response flow.

## Gate 8 — Offline

Must verify:

- PWA,
- IndexedDB,
- last-known data,
- freshness labeling,
- offline UX.

## Gate 9 — Security

Must verify:

- secrets,
- RLS,
- storage,
- authorization,
- privacy,
- AI abuse boundaries.

## Gate 10 — Production

Must verify:

- deployment,
- production configuration,
- monitoring,
- rollback,
- release checklist.

---

# 46. ZERO-SKIP DEVELOPMENT RULE

Antigravity MUST NOT:

- skip a phase because it looks easy,
- assume functionality works,
- mark untested work complete,
- build future functionality prematurely,
- add unjustified dependencies,
- replace architecture silently,
- rewrite working code unnecessarily,
- ignore failing tests,
- ignore console errors,
- ignore accessibility,
- ignore responsive behavior,
- ignore Marathi rendering,
- ignore weak-network behavior,
- ignore API failures,
- ignore security warnings.

If a phase cannot be completed correctly, STOP.

Use:

```text
BLOCKED

Phase:
Problem:
What was attempted:
Evidence:
Likely cause:
What is needed:
Impact:
Recommended next action:
```

---

# 47. STOP CONDITIONS

STOP instead of guessing when:

- requirements conflict,
- a source is missing,
- an API contract is unclear,
- a security issue appears,
- a migration may cause data loss,
- a major architecture change is needed,
- a Brand Bible rule would be violated,
- AI could produce unsafe certainty,
- a critical test fails,
- production data could be affected.

---

# 48. CHANGE MANAGEMENT

If Antigravity discovers that an existing architectural decision is wrong:

```text
STOP
 ↓
Document problem
 ↓
Measure impact
 ↓
Describe alternatives
 ↓
Recommend a technically justified option
 ↓
Request human approval
 ↓
Record decision
 ↓
Only then change architecture
```

Never silently rewrite the project.

---

# 49. ROLLBACK / RECOVERY

## Code failure

1. Identify last known-good commit.
2. Reproduce failure.
3. Revert or fix in the phase branch.
4. Re-run tests.
5. Do not continue to the next phase.

## Database migration risk

If migration could cause data loss:

**STOP.**

Do not execute destructive migration against production without explicit approval and backup/recovery confirmation.

## Deployment failure

Use the previous known-good deployment/version.

Document:

- failure,
- rollback,
- root cause,
- fix,
- verification.

## Provider failure

Use the external API fallback strategy.

Never fabricate provider data.

---

# 50. PHASE COMPLETION REPORT

Every phase ends with:

```text
PHASE COMPLETION REPORT

Phase:
Status:

Implemented:
- ...

Files changed:
- ...

Tests:
- ...

Build:
PASS / FAIL

Manual verification:
PASS / FAIL / UNVERIFIED — HUMAN REQUIRED

Brand compliance:
PASS / FAIL

Security review:
PASS / FAIL

Known issues:
- ...

Technical debt:
- ...

Documentation updated:
- ...

Ready for next phase:
YES / NO

Evidence:
- command/output/reference

Notes:
...
```

---

# 51. ANTIGRAVITY START-OF-PHASE PROTOCOL

At the beginning of every phase:

```text
1. Read Brand Bible.
2. Read Technology Stack.
3. Read DEVELOPMENT_STATUS.md.
4. Read ARCHITECTURE.md.
5. Read DECISION_LOG.md.
6. Inspect relevant existing code.
7. Confirm phase number.
8. Confirm prerequisites.
9. Confirm allowed dependencies.
10. Define current-phase scope.
11. Implement only that scope.
```

If prerequisites are not satisfied:

**STOP.**

---

# 52. ANTIGRAVITY END-OF-PHASE PROTOCOL

Before reporting completion:

```text
1. Run tests.
2. Run production build.
3. Check console/runtime errors.
4. Inspect changed files.
5. Verify acceptance criteria.
6. Check responsive behavior.
7. Check relevant accessibility.
8. Check Marathi strings.
9. Check security implications.
10. Update documentation.
11. Update DEVELOPMENT_STATUS.md.
12. Update DECISION_LOG.md if required.
13. Produce Phase Completion Report.
14. Stop at the gate if approval is required.
```

---

# 53. PROGRESS TRACKING RULES

A phase may only become:

`COMPLETED`

after:

- implementation,
- verification,
- documentation,
- completion report,
- required human approval.

If implementation is complete but a human test is pending:

`READY_FOR_REVIEW`

If a blocker exists:

`BLOCKED`

If work is underway:

`IN_PROGRESS`

---

# 54. RISK REGISTER

Maintain and update risks including:

| Risk | Mitigation |
|---|---|
| Hallucinated agricultural advice | Verified context + structured AI + confidence + escalation |
| Stale information | Provenance + freshness + stale labels |
| Weak network | PWA + IndexedDB + last-known data |
| Marathi quality | Native review + farmer testing |
| Voice browser differences | Capability detection + text fallback |
| API outage | timeout + fallback + retry |
| Exposed secrets | backend-only provider calls |
| Data leakage | RLS + server authorization |
| Unsafe uploads | type/size/ownership validation |
| Scope creep | phase scope + no-overengineering rule |
| Brand drift | design tokens + final audit |
| Architecture drift | decision log + approval gates |
| Database damage | migrations + backups + approval |
| Low-end device performance | lightweight UI + manual device testing |

---

# 55. DEFERRED / OUT-OF-SCOPE UNTIL APPROVED

Unless a future requirement explicitly activates them, do not build:

- microservices,
- Kubernetes,
- Kafka,
- Redis,
- vector database,
- autonomous multi-agent system,
- custom voice server,
- expert marketplace,
- advanced analytics platform,
- complex recommendation engine,
- national multi-language architecture,
- large notification infrastructure,
- speculative integrations.

Future scalability should come from clean boundaries and good data models, not premature infrastructure.

---

# 56. PRODUCTION RELEASE CHECKLIST

## Product

- [ ] Core flows work.
- [ ] Farmer gets a clear next step.
- [ ] Farmer can reach human help.

## Brand

- [ ] Watch concept.
- [ ] Rakhan mark/language.
- [ ] Brand tokens.
- [ ] Calm visual style.
- [ ] Marathi-first copy.

## UX

- [ ] Home hierarchy preserved.
- [ ] Voice available.
- [ ] No unnecessary clutter.
- [ ] Core tasks within reasonable interaction depth.

## AI

- [ ] Structured output.
- [ ] Confidence.
- [ ] Sources preserved.
- [ ] No guarantees.
- [ ] No invented facts.
- [ ] Human escalation.

## Accessibility

- [ ] Touch targets.
- [ ] Typography.
- [ ] Contrast.
- [ ] Voice.
- [ ] Keyboard.
- [ ] Screen reader basics.
- [ ] Responsive behavior.

## Reliability

- [ ] Loading.
- [ ] Error.
- [ ] Empty.
- [ ] Offline.
- [ ] Timeout.
- [ ] Provider failure.
- [ ] Permission denied.

## Security

- [ ] No secrets committed.
- [ ] Auth verified.
- [ ] Authorization verified.
- [ ] RLS verified.
- [ ] Storage policies verified.
- [ ] Privacy behavior verified.
- [ ] Upload validation verified.

## Performance

- [ ] Mobile tested.
- [ ] Low-end tested.
- [ ] Images optimized.
- [ ] Network use reviewed.

## Operations

- [ ] Production environment separated.
- [ ] Health checks.
- [ ] Rollback path.
- [ ] Release notes.
- [ ] Documentation current.

---

# 57. FINAL OPERATING RULE

The most important instruction in this entire document is:

> **Do one thing properly. Verify it. Document it. Then move to the next thing.**

And the product must continuously preserve:

> **समजतं. करता येतं. साथ आहे.**

If a proposed implementation makes the system more technically impressive but makes the farmer experience less clear, less trustworthy, less accessible, or harder to maintain, do not adopt it without evidence and approval.

The goal is not maximum technology.

The goal is a dependable agricultural decision-support product that helps a farmer understand the situation, take the next step, and reach a human when needed.

---

# APPENDIX A — SOURCE-DOCUMENT NON-NEGOTIABLES

The Brand Bible requires, among other things:

- Maharashtra-first
- Marathi-first
- cotton-first
- voice-first
- The Watch / पहारा
- Watchline
- Rakhan visual language
- Trust Strip
- source/date/confidence/human help
- one decision per screen
- next step before detail
- weak-network support
- calm UX
- no guarantees
- no fabricated facts
- human escalation
- accessibility
- privacy clarity
- official-source labeling
- native Marathi review
- agronomy review
- government-source verification
- expert verification
- AI messaging review

These are product requirements, not optional branding suggestions.

---

# APPENDIX B — MINIMUM DATA MODEL OUTLINE

This is a planning outline, not permission to create every table immediately.

Potential entities:

```text
auth.users
farms
crops
crop_stages
farmer_preferences
weather_cache
expert_cases
expert_responses
schemes
market_records
```

Every entity must earn its existence through a current requirement.

Use foreign keys, constraints, indexes, and RLS deliberately.

Avoid a generic “everything table”.

---

# APPENDIX C — ENVIRONMENT VARIABLE POLICY

Maintain `.env.example` without real values.

Likely server-only variables:

```text
WEATHER_API_KEY=
GEMINI_API_KEY=
SUPABASE_SERVICE_ROLE_KEY=
```

Likely public/browser-safe variables:

```text
VITE_SUPABASE_URL=
VITE_SUPABASE_ANON_KEY=
VITE_API_BASE_URL=
```

Exact variable names may be changed during implementation, but secret/public classification MUST remain correct.

Never place server-only secrets behind `VITE_`.

---

# APPENDIX D — APPROVED USER-FACING STATE LANGUAGE

Use Brand Bible language where applicable.

```text
Loading:
माहिती आणतोय…

Error:
काहीतरी चुकलं. पुन्हा प्रयत्न करा.

Success:
तुमची विनंती पाठवली. तज्ज्ञ संपर्क करतील.

Voice:
बोला, मी ऐकतोय.

Offline:
इंटरनेट नाही. शेवटची माहिती दाखवत आहोत.

Low confidence:
खात्री नाही; तज्ज्ञांना विचारा.
```

New critical farmer-facing copy must undergo language review.

---

# APPENDIX E — RELEASE PHILOSOPHY

A release is not successful because it contains many features.

A release is successful when:

```text
Reliable
   +
Understandable
   +
Trustworthy
   +
Accessible
   +
Safe
   +
Maintainable
```

The system should grow progressively:

```text
Simple MVP
   ↓
Verified core flows
   ↓
Reliable data
   ↓
Bounded AI
   ↓
Human escalation
   ↓
Offline resilience
   ↓
Measured scale
```

Never reverse this order merely to make the product look more sophisticated.

---

# END OF PLAYBOOK

**Operating motto:**  
> **Build → Verify → Test → Document → Approve → Continue**

**Product motto:**  
> **समजतं. करता येतं. साथ आहे.**
