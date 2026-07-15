<div align="center">

# 🌙 Luna — Cycle Wellness Tracker

### A Private, Single-File Menstrual Cycle Tracker

<img src="https://img.shields.io/badge/Domain-Health%20%26%20Wellness-2563EB?style=for-the-badge">
<img src="https://img.shields.io/badge/Category-Personal%20Tracker-EA580C?style=for-the-badge">
<img src="https://img.shields.io/badge/Type-Local--First%20Web%20App-16A34A?style=for-the-badge">
<img src="https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge">

> A single-file, private, browser-based menstrual cycle tracker that predicts periods and fertile windows a full year out, gives phase-by-phase wellness guidance, and includes an AI companion for personalized questions.

**[🌙 Try Luna Live](https://akshatsingh1427.github.io/Luna/)**

</div>

---

## Table of Contents

- [Live Demo](#-live-demo)
- [What It Does](#what-it-does)
- [Key Features](#key-features)
- [How Predictions Work](#how-predictions-work)
- [Luna AI](#luna-ai)
- [Data & Privacy](#data--privacy)
- [Tech Stack](#tech-stack)
- [How to Run](#how-to-run)
- [Notes for Further Development](#notes-for-further-development)

---

## 🌐 Live Demo

**[https://akshatsingh1427.github.io/Luna/](https://akshatsingh1427.github.io/Luna/)**

Hosted on GitHub Pages — open the link and complete the one-time setup to start.

> Note: the live version calls the Anthropic API client-side for Luna AI. Without a wired-up key/proxy, chat requests will fall back to the built-in offline responder rather than fail outright.

---

## What It Does

Luna is a self-contained cycle dashboard built for one person's use — no accounts, no server, no data leaving the browser (aside from optional AI chat requests). On first load it asks for your last period start date, average cycle length, and period length, then builds:

- **A live status dashboard** — current cycle day, current phase, days until next period, days until ovulation
- **A full-year forecast** — every predicted period, fertile window, and ovulation day for the whole calendar year, browsable month by month
- **Four phase guides** (Menstrual, Follicular, Ovulation, Luteal) — each with what to eat, what to avoid, what to do, self-care tips, and exercise suggestions tailored to that phase
- **A daily log** — mood tags, symptom tags, and a free-text note, saved per day with history
- **Luna AI** — a chat panel that answers cycle questions using the user's actual data (current day, phase, upcoming dates) as context

---

## Key Features

| Feature | Details |
|---|---|
| **Onboarding** | One-time setup: name, last period start date, cycle length, period length |
| **Cycle Math** | Computes current phase and day from the stored profile; supports variable cycle lengths |
| **Year Calendar** | Month-by-month grid showing predicted period days, fertile window, and ovulation day; navigate by year |
| **Phase Library** | 4 phases × (eat / avoid / do / self-care / exercise) tip cards, each with a "why" explanation |
| **Daily Log** | 8 mood tags, symptom chips, free-text note — stored with date, cycle day, and phase |
| **Log History** | Chronological list of past entries with delete support |
| **AI Chat** | Floating panel with quick-reply chips ("What should I eat today?", "PMS mood help", "My predictions") and free-text input |
| **Reset** | One-click wipe of all stored data to start over |

---

## How Predictions Work

`getCycleInfo(date)` computes cycle day and phase from the stored `lastPeriod` date and `cycleLen`/`periodLen`, using fixed phase boundaries:

| Phase | Days |
|---|---|
| Menstrual | 1–5 |
| Follicular | 6–13 |
| Ovulation | 14–17 |
| Luteal | 18–28 (scales with cycle length) |

The year calendar (`buildYearCal()`) projects this forward across every cycle in the selected year to mark predicted period ranges, fertile windows, and ovulation days.

---

## Luna AI

The chat panel calls the Anthropic Messages API directly from the browser (`claude-sonnet-4-20250514`), with a system prompt that injects the user's name, current cycle day/phase, and upcoming predicted dates as context — so answers are personalized without a backend.

> **Important:** the API is called client-side with no key management shown in the file, so `sendAI()` / `callLuna()` will fail in a plain browser deployment unless wired up to a backend proxy or given a valid endpoint/key. This is expected — there's a built-in fallback: if the API call fails, `getFallbackReply()` answers PMS, prediction, and general questions from hard-coded logic based on the user's own cycle data, so the app stays functional offline or without an API key.

---

## Data & Privacy

Everything is stored in the browser via `localStorage`:

| Key | Contents |
|---|---|
| `luna_profile` | Name, last period date, cycle length, period length |
| `luna_logs` | Array of daily log entries (date, cycle day, phase, moods, symptoms, note) |

No data is sent anywhere except the optional AI chat request. The **Reset** button in the nav clears both keys and returns to onboarding.

---

## Tech Stack

<div align="center">

<img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white">
<img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white">
<img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black">
<img src="https://img.shields.io/badge/Anthropic%20API-D97757?style=for-the-badge">

</div>

| Layer | Technology |
|---|---|
| **Structure** | Single HTML file |
| **Styling** | Vanilla CSS — custom properties, `clamp()` responsive type, soft gradient theme |
| **Logic** | Vanilla JavaScript, no framework, no build step |
| **Fonts** | Cormorant Garamond, DM Sans (Google Fonts) |
| **Storage** | Browser `localStorage` |
| **AI** | Anthropic Messages API (client-side fetch), with an offline fallback responder |

---

## How to Run

```
1. Open luna_cycle_tracker.html in any modern browser
2. Complete the one-time setup (name, last period date, cycle & period length)
3. Explore your dashboard, phase guides, year forecast, and daily log
4. Tap the ✨ button to chat with Luna AI
```

No install, server, or dependencies required.

---

## Notes for Further Development

- Wire `callLuna()` to a real key/proxy before relying on live AI responses in production — right now it silently falls back to canned replies on any fetch failure (including a missing key), which is safe but worth knowing about
- All wellness/food content is static, hard-coded per phase — not personalized beyond phase and day
- This is a wellness/lifestyle tool, not a medical device — no diagnostic claims are made, and severe-symptom messages already nudge the user toward seeing a doctor

<div align="center">

**Built as a private, single-file tool — no accounts, no server, no tracking.**

</div>
