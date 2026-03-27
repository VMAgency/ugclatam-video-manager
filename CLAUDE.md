[CLAUDE.md](https://github.com/user-attachments/files/26291029/CLAUDE.md)
# UGC LATAM Video Manager — Claude Project Context

## What This Project Is
A single-file HTML/CSS/JS video content management tool for UGC LATAM (ugclatam.io).
Hosted free on GitHub Pages at: https://vmagency.github.io/ugclatam-video-manager
No build tools. No framework. No Node.js. Pure vanilla HTML/CSS/JS in one file.

## The Business
UGC LATAM is a SaaS platform and brand-creator marketplace connecting global brands
with Latin American influencers across Mexico, Brazil, Colombia, Argentina, Chile, Peru.

## Host / On-Camera Talent
Chad Smalley — CEO, ugclatam.io

## Primary Goal of Videos
Grow Chad's follower count across platforms → convert to demo calls at ugclatam.io

## Video Format
- Short-form vertical: 20–60 seconds
- Platforms: TikTok, Instagram Reels, LinkedIn, YouTube Shorts, Substack
- Cadence: 3–4 videos per week (Mon/Wed/Fri + Thu bonus)
- Split: 50% LATAM Market education / 50% Platform Feature spotlights

---

## Technical Architecture

### Single File Rule
CRITICAL: This app must always remain a single index.html file.
- Never split into multiple files (no separate CSS, JS, or data files)
- All styles, scripts, and data inline in index.html
- GitHub Pages serves index.html directly — no build step needed

### GitHub Pages Deployment
- Repo: github.com/VMAgency/ugclatam-video-manager
- Live URL: https://vmagency.github.io/ugclatam-video-manager
- Always include .nojekyll file to prevent Jekyll CSS corruption
- Jekyll issue: }} in CSS @keyframes breaks stylesheet — .nojekyll prevents this

### Data Persistence
- All data stored in browser localStorage (key: ugcl_p1)
- No backend, no database for Phase 1–3
- Phase 4 will migrate to Supabase for multi-user sync
- Export/Import JSON backup built into Settings page

### Design System
- Dark editorial theme
- Font display: 'Bebas Neue' (Google Fonts)
- Font body: 'DM Sans' (Google Fonts)
- Font mono: 'DM Mono' (Google Fonts)
- CSS Variables (defined in :root — always use these, never hardcode):
  --bg: #0d0d0f       (main background)
  --bg2: #141416      (cards/sidebar)
  --bg3: #1c1c20      (inputs/secondary)
  --bg4: #242428      (tertiary surfaces)
  --accent: #c8f135   (lime green — primary accent)
  --market: #1ece8a   (teal green — Market video type)
  --platform: #9d7dff (purple — Platform video type)
  --amber: #f5a623    (filmed status / warnings)
  --red: #ff4d4d      (danger/delete)
  --text: #f0efe8     (primary text)
  --text2: #8a8980    (secondary text)
  --text3: #4a4a46    (tertiary/muted)

---

## Build Phases

### Phase 1 ✅ LIVE
Full CMS — script editor, video builder, brand settings, notes,
status tracker (Scripted → Filmed → Edited → Posted), program builder,
performance data entry, export .txt briefs

### Phase 2 ✅ BUILT (pending API connections)
N8N analytics pipeline — workflow JSON built and ready to import.
Tracks: views, likes, comments, shares, saves, watch %, profile visits,
follower growth, DMs per video across all 5 platforms.
Follower Impact Score = (new followers / views) × 1000

### Phase 3 ✅ LIVE
AI engine powered by Claude API (claude-sonnet-4-20250514):
- AI Chat Assistant (in-app)
- Script Generator (new scripts, hook generator, improve existing)
- Full 30-day program generator
- Monthly Intelligence Report (hook rankings, CTA analysis, Month N+1 recs)
API key stored in localStorage, entered via Settings → AI Engine

### Phase 4 🔲 PLANNED
- Supabase multi-user backend
- Live API auto-sync via N8N
- Slack/email performance alerts
- Compounding AI learning loop

---

## External Services

### N8N Instance
URL: https://viralmediaautomations.app.n8n.cloud
Purpose: Platform API data collection + analytics pipeline
Workflow JSON: Already built (Phase 2), ready to import

### Postiz (planned)
Purpose: Social media scheduling for Chad's videos
Deploy: Railway.app (one-click Docker deploy ~$5/mo)
N8N integration: github.com/gitroomhq/postiz-n8n

### Google Sheets (planned)
Purpose: Phase 2 data warehouse for all video performance metrics
Tabs needed: "Posted Videos" and "Performance"

---

## Content Structure

### 8 Hook Types
1. Stat Shock — lead with surprising data
2. Problem First — name the pain immediately
3. Contrarian Take — challenge conventional wisdom
4. Curiosity Gap — create intrigue, don't reveal yet
5. Chad's POV — personal experience/observation
6. Platform Demo — lead with proof/dashboard recording
7. Myth Bust — debunk a common belief
8. Speed Claim — bold time/speed assertion

### 4 CTA Types
- Type A (40%): Direct — "Book a demo at ugclatam.io"
- Type B (25%): DM — "DM me [KEYWORD] for [resource]"
- Type C (20%): Curiosity — "Link in bio"
- Type D (15%): Follow — "Follow for the next video"

### Platform Features (in spotlight order)
1. Brand ↔ Creator Marketplace & AI Matching
2. AI-Powered Campaign Tools
3. Cross-Border Payments & Contracts
4. Creator Gifting & Seeding Fulfillment
5. Campaign Analytics Dashboard
6. AI Brand Safety & Compliance
7. Full End-to-End Platform Walkthrough

### LATAM Markets Covered
Primary: Mexico, Brazil, Colombia
Secondary: Argentina, Chile, Peru

---

## Key Rules for Claude When Editing This Project

1. NEVER split index.html into multiple files
2. ALWAYS keep the .nojekyll file in the repo root
3. Use CSS variables — never hardcode colors
4. All JS state lives in the `S` object (S.brand, S.programs, S.activeId etc.)
5. All page renders go through the `renders` map object
6. The `save()` function persists to localStorage — call it after any state change
7. The `toast(msg, type)` function shows notifications ('ok' = green, 'err' = red)
8. Modal overlays use openM(id) / closeM(id) functions
9. Video status flow: Scripted → Filmed → Edited → Posted
10. When adding a new page: add div to HTML shell, add render function,
    add to renders map, add navbtn to renderSidebar()

---

## File Structure (single file, but logical sections)

```
index.html
├── <head> — Google Fonts, meta tags
├── <style> — All CSS (Phase 1 + Phase 3 AI styles at bottom)
├── <body>
│   ├── .shell (CSS Grid: topbar + sidebar + main)
│   ├── .topbar — logo, brand pill, host name, Export button
│   ├── .sidebar — rendered by renderSidebar()
│   ├── .main — all .page divs (rendered by JS)
│   ├── Modals — #m-prog, #m-video, #m-export, #m-del
│   └── #toast
└── <script>
    ├── DEFAULT DATA (BASE_VIDS array, DEFAULT_BRAND)
    ├── STATE (S object + loadState/save/prog/vid helpers)
    ├── NAVIGATION (go function, renders map)
    ├── TOPBAR (updateTopbar)
    ├── SIDEBAR (renderSidebar)
    ├── DASHBOARD (renderDash)
    ├── CALENDAR (renderCal, swWeek, toggleScript, closeScript)
    ├── SCRIPT PANEL (renderScriptPanel, swSpTab, saveScript, updStatus)
    ├── TRACKER / KANBAN (renderTracker)
    ├── ANALYTICS (renderAnalytics)
    ├── PROGRAMS (renderPrograms, swProg, createProg)
    ├── VIDEO BUILDER (renderBuilder, buildVideo)
    ├── HOOKS (renderHooks)
    ├── CTAs (renderCTAs)
    ├── FEATURES (renderFeatures)
    ├── SETTINGS (renderSettings, saveBrand, saveProgSettings)
    ├── GITHUB (renderGitHub)
    ├── PHASE 3 AI ENGINE
    │   ├── API key management (saveApiKey, testApiKey, callClaude)
    │   ├── Context builder (buildContext, getSystemPrompt)
    │   ├── AI Chat (renderAIChat, sendChat)
    │   ├── Script Generator (renderAIGenerate, genNewScript, genHooks etc.)
    │   └── Intelligence Report (renderAIReport, generateReport etc.)
    ├── MODALS & TOAST (openM, closeM, toast)
    └── BOOT (loadState, renderSidebar, updateTopbar, renderDash)
```

---

## What Has Been Completed In This Project (Session History Summary)

- Full 30-day content calendar with 14 video scripts built
- Complete Video Manager app: Phase 1 + Phase 3 live on GitHub Pages
- Phase 2 N8N workflow JSON built and ready to import
- N8N instance active at viralmediaautomations.app.n8n.cloud
- Anthropic API key connected and tested
- GitHub repo live with .nojekyll fix applied

## Next Steps
- [ ] Deploy Postiz on Railway for social scheduling
- [ ] Connect Postiz to N8N
- [ ] Install Claude Code CLI
- [ ] Add n8n-mcp + n8n-skills
- [ ] Connect platform APIs (YouTube first, then LinkedIn, TikTok, Instagram)
- [ ] Build Phase 4 multi-user Supabase backend
