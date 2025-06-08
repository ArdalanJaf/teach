# 📚 Exam Preparation Platform Long-term plan (subject to change)

This platform helps users **pass specific English-language exams and qualifications** (e.g. IELTS) through interactive gamified exercises. While it is designed to scale across multiple qualification types, the initial focus is tightly scoped around **learning for a specific exam**.

> 🦴 This is a full-stack project structured around _Strategic Grug_ principles: minimal complexity, dev-friendly structure, scalable foundations.

> 🧪 This README outlines the full MVP vision (and beyond).  
> For the current prototype scope and progress, see `PROTOTYPE.MD`.

---

## 🧱 Tech Stack

| Layer      | Tech                                         | Purpose                                                |
| ---------- | -------------------------------------------- | ------------------------------------------------------ |
| Frontend   | SvelteKit, Tailwind CSS, daisyUI             | UI rendering, styling, routing, user and admin UI      |
| Backend    | Fastify, Zod, Prisma                         | API server, validation, DB access, logic separation    |
| Database   | PostgreSQL                                   | Store users, answers, feedback, etc.                   |
| AI Module  | Python service (FastAPI / modal / langchain) | Optional module for writing feedback and AI assistance |
| Cache      | Redis (optional)                             | Reduce AI cost/latency with prompt/response storage    |
| Monitoring | Sentry or Highlight.io                       | Observability and error tracking                       |

---

## 📁 Folder Structure

```txt
/apps
  /frontend           → SvelteKit frontend app
    /routes             → Pages (e.g. /exercise, /result, /admin)
    /components         → UI atoms, molecules
    /lib                → Utils (fetch, stores, helpers)
    /config             → App-level constants (e.g. supportedLangs)
    /tests              → Unit and integration tests for UI flows

  /backend            → Fastify backend API
    /routes             → Fastify route declarations (eg. /admin, /user, /exercise)
    /controllers        → Request handlers (thin)
    /services           → App logic (e.g. submitAnswerService, token logic, CMS)
    /adapters           → DB access via Prisma (e.g. getUserByEmail)
    /entities           → Prisma schemas (User, Exercesises, etc.)
    /transformers       → Convert Prisma entities ⇄ DTOs (Zod schemas stored in packages/schemas)
    /tasks              → Background jobs (e.g. cleanup, audits)
    /config             → App env, feature flags, etc.
    /tests              → Unit and integration tests for backend logic

  /ai-module          → Python AI service (dumb, stateless)
    /routers            → API routes if needed (e.g. /generate-feedback)
    /prompts            → Prompt templates, reusable structures
    /strategies         → Feedback generation + auditing logic
    /llms               → Providers (OpenAI, Claude, local models)
    /cache              → In-memory or Redis access layer
    /config             → API keys, model tuning, etc.
    /tests              → Prompt/strategy unit tests

/packages
  /schemas            → Zod schemas used for validation + API contracts
  /shared-types       → TS types/enums shared across apps
  /logger             → Logging util with route/DTO awareness

/infrastructure (planned)
```

---

## 🧠 AI System Overview (Planned)

### AI as a Feature

- Most exercises (e.g. multiple choice, grammar) are non-AI.
- Writing tasks **use AI** to generate feedback.
- Users can request additional **AI help**, gated by a **token/life system**.
- The platform functions fully without AI; AI features enhance user experience and writing improvement.

### High-Level Summary

- Users complete writing tasks or request help on exercises.
- AI (LLM) provides feedback or assistance.
- Responses are cached when possible to reduce cost.
- Users rate the AI’s response (e.g. helpful / unhelpful).
- Feedback data is stored for quality tracking.
- In early stages, AI mistakes are accepted — feedback helps flag bad outputs.
- Over time, human reviewers identify common failure patterns and improve prompts.
- Eventually, a secondary AI may be introduced to automatically detect poor responses and retry once with a refined prompt — but only where it adds clear value.

### Modular Multi-AI Pipeline

- **Primary AI:** Generates user-facing feedback
- **Secondary AI (future):** Reviews and audits the feedback’s quality
- **User Feedback:** Triggers QA checks and learning loops
- **Human Review:** Refines prompts/templates based on common fail cases
- **Caching Layer:** Prevents repeated AI calls for common questions
- **Model Strategy:** Use different AI providers/models based on task complexity and cost

---

## ✍️ Content Management System (Admin Panel)

All exercises and instructional content are created and managed through an internal admin interface (merged into the main frontend app under `/admin`).

> We chose **not to use a headless CMS** (e.g. Strapi, Sanity) to avoid syncing logic between CMS and backend, prevent schema drift, and ensure accurate previews using real app components. By building our own admin UI, we maintain a single source of truth, full control over rendering, and a clean integration with our exercise logic and gamified flow. In short a bit more work early on for much less work down the road.

### Features:

- Create/edit exercises with structured templates (e.g. MCQ, writing)
- Assign exercises to a curriculum, stage, and difficulty level
- Add optional media assets via S3 (e.g. images for prompts)
- Control token cost, hints, and explanations
- Draft/publish toggle for release management
- Live preview using the same rendering components as learners (future?)

### Translation Strategy:

- Exercises support multilingual content via schema-based fields (`{ en: "...", es: "..." }`)
- The app UI defaults to English; general copy is hardcoded or wrapped in lightweight `t()` helpers for future i18n
- Long-term support for multiple curricula (e.g. Spanish, American exams) is built into the schema
- Scoped content zones (e.g. empty state messages, onboarding blurbs) will be admin-editable where safe — static UI labels remain code-defined (future)

---

## 🦴 Strategic Grug Philosophy (needs futher refinement - too verbose to be grug!)

> Normal Grug say:
>
> > "grug code now. problem later not grug problem."
> > then grug live in spaghetti cave. many bugs. grug cry.
>
> Strategic Grug say:
>
> > "grug no build future today, but grug make space for future. cave have good bones."
> > so when future come, grug not trapped. grug adapt, scale, survive winter.

- KISS: Keep it simple, avoid premature abstraction
- GRUG: Code should be obvious and easy to onboard
- DRY: Reuse logic, schema definitions, and prompt formats
- No Magic: Clear logic over clever tricks
- Consistent Structure: All parts of the codebase follow a standard, predictable structure.
  For example, API endpoints return a shared response shape, UI elements follow atoms → molecules → organisms pattern, and apps/packages follow a shared folder layout.
  Shared layout example:

/app-or-package
/routes → API or page routes (Fastify, SvelteKit, etc.)
/services → App logic or orchestration (side-effectful)
/adapters → I/O logic (DB, APIs, files)
/lib → Stateless helpers (pure functions)
/config → Constants, env, flags
/tests

- Modular by Role: Each folder/package has a clear responsibility — adapters, services, schemas, etc.
- Shared Core, Clear Boundaries: Shared schemas (via Zod) define strong contracts across apps
- Service-Oriented, Not Over-Engineered: Apps communicate over simple, clear interfaces — no monoliths or microservice mess
- Typed End-to-End: TS + Zod used wherever possible to enforce correctness across systems
