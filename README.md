# KEC Archives

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19771053.svg)](https://doi.org/10.5281/zenodo.19771053)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-green.svg)](https://github.com/humairaambreen/kecarchives/releases/tag/v1.0.0)
[![Live](https://img.shields.io/badge/live-kecarchives.com-brightgreen)](https://kecarchives.com)

**KEC Archives** is the official academic platform for Krishna Engineering College, Bhilai — built to replace scattered WhatsApp groups with a proper, verified space for students, faculty, and staff.

**Live app:** [kecarchives.com](https://kecarchives.com)  
**Built by:** [Humaira Ambreen](https://github.com/humairaambreen)

---

## Source Code

This repository is the full release archive (frontend + backend together). The two are also maintained as separate development repositories:

| | Repo | Stack |
|---|---|---|
| Frontend | [humairaambreen/kecarchives-web](https://github.com/humairaambreen/kecarchives-web) | Next.js 15, React 19, TypeScript, Tailwind CSS |
| Backend | [humairaambreen/kecarchives-api](https://github.com/humairaambreen/kecarchives-api) | Python FastAPI, SQLAlchemy, PostgreSQL |

Setup instructions are in each repo's README.

---

## The Problem

At Krishna Engineering College, important information — placement notices, batch announcements, subject materials — was scattered across dozens of overlapping WhatsApp groups. There was no way to tell if something was officially from a faculty member or just a forward, and things got buried constantly.

KEC Archives fixes this. Every account requires OTP verification with an institutional email before it can post or interact, so you always know who you're talking to. Posts can be scoped to exactly the right audience: the whole college, a specific batch year, faculty only, or students enrolled in a particular subject. Nothing gets lost, and nothing is anonymous.

---

## What's Inside

### Verified accounts, role-based access
Four roles: guest, student, faculty, admin — each with different capabilities. No anonymous posting. Admin accounts require a two-step login (password + time-limited OTP) before getting in.

### Feed that actually filters
Tabs for Public, Students-only, Batch-specific, Faculty-only, and one tab per subject the user is enrolled in. The feed is cached in memory — switching tabs doesn't reload data already fetched.

### Direct messages and group chat
Full DM system: file attachments, message replies, reactions, edit/delete, typing indicators, and read receipts. Group chats have the same features, plus invite links, join request approval, and member role management.

### Audio and video calls
Peer-to-peer calls inside any DM conversation via WebRTC (PeerJS) — no server in the call path.

### AI post assistant
Faculty and admins get an AI panel on the post creation page:
- **Text generation** — type a topic, get a written post body (Groq LLM)
- **Image generation** — type a prompt, get a generated image (HuggingFace FLUX.1-schnell)

### Subject management
Faculty manage their subjects — enroll students, remove them, and scope posts to only enrolled members. Students see their enrolled subjects as feed tabs automatically.

### Role dashboards
- **Student** — batch year, enrolled subjects, recent updates from those subjects
- **Faculty** — subject management with live student search and enrollment
- **Admin** — platform stats, full user management (role changes, ban/unban, deletion), subject CRUD, post deletion

### Notifications
Reaction, comment, mention, comment reply, and group event notifications. Polled every 15 seconds and on tab focus.

### SEO and PWA
Dynamic Open Graph images per post and profile, ISR sitemap updated hourly, JSON-LD structured data. Installable as a PWA on Android and iOS.

---

## Architecture

```
┌──────────────────────────────────────┐
│  Next.js 15 Frontend (kecarchives.com)│
│                                      │
│  /api/v1/* ──────────────────────────┼──► FastAPI Backend (kec-api-pi.vercel.app)
└──────────────────────────────────────┘
                │
                ├─► Groq             LLM text generation
                ├─► HuggingFace      FLUX image generation
                ├─► Cloudinary       media storage and CDN
                ├─► Resend           transactional email (OTP delivery)
                └─► Supabase         PostgreSQL database (AWS ap-southeast-2)
```

The browser makes all API calls to the same origin. A Next.js rewrite rule forwards `/api/v1/*` to the backend transparently — no hardcoded backend URLs in the frontend code.

---

## Tech Stack

**Frontend (`apps/web`)**

| Technology | Version | Purpose |
|---|---|---|
| Next.js | 15.5 | App framework |
| React | 19.0 | UI |
| TypeScript | 5.7 | Type safety |
| Tailwind CSS | 3.4 | Styling |
| PeerJS | 1.5.5 | WebRTC calls |

**Backend (`apps/api`)**

| Technology | Purpose |
|---|---|
| Python FastAPI | REST API |
| SQLAlchemy + Alembic | ORM and migrations |
| Supabase PostgreSQL | Database |
| JWT HS256 | Auth tokens |
| Cloudinary | Media CDN |
| Resend | Email delivery |
| Groq | LLM inference |
| HuggingFace FLUX | Image generation |
| pywebpush | Web Push notifications |

---

## Release History

### v1.0.0 — April 2026

First production release. Full feature set deployed on Vercel with Supabase PostgreSQL.

---

## Citing This Software

```bibtex
@software{ambreen_2026_kecarchives,
  author    = {Ambreen, Humaira},
  title     = {{KEC Archives: An Academic Platform for Krishna Engineering College}},
  month     = apr,
  year      = 2026,
  publisher = {Zenodo},
  version   = {v1.0.0},
  doi       = {10.5281/zenodo.19771053},
  url       = {https://doi.org/10.5281/zenodo.19771053}
}
```

---

## License

MIT — see [LICENSE](LICENSE).
