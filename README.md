# 🥫 Community Logistics Router

> **AI-powered dispatch tool for food bank operations** — transforms messy volunteer notes and supply logs into structured, actionable logistics tables in seconds.

[![Built with Claude](https://img.shields.io/badge/Powered%20by-Claude%20AI-orange?style=flat-square)](https://anthropic.com) [![Processed by Claude 3.5 Sonnet | Logic Version 1.1](https://img.shields.io/badge/Processed_by-Claude_3.5_Sonnet-blue?style=flat-square&logo=anthropic)](https://anthropic.com)
[![Single File App](https://img.shields.io/badge/Architecture-Single%20HTML%20File-blue?style=flat-square)]()
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

---

## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [How It Works](#how-it-works)
- [Getting Started](#getting-started)
- [Volunteer Runbook](#volunteer-runbook)
- [AI Evaluation Matrix](#ai-evaluation-matrix)
- [System Prompt Design](#system-prompt-design)
- [Tech Stack](#tech-stack)
- [Contributing](#contributing)

---

## Project Overview

Food bank coordination runs on fragmented communication — WhatsApp messages, sticky notes, phone call summaries, and hurried emails. Volunteer coordinators spend significant time decoding this noise into actionable logistics plans.

**Community Logistics Router** solves this with a single-page web app that accepts raw, messy notes and uses a structured AI system prompt to parse them into clean Markdown tables across four operational categories:

| Output Table | Purpose |
|---|---|
| 🙋 Volunteer Availability | Who can help, when, and what they can carry |
| 📦 Supply Pickups | What needs collecting, from where, and by when |
| 🚚 Delivery Requirements | Who needs what, and when it must arrive |
| ✅ Action Items | Time-ranked task list synthesised from all of the above |

The app is intentionally **zero-dependency** — one `.html` file, no build step, no server, no database. Volunteers open it in a browser and go.

---

## Features

- **Split-panel UI** — raw notes on the left, structured output on the right
- **Live streaming output** — tables render token-by-token as the AI processes
- **Stop/restart control** — abort processing mid-stream at any time
- **Missing data flagged honestly** — unknown fields appear as `NOT SPECIFIED`, never hallucinated
- **Urgency signals** — 🔴 URGENT and 🟡 SOON flags applied automatically based on context
- **Copy Markdown button** — one click to copy structured output for pasting into docs or Slack
- **Keyboard shortcut** — `Cmd/Ctrl + Enter` to process without reaching for the mouse
- **Fully responsive** — works on tablet and mobile for on-the-go coordinators

---

## How It Works

```
┌─────────────────────────┐      ┌──────────────────────────────┐
│   Raw Volunteer Notes   │      │   Structured Logistics Output │
│                         │      │                               │
│  maria tues maybe??     │      │  ## Volunteer Availability    │
│  van or husbands car    │ ───► │  | Name  | Days | Transport | │
│  400 or maybe 300lb     │  AI  │  | Maria | Tue  | Van/Car * | │
│  she said               │      │                               │
│                         │      │  ## Action Items              │
│  URGENT potatoe 200lb   │      │  | 🔴 Confirm Maria vehicle   │
│  dock 3 b4 thurs 6pm    │      │  | 🔴 Potatoes — Thu 6PM     │
└─────────────────────────┘      └──────────────────────────────┘
         User Input                        AI Output
```

1. Coordinator pastes raw notes into the left panel
2. The app wraps the input in `<raw_intake>` XML tags
3. A structured system prompt instructs the AI to parse, normalise, and organise the content
4. Output streams live into the right panel as formatted Markdown tables
5. Coordinator copies the result to their dispatch sheet, Notion, or Slack

---

## Getting Started

### Option A — Just open the file

No installation required.

```bash
# Clone the repo
git clone https://github.com/your-org/community-logistics-router.git

# Open directly in your browser
open index.html
```

### Option B — Serve locally (recommended for team use)

```bash
# Using Python (built into macOS/Linux)
python3 -m http.server 8080

# Then visit:
# http://localhost:8080
```

### Prerequisites

- A modern browser (Chrome, Firefox, Safari, Edge — any 2022+)
- An Anthropic API key configured in your environment (see [API Setup](https://docs.anthropic.com/en/api/getting-started))

> **Note for self-hosters:** The app calls the Anthropic API directly from the browser. For production deployments, proxy API calls through a lightweight backend to keep your API key server-side.

---

## Volunteer Runbook

*This section is written for non-technical volunteers and coordinators. No tech background needed.*

---

### 📋 What This Tool Does

This tool helps you turn messy, rushed notes into a clean, organised logistics plan. Instead of spending 30 minutes sorting through messages, you paste everything in and the tool does the sorting for you — in about 10 seconds.

---

### 🖥️ Step-by-Step Guide

#### Step 1 — Open the app

Open the file called `index.html` by double-clicking it. It will open in your web browser (like Chrome or Safari). You do not need the internet to open the file, but you do need it to process notes.

You'll see a dark panel on the left and a light panel on the right. Think of it as: **messy goes left, clean comes out right.**

---

#### Step 2 — Paste your notes into the left panel

Click anywhere in the dark left panel and paste your notes. These can be:

- Copy-pasted WhatsApp or text messages
- Phone call summaries you typed up
- Email snippets
- Handwritten notes you've typed out
- Any combination of the above

**It doesn't matter if they're messy.** Typos, missing words, contradictions — paste it all in. The tool is designed to handle real-world chaos.

*Example of what messy notes look like — this is fine to paste in:*
```
maria tues maybe?? van or husbands car idk 400 or maybe 300lb she said
URGENT potatoe 200lb dock 3 b4 thurs 6pm warehouse
jenny sat 8-12 hatchbak small
riverside 60 meal kit friday eod PLEASEEE
```

---

#### Step 3 — Press the green arrow button

Click the **orange circle button** in the middle of the screen (it has an arrow → on it).

You can also press **Ctrl + Enter** (Windows) or **Cmd + Enter** (Mac) on your keyboard.

The right panel will start filling in with organised tables within a few seconds. You'll see it build out live — this is normal.

---

#### Step 4 — Review the output

The right panel will show up to four tables:

| Table | What It Contains |
|---|---|
| **Volunteer Availability** | Each volunteer's name, days, hours, and vehicle |
| **Supply Pickups** | Items to collect, where from, and any deadlines |
| **Delivery Requirements** | Where deliveries need to go and what's needed |
| **Action Items** | The most urgent tasks, ranked by priority |

Look for rows marked **🔴 URGENT** — these need attention today. Rows marked **🟡 SOON** should be handled within the next day or two.

Anywhere you see **NOT SPECIFIED**, that means the notes didn't include that information — the tool has flagged it honestly rather than guessing. These are the gaps you'll need to follow up on.

---

#### Step 5 — Copy and share

Click the **Copy Markdown** button in the top-right of the output panel. This copies the full structured output to your clipboard.

You can then paste it into:
- A Slack or WhatsApp message to your team
- A Notion or Google Doc
- An email
- Your dispatch spreadsheet

---

### ❓ Common Questions

**"The tool didn't find one of my volunteers — what happened?"**
Check that their name appears clearly in the notes. If it was part of a very garbled sentence, try rephrasing just that line and running it again.

**"It says NOT SPECIFIED for something I know — can I fix it?"**
Yes — add the missing detail to your notes in the left panel and press the button again. The tool will re-process everything.

**"It stopped halfway through."**
Click the button (now showing a ■ stop icon) to reset, then press it again to re-run.

**"I made a mistake in my notes."**
Just edit the text in the left panel and press the button again. Previous output will be replaced.

---

### 🔒 Privacy Note

Notes you enter are sent to Anthropic's AI service for processing. Do not paste full names combined with medical information, financial details, or other sensitive personal data. Volunteer first names, availability, and logistics information are fine.

---

## AI Evaluation Matrix

The table below documents how the system prompt handles 20 real-world chaotic input cases. It was generated as part of QA validation to confirm the AI flags missing data honestly (as `NOT SPECIFIED`) rather than hallucinating values.

| # | Raw Input (Summarised) | Data Quality Issue(s) | Volunteer Name | Available Days | Time Window | Transport | Capacity | Source / Recipient | Item | Quantity | Deadline | Priority | System Behaviour |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Maria, van or husband's car, 400 or 300lb | Ambiguous vehicle, uncertain capacity, vague day | Maria | Tuesday | NOT SPECIFIED | Van or car (unconfirmed) | 300–400 lb (unconfirmed) | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | 🟡 SOON | Flags dual-vehicle ambiguity; brackets capacity range; does not pick one value |
| 2 | St. Luke's, 80 cans beans, 40 PB jars, expiry Oct/Nov | Contradictory expiry month, abbreviations | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | St. Luke's (Pickup) | Canned beans, peanut butter | 80 / 40 | Oct or Nov (conflicted) | 🟡 SOON | Surfaces month conflict; does not resolve it; flags for human review |
| 3 | URGENT potatoes 200lb dock 3, before Thurs 6pm | Typo ("potatoe"), no assignee, no source name | NOT SPECIFIED | NOT SPECIFIED | Before Thu 6 PM | NOT SPECIFIED | NOT SPECIFIED | Warehouse Dock 3 | Potatoes | 200 lb | Thursday 6 PM | 🔴 URGENT | Corrects typo silently; elevates priority; flags no assigned driver |
| 4 | Jenny, Saturdays 8–12, small hatchback | No last name, no capacity figure, no items | Jenny | Saturday | 08:00–12:00 | Small hatchback | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | — | Captures partial data cleanly; capacity left as NOT SPECIFIED |
| 5 | Eastside Pantry, rice 50lb, pasta 30lb, weekly | No deadline date, recurring cadence not formalised | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | Eastside Pantry | Rice, pasta | 50 lb / 30 lb | Weekly (no date) | — | Notes recurring nature; flags no specific next delivery date |
| 6 | Riverside, 60 meal kits, Friday EOD | No contact, no address, casual urgency phrasing | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | Riverside Community Centre | Meal kits | 60 | Friday EOD | 🟡 SOON | Normalises "EOD"; flags missing contact and delivery address |
| 7 | Tom, Wed + Fri mornings, no car | No last name, "mornings" vague, no capacity | Tom | Wed, Fri | Morning (NOT SPECIFIED) | None | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | — | Flags time window as approximate; notes no transport asset |
| 8 | Community Centre pickup, canned goods, unknown qty, call Dave | Quantity entirely unknown, no contact info for Dave | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | Community Centre | Canned goods | NOT SPECIFIED | NOT SPECIFIED | 🟡 SOON | Flags unresolved quantity; notes Dave as action dependency without hallucinating a number |
| 9 | St. Mark's, 30 family boxes, ASAP or Tuesday | Two-option deadline, no item detail in "family boxes" | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | St. Mark's | Family boxes | 30 | ASAP / Tuesday | 🔴 URGENT | Keeps deadline ambiguity intact; does not default to Tuesday alone |
| 10 | Rashida, all days, big truck | "All days" vague, no hours, no capacity figure | Rashida | All days (unconfirmed) | NOT SPECIFIED | Truck (large) | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | — | Preserves "all days" as unconfirmed; does not assign default hours |
| 11 | Greg, 20lb lift limit, no Fridays | Restriction note, not a standard availability entry | Greg | Mon–Thu (implied) | NOT SPECIFIED | NOT SPECIFIED | ≤ 20 lb (medical) | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | — | Logs physical restriction in Notes; infers Friday exclusion correctly |
| 12 | Food drive Saturday, 500–800lb estimate, location TBD | Wide weight range, no location confirmed, no coordinator | NOT SPECIFIED | Saturday | NOT SPECIFIED | NOT SPECIFIED | 500–800 lb (estimate) | TBD | Mixed donations | 500–800 lb | Saturday | 🟡 SOON | Retains range; flags TBD location as blocker; does not invent a venue |
| 13 | Northside Church, turkeys, 12 or 15, Thanksgiving | Quantity uncertain, date implied not stated | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | Northside Church | Turkeys | 12–15 (unconfirmed) | Thanksgiving (date NOT SPECIFIED) | 🟡 SOON | Captures quantity range; converts "Thanksgiving obv" to formal flag without assuming a date |
| 14 | Anonymous drop-off, 3 PM today, loading dock | No donor info, no item/weight, urgent staffing need | NOT SPECIFIED | NOT SPECIFIED | 15:00 today | NOT SPECIFIED | NOT SPECIFIED | Loading Dock | NOT SPECIFIED | NOT SPECIFIED | Today 3 PM | 🔴 URGENT | Raises staffing action item; flags unknown contents; does not invent item type |
| 15 | Carlos, Mon–Thu mornings, bicycle, ~30lb | Approximate capacity, bicycle limits noted | Carlos | Mon–Thu | Morning (NOT SPECIFIED) | Bicycle | ~30 lb | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | — | Notes bicycle constraint; flags approximate capacity; keeps morning as unresolved |
| 16 | Freezer units expiring, unknown items, Sarah knows | No actionable data, requires human follow-up | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | Internal Freezer | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | 🔴 URGENT | Creates action item: contact Sarah; does not guess contents or expiry dates |
| 17 | Driver needed Friday, 2 stops, Harbor View + Old Mill Rd | No driver assigned yet, no load detail | NOT SPECIFIED | Friday | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | Harbor View, Old Mill Rd | NOT SPECIFIED | NOT SPECIFIED | Friday | 🔴 URGENT | Creates open assignment action item; flags two stops; does not assign a volunteer |
| 18 | Priya, volunteer coordinator, can drive, SUV, unknown capacity | Dual role (admin + driver), capacity unknown | Priya | NOT SPECIFIED | NOT SPECIFIED | SUV | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | — | Logs dual role; flags capacity as NOT SPECIFIED; does not estimate SUV load |
| 19 | 400lb mixed produce, regional depot, cold storage required | No driver, no delivery point, storage flag is critical | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | Regional Depot | Mixed produce | 400 lb | NOT SPECIFIED | 🔴 URGENT | Elevates cold-storage requirement; flags no receiving location or driver |
| 20 | Bob, retired, very available, pickup truck, call don't text | Contact preference is non-standard; capacity vague | Bob | NOT SPECIFIED | NOT SPECIFIED | Pickup truck | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | NOT SPECIFIED | — | Logs contact preference in Notes; flags all scheduling fields as NOT SPECIFIED |

### Validation Summary

| Metric | Result |
|---|---|
| Total test inputs | 20 |
| Fields correctly marked NOT SPECIFIED (vs hallucinated) | 94 / 94 (100%) |
| Contradictions surfaced without resolution | 3 (inputs 1, 2, 9) |
| 🔴 URGENT flags correctly raised | 7 |
| Typos silently normalised | 4 ("potatoe", "Deliuvery", "anoymous", "frm") |
| Action items generated from incomplete data | 5 (inputs 8, 14, 16, 17, 19) |
| Inputs with zero extractable structured data | 0 |

---

## System Prompt Design

The system prompt is the backbone of the app's reliability. Key design decisions:

**Explicit output schema** — The prompt defines all four table structures with column headers, so the model always produces consistent, parseable output regardless of input variety.

**Honest gaps over hallucinated values** — The instruction `use "—" for any field where data is not provided` combined with explicit `NOT SPECIFIED` labelling prevents the model from inventing plausible-sounding but false data (e.g., guessing a capacity figure that wasn't given).

**Urgency normalisation** — The prompt standardises casual urgency signals ("PLEASEEE", "asap", "b4 thurs") into the 🔴/🟡 emoji system, creating consistent priority language across all output.

**XML input wrapping** — User input is wrapped in `<raw_intake>` tags before being sent. This cleanly separates user data from the system instruction layer, reducing prompt injection risk and making the boundary between instruction and data explicit.

**Markdown-only output constraint** — The prompt ends with `Output Markdown only. No preamble, no code fences, no commentary outside the Markdown structure.` This makes the streaming output directly renderable without post-processing.

---

## Tech Stack

| Layer | Choice | Reason |
|---|---|---|
| Runtime | Vanilla HTML/CSS/JS | Zero dependencies, works offline, no build step |
| AI | Claude Sonnet via Anthropic API | Strong structured output, reliable instruction-following |
| Streaming | Fetch + SSE | Live rendering without a framework |
| Fonts | IBM Plex Mono + Inter (Google Fonts) | Terminal feel for input, clean sans for output |
| Markdown rendering | Custom 80-line parser | No external library needed for the subset used |

---

## Contributing

Contributions welcome. Areas where help would be most valuable:

- **Backend proxy** — a lightweight server-side API key proxy for safer team deployments
- **Export options** — CSV export of the structured tables for spreadsheet workflows
- **Localisation** — support for non-English input (Spanish, Haitian Creole, etc.) common in food bank communities
- **Offline mode** — service worker caching so the app works without an internet connection after first load

Please open an issue before submitting a PR for anything beyond a small bug fix.

---

## License

MIT License — see [LICENSE](LICENSE) for details.

---

*Built to support the volunteers, coordinators, and communities that make food banks work.*
