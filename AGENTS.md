# AGENTS.md

## Project

KenduriAmpang RSVP — a PWA for managing guest invitations and RSVPs for a Malaysian wedding reception (Ampang, Selangor). Guests open personalized invitation links (e.g. `/invite/ABCD123`) shared via WhatsApp and submit attendance, pax count, and dietary notes; admins track RSVPs and export data.

**Current status: planning stage.** The only file is `SOFTWARE DESIGN DOCUMENT.txt` (the full SDD). No code, package manifests, or git history exist yet — read the SDD before doing any implementation work.

## Planned stack (from the SDD)

- Frontend: Next.js + React, Tailwind CSS, `next-pwa`, React Hook Form, Zustand
- Backend: NestJS REST API with Prisma ORM
- Database: PostgreSQL on Supabase
- Deployment: Vercel (frontend), Railway (backend), Supabase (DB)

## Key requirements to preserve when implementing

- Mobile-first UI; guests access links from WhatsApp on phones. First load < 3s; works offline after first visit (PWA caching of invitation page/assets).
- RSVP flow: name + phone required, guest count ≥ 1, editable until the RSVP deadline.
- Data model: `Event` (1) → `RSVP` (N) ← (1) `Guest`; RSVP keyed by `invitation_code` on Guest.
- API endpoints per SDD: `POST /api/rsvp`, `GET /api/dashboard`.
- Admin side: dashboard KPIs (invited/confirmed/declined/pending), Excel export, WhatsApp click-to-chat reminders.
- Security: HTTPS only, input validation, rate limiting / anti-spam.
- Accessibility: WCAG 2.1 AA, large touch targets.
- Content: bilingual Malaysian context — English UI logic with Malay event copy (e.g. "Bismillahirrahmanirrahim" header, date formats like "21 February 2027").
- Out of scope for MVP: payments/e-wallet, live streaming, QR check-in, table assignment, e-Angpow (all Phase 2).

## Conventions for future agents

- When scaffolding, keep the MVP scope listed in the SDD's final section (invitation, RSVP form, guest count, Maps/Waze links, WhatsApp contact, admin dashboard, Excel export).
- Update the SDD or this file if decisions deviate from the planned stack.
