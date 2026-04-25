# KEC Archives

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.XXXXXXX.svg)](https://doi.org/10.5281/zenodo.XXXXXXX)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-green.svg)](https://github.com/humairaambreen/kecarchives/releases/tag/v1.0.0)
[![Live](https://img.shields.io/badge/live-kecarchives.com-brightgreen)](https://kecarchives.com)

**KEC Archives** is the official academic platform for Krishna Engineering College, Bhilai — built to replace scattered WhatsApp groups with a proper, verified space for students, faculty, and staff.

**Live app:** [kecarchives.com](https://kecarchives.com)  
**Built by:** [Humaira Ambreen](https://github.com/humairaambreen)

---

## Source Code

The project is split into two repositories:

| | Repo | What it is |
|---|---|---|
| Frontend | [humairaambreen/kecarchives-web](https://github.com/humairaambreen/kecarchives-web) | Next.js 15 app — everything the user sees and interacts with |
| Backend | [humairaambreen/kecarchives-api](https://github.com/humairaambreen/kecarchives-api) | Python FastAPI — handles the database, auth, emails, AI, and media |

Setup instructions are in each repo's README.

---

## The Problem It Solves

At most engineering colleges, important information gets buried in overlapping WhatsApp groups — placement notices go to the wrong batch, faculty announcements get lost in noise, and there's no way to know if something is officially from a faculty member or just a forward.

KEC Archives fixes this by requiring every account to be verified with an institutional email OTP before it can post or interact. Posts can be scoped to exactly the right audience: the whole college, a specific batch year, faculty only, or students enrolled in a particular subject. Everyone knows who they're talking to, and everything is findable later.

---

## What's Inside

### Verified accounts, role-based access
Four roles — guest, student, faculty, admin — each with different capabilities. No anonymous posting. Admins go through a two-step login (password + OTP) before getting access.

### Feed that actually filters
The feed has tabs for Public, Students-only, Batch-specific, Faculty-only, and one tab per subject the user is enrolled in. The feed cache is global — switching tabs doesn't reload data already fetched.

### Direct messages and group chat
Full DM system with file attachments, message replies, reactions, edit/delete, typing indicators, and read receipts. Group chats work the same way, with invite links, join request approval, and member role management.

### Audio and video calls
Peer-to-peer calls inside any DM conversation, built on WebRTC via PeerJS — no server in the call path.

### AI post assistant
Faculty and admins get an AI panel on the post creation page:
- **Text generation** — type a topic, get a professionally written post body (Groq LLM)
- **Image generation** — type a prompt, get a generated image (HuggingFace FLUX.1-schnell)

### Subject management
Faculty manage their assigned subjects — enroll students, remove them, scope posts to subject members only. Students see their enrolled subjects as feed tabs automatically.

### Role dashboards
- **Student** — batch year, enrolled subjects, recent updates from those subjects
- **Faculty** — subject management hub with live student search and enrollment
- **Admin** — platform stats, all-user management (role changes, ban/unban, deletion), subject creation/deletion

### Notifications
Reaction, comment, mention, comment reply, and group event notifications. Polled every 15 seconds, also triggers on tab focus.

### SEO and PWA
- Dynamic Open Graph images per post and per profile (Edge Runtime)
- ISR sitemap with live post and profile URLs revalidated hourly
- JSON-LD structured data (WebSite, Organization, FAQPage)
- Installable as a PWA on Android and iOS

---

## Architecture

```
┌─────────────────────────────────────┐
│  Next.js 15 Frontend (kecarchives.com)  │
│                                     │
│  /api/v1/* ─────────────────────────┼──► FastAPI Backend (kec-api-pi.vercel.app)
└─────────────────────────────────────┘
                │
                ├─► Groq             LLM text generation
                ├─► HuggingFace      FLUX image generation
                ├─► Cloudinary       media storage and CDN
                ├─► Resend           transactional email (OTP delivery)
                └─► Supabase         PostgreSQL database (AWS ap-southeast-2)
```

The browser makes all API calls to the same origin. A Next.js rewrite rule forwards `/api/v1/*` transparently to the backend — no hardcoded backend URLs in the frontend code.

---

## Tech Stack

**Frontend**

| Technology | Version | Purpose |
|---|---|---|
| Next.js | 15.5 | App framework |
| React | 19.0 | UI |
| TypeScript | 5.7 | Type safety |
| Tailwind CSS | 3.4 | Styling |
| PeerJS | 1.5.5 | WebRTC calls |

**Backend**

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

First production release. Covers the full feature set described above, deployed on Vercel with Supabase PostgreSQL.

---

## Citing This Software

If you use or reference KEC Archives in academic work, please cite it as:

```bibtex
@software{ambreen_2026_kecarchives,
  author       = {Ambreen, Humaira},
  title        = {{KEC Archives: An Academic Platform for Krishna Engineering College}},
  month        = apr,
  year         = 2026,
  publisher    = {Zenodo},
  version      = {v1.0.0},
  doi          = {10.5281/zenodo.XXXXXXX},
  url          = {https://doi.org/10.5281/zenodo.XXXXXXX}
}
```

*(Replace `XXXXXXX` with the DOI assigned after Zenodo deposit.)*

---

## License

MIT — see [LICENSE](LICENSE).
