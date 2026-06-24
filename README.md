# xdpdr

An AI mental health companion for people experiencing **Depersonalization/Derealization Disorder (DPDR)** — a dissociative condition where reality, the self, or both feel unreal, foggy, or detached.

This repository is a project overview. The production code is private while the product is in active development.

---

## Why I'm building this

I had DPDR.

For people who haven't experienced it, the short version: imagine looking at your own hands and not recognizing them as yours. Walking through your city and feeling like the world is behind a pane of glass. Knowing intellectually that you are real, that your life is real, while feeling on a continuous, exhausting level that none of it is. It is one of the most isolating things a person can go through, partly because the symptoms themselves are hard to describe, and partly because most people — including most therapists — have never heard of it.

I recovered. The path out is real, but it's slow, non-linear, and most of the available resources are either clinical jargon, recovery forums of varying quality, or generic mindfulness apps that don't understand the specific shape of this condition.

**xdpdr is the companion I wish I'd had during recovery.** Not a replacement for therapy. Not a chatbot pretending to be a therapist. A grounded, structured tool that meets people where they are: in stabilization when symptoms are acute, or in exploration when they're ready to do the deeper work.

---

## What it is

xdpdr is a full-stack web application built around **Nova**, an AI companion powered by the **Anthropic Claude API**.

Nova operates in two distinct modes:

- **Stabilization mode** — for acute symptom episodes. Grounding techniques, sensory anchoring, short structured responses designed to reduce overwhelm rather than analyze it.
- **Exploration mode** — for users in a calmer state who want to work through triggers, patterns, and the cognitive loops that sustain DPDR.

Onboarding routes users into one of three paths based on where they are in their experience — newly experiencing DPDR, long-term sufferers, or calm researchers — each receiving a different first conversation with Nova.

Nova detects the appropriate mode automatically — based on language signals, time of day, and conversation context — and shifts between them within a session as needed. Conversations follow a structured protocol, not free-form chat — the model is constrained by a session schema and a memory model that distinguishes between session context, user profile, and long-term progress markers.

---

## Architecture

```
React + Vite + Tailwind frontend
        │
        │  JWT auth
        ▼
Node.js / Express API ──► MongoDB Atlas (user data, sessions, profile)
        │
        │  conversation context + memory + mode
        ▼
Nova (Anthropic Claude API)
        │
        ▼
   structured response: grounding /
   exploration / referral to professional
```

Key design decisions:

- **Dual-mode design over single chatbot.** A single Nova that tries to be everything at once would fail at both jobs. Stabilization needs short, simple, sensory. Exploration needs depth and patience. Same model, different system prompts and conversation protocols.
- **Memory schema, not raw chat history.** Naive chat history grows unbounded and confuses long-term context with session context. Nova's memory is structured: stable user profile, current session state, and explicit long-term progress markers.
- **Hard professional-referral boundaries.** Nova is not a therapist. The system is designed to recognize cases that need human professional support and route to them, not pretend to handle them.
- **Security from day one.** JWT auth, bcrypt password hashing, Helmet, CORS, rate limiting on the API. Mental health data is sensitive — the bar is higher than for a generic web app.

---

## In progress: RAG knowledge base

Nova's responses are currently grounded in the system prompt and conversation context. The next major piece is a **Retrieval Augmented Generation** knowledge base built from source material I've written across **11 sections** covering:

- What DPDR is and isn't
- Common triggers and maintaining factors
- Grounding techniques (with the reasoning behind each)
- The cognitive patterns that sustain the condition
- Recovery markers and what realistic progress looks like
- When and how to seek professional help

The source material is complete. The ingestion pipeline, vector store, and retrieval logic are the next build phase.

---

## Stack

- **Frontend:** React, Vite, Tailwind CSS, React Router, Context API
- **Backend:** Node.js, Express
- **Database:** MongoDB Atlas, Mongoose
- **AI:** Anthropic Claude API
- **Auth & security:** JWT, bcrypt, Helmet, CORS, rate limiting
- **Planned:** RAG pipeline, vector store

---

## Status

Active development. Rebuilding v1 into a production-grade architecture. Pre-launch.

The production code lives in private repositories. This page exists so the project is visible and the reasoning is documented.

For questions or collaboration: [vicente.ibarra@theoros.se](mailto:vicente.ibarra@theoros.se)
