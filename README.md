# UGC LATAM Video Manager

Production-grade video content management tool for the UGC LATAM 30-day short-form video program. Built for Chad Smalley, CEO of [ugclatam.io](https://ugclatam.io).

## Features

- **30-Day Content Calendar** — visual week-by-week calendar with clickable video cards
- **Script Editor** — inline hook / body / CTA editing with auto-save to localStorage
- **Status Tracker** — kanban board: Scripted → Filmed → Edited → Posted
- **Program Builder** — create new 30-day content blocks, duplicate from template
- **Hooks Library** — 8 proven hook types with usage guidance
- **CTA Rotation** — 4 CTA types with frequency strategy and LinkedIn tips
- **Feature Sequence** — platform feature spotlight order with rationale
- **Export** — download full scripts as .txt briefs for filming sessions

## Quick Start (GitHub Pages)

```bash
# 1. Clone or download this repo
git clone https://github.com/YOUR_USERNAME/ugclatam-video-manager.git
cd ugclatam-video-manager

# 2. Push to GitHub (if not already)
git add .
git commit -m "Initial deploy"
git push origin main

# 3. Enable GitHub Pages
# Repo → Settings → Pages → Source: main branch / root → Save
# Your URL: https://YOUR_USERNAME.github.io/ugclatam-video-manager
```

## File Structure

```
ugclatam-video-manager/
├── index.html          # Main app entry point
├── css/
│   └── app.css         # Full stylesheet (dark editorial theme)
├── js/
│   └── app.js          # Application logic
├── data/
│   └── programs.js     # All video program data (edit here)
└── README.md
```

## Adding a New Month

Edit `data/programs.js` to add a new program object to the `programs` array, or use the **+ New Program** button in the UI (creates from template).

To update scripts, edit the `videos` array inside the relevant program object and push:

```bash
git add data/programs.js
git commit -m "Add Month 2 program"
git push
```

## Content Strategy

- **50% LATAM Market** (green) — Mexico, Brazil, Colombia, Argentina, Chile, Peru
- **50% Platform Features** (purple) — Marketplace, AI Matching, Payments, Gifting, Analytics, Brand Safety
- **Primary CTA**: Book a demo at ugclatam.io
- **Cadence**: Mon / Wed / Fri (+Thu) = 3–4 videos/week
- **Format**: 20–60 second vertical short-form

## Tech Stack

Vanilla HTML + CSS + JavaScript. No build tools, no dependencies, no Node.js required. Works offline. Data persists via `localStorage`.

---

Built for UGC LATAM · [ugclatam.io](https://ugclatam.io)
