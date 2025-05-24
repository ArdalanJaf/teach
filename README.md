# AI-Powered English Teaching Platform

This project is a scalable platform designed to help users improve their English skills, particularly in preparation for language exams. It uses AI-generated feedback to guide user learning and will support both public use and potential B2B integrations.

---

## 🚀 Goal: Prototype (Initial Build)

The current focus is building a lean prototype to demonstrate the core user flow:

- User sees a writing prompt
- User submits a response
- OpenAI provides feedback

No database, authentication, or deployment is required at this stage.

---

## 🧱 Tech Stack

### Frontend

- **Framework:** SvelteKit
- **Styling:** Tailwind CSS + daisyUI
- **Component Design:** Simple component wrappers (e.g. `<BaseButton>`) using raw daisyUI class names internally
- **Form Handling:** Native Svelte bindings
- **Deployment (later):** Vercel

### Backend

- **AI Integration:** OpenAI API (GPT-3.5-turbo or similar)
- **Backend Server:**

  - **FastAPI (Python)** — handles all business logic, AI interactions, and DB access. This is the recommended path for scalability.

- **Database (future):** Supabase (hosted Postgres with RLS)

---

## 🧪 Prototype Scope (\~6.5 hours of work)

- One page app with a writing prompt and textarea
- Submit button triggers OpenAI call
- Feedback displayed using daisyUI alerts
- Basic loading/error state handling
- No user accounts, DB, or deployment needed yet

---

## 🔄 MVP Scope (Next Phase)

To bring the platform to public release:

### Core Features

- Auth via Clerk or Supabase Auth
- Store user data: attempts, feedback, metadata
- Add dashboard and progress tracking
- Multiple exercise types (essay, grammar, etc.)

### Payments (Optional)

- Stripe Checkout or Lemon Squeezy
- Plan tiers and feature gating

### Admin

- View and moderate user submissions
- Analytics and basic admin dashboard

### DevOps

- Vercel for frontend hosting
- Render or Fly for backend
- Sentry or Highlight.io for monitoring

---

## 🧠 Code Philosophy

- **KISS:** Keep it simple, avoid premature abstractions
- **Consistency:** Use base components to enforce design without overengineering
- **Readability:** Prefer readable class names (`btn`, `alert`) inside components
- **Scalability:** Structure code to allow future theming, accessibility, and analytics
- **Focus on UX:** Error states, loading feedback, and input validation handled at the component level

---

## 🤖 AI System Design

### Multi-Model Architecture

- Use different AI models for different tasks to balance **cost, speed, and quality**:

  - **OpenAI GPT-3.5-turbo** for general feedback and grammar correction
  - **Claude/Mixtral** or open models for basic scaffolding or faster suggestions
  - **Higher-cost models (e.g. GPT-4)** reserved for premium features or edge cases

### Feedback Oversight

- Implement a **secondary AI layer** to audit or review the primary AI's feedback

  - Ensure correctness, bias mitigation, tone, and appropriateness
  - May involve simple logic checks, confidence scoring, or LLM critique prompts

### Customization and Training

- Long-term plan includes:

  - Collecting anonymized training data from user submissions (with consent)
  - Fine-tuning lightweight models on writing types, error patterns, and exam formats
  - Incorporating user-level tuning for adaptive learning paths

---

## 🔭 Scalability Path

- Easily extendable to support more exercise types
- Built to allow role-based access (e.g. admin, teacher)
- Clean separation of frontend/backend for future API integrations
- B2B capability planned through multi-tenant or white-label models
- OpenAI usage can be swapped for Claude, Mixtral, or self-hosted LLMs later
