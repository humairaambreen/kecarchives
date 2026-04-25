# KEC Archives — v1.0.0

> The official academic platform for Krishna Engineering College, Bhilai.

**Live:** https://kecarchives.vercel.app  
**Built by:** [Humaira Ambreen](https://github.com/humairaambreen)

---

## Repositories

| Repo | Description | Stack |
|---|---|---|
| [kecarchives-web](https://github.com/humairaambreen/kecarchives-web) | Frontend application | Next.js 15, React 19, TypeScript, Tailwind CSS |
| [kecarchives-api](https://github.com/humairaambreen/kecarchives-api) | Backend REST API | Python FastAPI, SQLAlchemy, PostgreSQL |

---

## What is KEC Archives?

KEC Archives replaces scattered WhatsApp groups and informal communication at Krishna Engineering College with a verified, role-based platform. Every account is OTP-verified via institutional email, eliminating anonymous accounts and unverified information.

The platform supports four distinct roles — guest, student, faculty, and admin — each with their own dashboard, feed, and access controls.

---

## Architecture

```
┌──────────────────────────────────┐
│   Next.js 15 Frontend (Vercel)   │
│   https://kecarchives.vercel.app │
│                                  │
│  /api/v1/* (rewrites) ───────────┼──► Python FastAPI Backend
│                                  │     https://kec-api-pi.vercel.app
└──────────────────────────────────┘
                │
                ├─► Groq API          (text generation)
                ├─► HuggingFace FLUX  (image generation)
                ├─► Cloudinary        (media CDN)
                ├─► Resend            (transactional email)
                └─► Supabase          (PostgreSQL database)
```

All `/api/v1/*` requests from the browser are proxied transparently to the backend via a Next.js rewrite rule — no hardcoded API URLs in frontend code.

---

## Feature Overview

### Authentication
- OTP email verification on registration — no anonymous accounts
- Login by email or username
- Admin two-factor: password + time-limited OTP
- Silent token refresh — no logout on tab sleep

### Roles
| Role | Capabilities |
|---|---|
| Guest | View public posts only |
| Student | Feed, reactions, comments, saves, DMs, groups |
| Faculty | All student features + post creation + subject management |
| Admin | All faculty features + user management + platform stats |

### Feed & Posts
- Tab-based filtering: Public, Students, Batch, Faculty, Subject-specific
- `@mention` and `#hashtag` support in post content
- Multi-file media attachments (images, video, audio, PDF) up to 50 MB each
- Global in-memory feed cache — tab switches don't re-fetch

### Messaging
- Direct messages with file attachments, replies, reactions, edit/delete
- Message requests flow for first contact
- Typing indicators and read receipts
- Peer-to-peer audio/video calls via WebRTC (PeerJS)

### Groups
- Create group chats with invite links
- Auto-approve or manual join request approval
- Member roles: admin and member
- Full message feature parity with DMs

### Notifications
- Types: reaction, comment, mention, comment reply, group events
- Polled every 15 seconds; refetches on tab focus
- Mark individual or all as read

### AI Post Assistant *(faculty and admin only)*
- **Text generation** via Groq LLM — writes a post body from a topic
- **Image generation** via HuggingFace FLUX.1-schnell — generates post images from a prompt

### Dashboards
- **Student** — enrolled subjects, batch-year updates, quick nav
- **Faculty** — subject management with per-subject student enrollment, recent posts
- **Admin** — platform stats, full user management, subject CRUD, post deletion

### SEO & PWA
- Dynamic OG images per post and profile (Edge Runtime)
- ISR sitemap with live post and profile URLs
- JSON-LD structured data (WebSite, Organization, FAQPage schemas)
- Installable as a PWA on Android and iOS
- Backend keep-alive ping every 3 minutes (prevents Vercel cold starts)

### Themes
Three color themes — Default, Slate, Sepia — stored in localStorage.

---

## Tech Stack

### Frontend ([kecarchives-web](https://github.com/humairaambreen/kecarchives-web))

| Technology | Version |
|---|---|
| Next.js | 15.5 |
| React | 19.0 |
| TypeScript | 5.7 |
| Tailwind CSS | 3.4 |
| PeerJS (WebRTC) | 1.5.5 |
| Geist Font | 1.7 |

### Backend ([kecarchives-api](https://github.com/humairaambreen/kecarchives-api))

| Technology | Purpose |
|---|---|
| Python FastAPI | REST API |
| SQLAlchemy + Alembic | ORM and migrations |
| Supabase PostgreSQL | Database |
| JWT HS256 | Stateless auth |
| Resend | Email delivery |
| Cloudinary | Media CDN |
| Groq | LLM inference |
| HuggingFace FLUX | Image generation |
| pywebpush | Web Push notifications |

### Infrastructure

| Service | Role |
|---|---|
| Vercel | Frontend and backend hosting |
| Supabase | Managed PostgreSQL (AWS ap-southeast-2) |
| Cloudinary | Media CDN |

---

## Release History

### v1.0.0 — April 2026

Initial production release.

- Full authentication system with OTP and admin 2FA
- Role-based feed with subject-scoped posts
- Real-time direct messaging and group chat
- Peer-to-peer audio/video calls (WebRTC)
- AI post assistant (text + image generation)
- Role dashboards for students, faculty, and admins
- PWA support with push notifications
- Full SEO — dynamic OG images, ISR sitemap, JSON-LD structured data
- Deployed on Vercel with Supabase PostgreSQL

---

## Getting Started

See the individual repo READMEs for setup instructions:

- **Frontend:** [kecarchives-web/README.md](https://github.com/humairaambreen/kecarchives-web#readme)
- **Backend:** [kecarchives-api/README.md](https://github.com/humairaambreen/kecarchives-api#readme)
