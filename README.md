# 🧠 AI-Powered Exam Preparation Platform

This platform helps users **pass specific English-language exams and qualifications** (e.g., IELTS) through interactive exercises and AI-powered assistance. While it is designed to scale across multiple exams and skill types, the initial focus is tightly scoped around exam-first learning.

> 🎯 This is part of the **discovery phase** to explore whether a scalable, AI-powered exam platform is technically viable and practically valuable. We are developing a lightweight prototype to demonstrate the concept and outline the path to a working product.

---

## 🚀 Current Stage: Prototype

A **frontend-only implementation** that illustrates the core user flow and concept. There is no backend, storage, or user management.

### Features

- Users are presented with an exam-style exercise (e.g., writing, grammar, reading)
- Users submit an answer
- AI (via OpenAI API) provides optional feedback
- Users rate the feedback (e.g., “helpful” / “unhelpful”)
- Stateless: all logic is client-side and temporary

### Goals

- Communicate the product vision to stakeholders and domain experts
- Demonstrate the UX and AI interaction loop
- Collect feedback on the format and experience before backend or database development

---

## 🧪 Planned Next Step: Proof of Concept

A **full-stack implementation** that enables feedback learning and quality control using AI and human input.

### Features

- **Primary AI** generates feedback on user submissions
- **User feedback** is collected (e.g., “I didn’t understand this”)
- **Secondary AI** checks the **primary AI's** feedback for consistency, clarity, and correctness
- Poor-quality feedback is flagged for **human review**
- Human reviewers update prompts or feedback rules based on common failure patterns
- **Caching** of frequent Q&A reduces cost
- **Structured storage** for submissions, feedback ratings, and audit results

This stage investigates whether the system can **self-correct**, **scale feedback quality**, and **adapt** based on actual user experience.

---

## 🧠 AI System Overview

### Modular Multi-AI Pipeline (Planned)

- **Primary AI:** Generates user-facing feedback
- **Secondary AI:** Reviews and audits the feedback’s quality
- **User Feedback:** Triggers QA checks and learning loops
- **Human Review:** Refines prompts/templates based on common fail cases
- **Caching Layer:** Prevents repeated AI calls for common questions
- **Model Strategy:** Use different AI providers/models based on task complexity and cost

---

## 🧱 Tech Stack

### Prototype

- **Frontend:** SvelteKit
- **Styling:** Tailwind CSS + daisyUI
- **Form Handling:** Native Svelte bindings
- **AI Integration:** OpenAI API (GPT-3.5-turbo)
- **Deployment:** Local development only (no hosting, DB, or backend)

### Proof of Concept (Planned)

- **Backend:** FastAPI (Python)
- **AI Logic:** Modular orchestration for multi-AI flow
- **Database:** PostgreSQL (Supabase or equivalent)
- **Monitoring:** Sentry or Highlight.io
- **Cache Layer:** Redis or similar

---

## 💡 Code Philosophy

- **KISS:** Keep it simple, avoid premature abstraction
- **GRUG:** Code should be obvious and easy to onboard
- **DRY:** Reuse logic, schema definitions, and prompt formats
- **No Magic:** Clear logic over clever tricks
- **Consistent Structure:** All parts of the codebase — from API responses to frontend components — follow a standard, predictable structure. For example, API endpoints return a shared response shape, and UI elements follow a clear hierarchy (e.g., atoms, molecules, organisms) to maintain clarity and scalability.
