# How to Submit KEC Archives to Zenodo

This is a step-by-step guide for depositing this project on Zenodo and getting a DOI.

---

## Option A — Automatic (via GitHub, easiest)

Zenodo can watch your GitHub repo and auto-create a deposit every time you publish a release.

1. Go to [zenodo.org](https://zenodo.org) and log in (create an account if you don't have one)
2. Click your name (top right) → **GitHub**
3. Find `humairaambreen/kecarchives` in the list and toggle it **ON**
4. Go back to GitHub → [create a new release](https://github.com/humairaambreen/kecarchives/releases/new)
   - Tag: `v1.0.0` (already exists — you can use it or create `v1.0.1`)
   - Zenodo will pick it up automatically
5. Go back to Zenodo → **Upload** — you'll see a draft deposit has been created
6. Review and click **Publish**
7. Zenodo gives you a DOI like `10.5281/zenodo.1234567`

Zenodo reads the `.zenodo.json` file in this repo automatically, so the title, description, keywords, and your name are already pre-filled.

---

## Option B — Manual upload

If you want to upload a zip directly without connecting GitHub:

1. Log in to [zenodo.org](https://zenodo.org)
2. Click **+ New Upload** (top right)
3. Upload a zip of this repo (download it from the [v1.0.0 release](https://github.com/humairaambreen/kecarchives/releases/tag/v1.0.0))
4. Fill in the form using the fields below

---

## What to fill in on the Zenodo form

### Upload type
Select: **Software**

### Basic information

| Field | What to write |
|---|---|
| **Title** | KEC Archives: An Academic Platform for Krishna Engineering College |
| **Authors** | Ambreen, Humaira — Affiliation: Krishna Engineering College, Bhilai |
| **Description** | Copy the block below |
| **Version** | 1.0.0 |
| **Publication date** | 2026-04-26 |
| **Language** | English |

**Description to paste:**

```
KEC Archives is the official academic platform for Krishna Engineering College, Bhilai. It replaces scattered WhatsApp groups with a verified, role-based system for students, faculty, and staff.

The platform supports four roles (guest, student, faculty, admin), scoped posts (public, batch-year, faculty-only, subject-specific), direct messaging with file attachments and peer-to-peer audio/video calls (WebRTC), group chat, push notifications, and an AI post assistant for text and image generation. Every account is OTP-verified against an institutional email.

Built with Next.js 15 (frontend) and Python FastAPI (backend), deployed on Vercel with Supabase PostgreSQL.

Live: https://kecarchives.com
Frontend repo: https://github.com/humairaambreen/kecarchives-web
Backend repo: https://github.com/humairaambreen/kecarchives-api
```

### Keywords (add each one separately)
- academic platform
- student communication
- role-based access control
- Next.js
- FastAPI
- engineering college
- PWA
- real-time messaging

### License
Select: **MIT License**

### Related/alternate identifiers

Add these three (use "URL" as the scheme for all):

| URL | Relation |
|---|---|
| `https://github.com/humairaambreen/kecarchives-web` | `hasPart` |
| `https://github.com/humairaambreen/kecarchives-api` | `hasPart` |
| `https://kecarchives.com` | `isDocumentedBy` |

---

## After publishing

Once Zenodo gives you the DOI (looks like `10.5281/zenodo.XXXXXXX`):

1. Add the DOI badge to the top of `README.md`:
   ```markdown
   [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.XXXXXXX.svg)](https://doi.org/10.5281/zenodo.XXXXXXX)
   ```

2. Add the DOI to `CITATION.cff` under `identifiers`:
   ```yaml
   identifiers:
     - type: doi
       value: "10.5281/zenodo.XXXXXXX"
       description: "Zenodo DOI for v1.0.0"
   ```

3. Add the DOI to the BibTeX block in `README.md`:
   ```bibtex
   doi = {10.5281/zenodo.XXXXXXX},
   url = {https://doi.org/10.5281/zenodo.XXXXXXX}
   ```

4. Commit the updated files and push.
