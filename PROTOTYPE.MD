# 🧪 Prototype Plan

This prototype is a **bare-bones interactive demo** to validate the core UX and teaching concept.

### 🎯 Goals

- Display a static list of exercises (MCQ + writing)
- Allow users to answer questions and view basic results
- Simulate AI feedback with dummy responses
- No user accounts, no admin, no DB

### 📦 Features (Included)

- [x] Hardcoded exercises
- [x] Basic UI flow: / → /exercise → /result
- [x] Feedback simulation with delay

### 🔜 Phase 2

- Hook in real AI (OpenAI or Claude)
- Add backend API for feedback
- Optional: add basic Zod validation

### 🧠 Prototype Constraints

This prototype skips:

- User authentication
- CMS / content editing
- Real database
- Admin dashboard
- Exercise progression logic
- Deployment

## ✅ Prototype TODO List (Phase 1 – No AI)

- [x] Project setup (SvelteKit + Tailwind)
- [ ] Exercise selection UI (3–4 static examples) — **1.5 hrs**
- [ ] Answer interaction UI (text, MCQ, T/F) — **2 hrs**
- [ ] Feedback display UI (static text for now) — **1 hr**
- [ ] Loading and error states — **1 hr**
- [ ] Tailwind layout & styling polish — **1–1.5 hrs**
- [ ] Deployment to Vercel — **0.5 hr**
- [ ] Final polish & buffer — **1.5 hrs**

**Total Estimate:** ~9 hrs
