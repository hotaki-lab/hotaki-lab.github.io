# SiteLog AI — Construction Daily Report

**A mobile-first, AI-powered daily site report tool for field engineers.** Built as a single HTML file that runs entirely in the browser — no installation, no app store, no backend required.

---

## Table of Contents

1. [Overview](#overview)
2. [Getting Started](#getting-started)
3. [Features](#features)
   - [Configuration](#1-configuration)
   - [Project Info & GPS](#2-project-info--gps)
   - [Weather — Auto Wind & Temperature](#3-weather--auto-wind--temperature)
   - [Equipment Log](#4-equipment-log)
   - [Labor Compliance Log](#5-labor-compliance-log)
   - [Site Notes & Voice Input](#6-site-notes--voice-input)
   - [Multi-Language Support](#7-multi-language-support)
   - [Site Photos with AI Captions](#8-site-photos-with-ai-captions)
   - [Report Section Selection](#9-report-section-selection)
   - [AI Report Generation](#10-ai-report-generation)
   - [Digital Signatures](#11-digital-signatures)
   - [Email Delivery](#12-email-delivery)
   - [Offline Mode & Auto-Save](#13-offline-mode--auto-save)
4. [Mobile Usage Guide](#mobile-usage-guide)
5. [Offline Installation (PWA)](#offline-installation-pwa)
6. [Multi-Inspector Use](#multi-inspector-use)
7. [API Key Setup](#api-key-setup)
8. [Privacy & Data Storage](#privacy--data-storage)
9. [Troubleshooting](#troubleshooting)
10. [Technology Stack](#technology-stack)

---

## Overview

SiteLog AI eliminates the end-of-day paperwork burden for site engineers. Instead of filling out lengthy forms, the engineer speaks or types rough notes in any language, and the AI generates a fully structured, professional daily report — including equipment registers, labor compliance logs, site photos with captions, and legally binding signatures.

### Who It's For

- **Field Engineers / Site Engineers** — primary report authors
- **Owner's Field Inspectors** — sign off on completed shifts
- **Contractor Superintendents** — counter-sign at end of day
- **Project Managers** — receive emailed reports
- **Safety Officers** — equipment and incident documentation

### Key Principles

- **Zero friction for the field** — speak, tap, and you're done
- **Works offline** — no internet required during data entry
- **No installation** — opens in any mobile browser
- **Everything in one file** — easy to host and share

---

## Getting Started

### Prerequisites

- An [Anthropic API key](https://console.anthropic.com/) (for AI report generation and photo captioning)
- A modern browser (Chrome, Safari, Firefox, Edge — on desktop or mobile)
- The page hosted on HTTPS (required for GPS and camera access)

### Quick Start

1. Open the hosted URL in your browser
2. Scroll to **Configuration** and paste your Anthropic API key
3. Enter the email address where reports should be sent
4. Click **Save Config**
5. Fill in Project Info — GPS and weather will auto-populate
6. Log equipment and labor
7. Type or speak your site notes
8. Upload site photos
9. Have both parties sign
10. Click **⚡ Generate Full Report**

---

## Features

---

### 1. Configuration

Located at the top of the page.

| Field | Description |
|---|---|
| Anthropic API Key | Your `sk-ant-...` key from [console.anthropic.com](https://console.anthropic.com). Stored locally on your device only — never transmitted to any third party. |
| Email Report To | The email address that receives the generated report. Can be a distribution list. |

- **Save Config** — saves both values to local device storage so you don't need to re-enter them each session
- **Load Saved Draft** — restores a previously auto-saved draft, including all equipment, labor, notes, and weather
- **Clear Draft** — wipes the saved draft from local storage

The **Auto-Save status indicator** (green dot) confirms when data has been saved locally. The timestamp updates every time a field changes.

---

### 2. Project Info & GPS

A six-field header block that populates the report's cover section.

| Field | Notes |
|---|---|
| Project Name | Free text — e.g. "Highway 50 Bridge Deck, Span 3" |
| Engineer Name | Full name of the reporting engineer |
| Report Date | Defaults to today's date |
| Overall Progress % | 0–100 percentage of project completion |
| Workers on Site | Headcount for the day |
| Shift | Day / Night / Full Day |

#### GPS Coordinates

GPS coordinates are **automatically captured** when the page loads and location permission is granted.

- Displays as: `37.123456, -121.654321  (±8m)` — latitude, longitude, and accuracy radius
- The **📍 badge** in the top header shows current GPS status:
  - `📍 Getting GPS...` — acquiring signal
  - `📍 GPS ✓ (tap to refresh)` — successfully locked
  - `📍 Tap to get GPS` (orange) — permission denied or timed out
- **Tap the 📍 badge** at any time to refresh coordinates
- Coordinates are printed in the report header and included in every auto-saved draft

> **iOS Note:** Safari on iPhone may prompt for location permission. Tap **Allow** when prompted. If the badge shows orange, tap it to trigger a fresh permission request.

---

### 3. Weather — Auto Wind & Temperature

Weather is split into two parts: condition selection and auto-fetched measurements.

#### Condition Chips

Tap one:  ☀ Sunny · ⛅ Partly Cloudy · 🌧 Rainy · 🌩 Storm · 🌬 Windy · ❄ Cold

#### Wind Speed & Temperature (Auto-Fetch)

Click **🌬 Auto-fetch** to pull live data from [Open-Meteo](https://open-meteo.com/) — a free, no-key-required weather API.

- Requires GPS to be locked first
- Auto-fills **Wind Speed (mph)** and **Temperature (°F)** from current conditions at the site's exact coordinates
- Displays: `✓ Live data: Wind 12 mph @ 245° · Temp 78°F`
- Both fields can also be entered manually

> **Why this matters for bridge construction:** OSHA and most DOT specifications require wind speed to be documented for elevated work, crane operations, and concrete pours. Auto-fetch eliminates the need for a separate anemometer reading.

---

### 4. Equipment Log

**Mandatory for accident investigation and insurance compliance.** Every piece of equipment on site must be logged.

#### Adding Equipment

- **＋ Add Equipment** — adds a general equipment row (crane, pump, scaffolding, generator, etc.)
- **🚛 Add Vehicle** — adds a vehicle row with additional fields for Make/Model and License Plate

#### Equipment Fields

| Field | General | Vehicle |
|---|---|---|
| Equipment ID | ✅ e.g. "EQ-001" | ✅ |
| Name / Type | ✅ e.g. "Tower Crane" | ✅ e.g. "Dump Truck" |
| Make & Model | — | ✅ e.g. "Caterpillar 777G" |
| License Plate | — | ✅ e.g. "ABC-1234" |
| Status | ✅ | ✅ |

#### Equipment Status

Each equipment row has a status selector:

| Status | Description |
|---|---|
| Active | Operating normally |
| Idle | On site but not working — triggers idle time capture |
| Off Site | Left the site during the shift |
| Breakdown | Mechanical failure — should be noted in site notes |

#### Idle Time Capture

When status is set to **Idle**, an orange row automatically expands below the equipment entry:

- **Hours** and **Minutes** fields for precise idle time
- **Reason** field — e.g. "Waiting for inspection", "No material delivery", "Rain delay"

This satisfies fleet management, rental billing verification, and productivity analysis requirements.

The AI includes a formatted **Equipment Register** section in the generated report, listing all units with their status and any idle time recorded.

---

### 5. Labor Compliance Log

**Legally required for labor law compliance, OSHA record-keeping, and prevailing wage verification.**

#### Adding Workers

- **＋ Add Worker** — adds a single worker row
- **⚡ Bulk Add** — opens a dialog where you paste a list of workers, one per line, in the format:

```
Full Name, Role, Company
John Martinez, Ironworker, ABC Steel Co.
Maria Nguyen, Electrician, XYZ Electric
Wei Chen, Carpenter, General Contractor
```

All workers are added in a single action — ideal for large crews.

#### Labor Fields

| Field | Description |
|---|---|
| Legal Full Name | First and last name as it appears on ID |
| Role / Trade | e.g. Carpenter, Foreman, Electrician, Ironworker |
| Company / Sub | Employing company or subcontractor name |

The AI generates a **Labor Compliance Register** section in the report listing all workers in a formatted table.

> **Tip:** For large projects with a fixed crew, use **Load Saved Draft** to restore yesterday's labor list and make only the changes — additions and departures.

---

### 6. Site Notes & Voice Input

The main free-form input for the day's activities. This is what the AI uses to write the narrative sections of the report.

#### How to Use

**Option A — Type:** Enter rough notes in any form. Grammar, structure, and completeness don't matter — the AI fixes it all.

**Option B — Voice Record:** Tap **🎙 Record Voice** to capture a verbal field report. Tap again to stop. Then hit Generate.

**Option C — Hint Chips:** Tap starter phrases to quickly begin common note types:
- `# Concrete pour` — inserts "Poured concrete on "
- `# Safety` — inserts "Safety incident: "
- `# Delay` — inserts "Delay caused by "
- `# Inspection` — inserts "Inspection by "
- `# Materials` — inserts "Materials delivered: "
- `# RFI` — inserts "RFI submitted for "
- `# Plan` — inserts "Tomorrow we plan to "

#### Example Input

```
Poured 40m³ concrete columns C1-C8, done by noon. 2hr delay morning — mixer truck broke down. 
Safety near miss at scaffold level 3, worker wasn't clipped in, corrected immediately, toolbox 
talk given. Rebar delivery arrived 3pm, stored at laydown area B. Tomorrow starting formwork level 3.
```

The AI turns this into 6 structured professional sections.

---

### 7. Multi-Language Support

Field crews often speak languages other than English. The engineer can enter notes in their native language and the AI will translate and formalize the content into English in the final report.

#### Supported Input Languages

| Button | Language |
|---|---|
| 🇺🇸 English | Default — no translation needed |
| 🇪🇸 Español | Spanish |
| 🇨🇳 中文 | Chinese (Mandarin) |
| 🇻🇳 Tiếng Việt | Vietnamese |

Tap the language pill before entering notes. The placeholder text in the notes box switches to that language as a guide. When the AI generates the report, it is instructed to detect the input language, translate the content, and produce the full formal report in English.

---

### 8. Site Photos with AI Captions

Documentation photographs are a standard requirement in construction daily reports.

#### Uploading Photos

- **Tap the photo drop zone** to open the device camera or photo library
- On mobile, this opens the rear camera by default for immediate capture
- **Multiple photos** can be selected at once
- **Drag and drop** is supported on desktop

#### AI Auto-Captioning

Each photo card includes an **⚡ AI Caption** button. Tapping it sends the photo to Claude's vision model, which analyzes the image and writes a professional 1–2 sentence construction caption.

Example AI-generated captions:
- *"Reinforced concrete columns C1 through C4 at Level 2 with formwork in place, ready for pour."*
- *"Scaffolding platform at Gridline E, Level 3 — handrail installed per OSHA 1926.502."*
- *"Structural steel beam splice connection at mid-span, bolts torqued and inspection tag applied."*

#### Caption All

**⚡ AI Caption All Photos** runs AI captioning on every uploaded photo in sequence — ideal when uploading a batch of 10–15 photos at end of shift.

#### Photo Categories

Each photo can be tagged:

| Category | Use Case |
|---|---|
| General | Miscellaneous documentation |
| Progress | Work completed, milestone documentation |
| Safety | Hazards, near-misses, PPE, corrective actions |
| Quality | Inspections, material samples, test results |
| Defect | Non-conforming work, punch list items |
| Material | Delivered materials, storage conditions |
| Equipment | Equipment on site, breakdown documentation |

The generated report includes a **Photo Log** section with thumbnail images, category tags, and captions embedded directly in the report output.

---

### 9. Report Section Selection

Toggle which sections appear in the generated report. All six are enabled by default.

| Section | Content |
|---|---|
| ✅ Work Completed | Tasks performed, quantities, locations, crew assignments |
| ✅ Safety & HSE | Incidents, near-misses, PPE observations, toolbox talks |
| ✅ Resources & Equipment | Labor deployed, machinery utilization, material consumption |
| ✅ Delays & Issues | Causes of delays, RFIs submitted, change order events |
| ✅ Quality & Inspections | Tests conducted, inspector visits, non-conformances |
| ✅ Plan for Tomorrow | Next day schedule, targets, crew requirements |

The AI also always includes:
- **Equipment Register** — from the Equipment Log
- **Labor Compliance Register** — from the Labor Log
- **Photo Log** — from uploaded photos
- **Sign-Off Block** — with signature images

---

### 10. AI Report Generation

Click **⚡ Generate Full Report** to produce the complete report.

The AI receives:
- All project header fields
- GPS coordinates
- Weather, wind, and temperature
- The complete equipment register with idle times
- The complete labor register
- Your rough site notes (translated if needed)
- The selected report sections

It returns a fully formatted professional report with:
- Cover header block (project, date, engineer, GPS, weather)
- All selected narrative sections with formal language
- Equipment Register table
- Labor Compliance Register
- Photo Log with thumbnail grid and captions
- Signature block with captured signature images

#### After Generation

| Button | Action |
|---|---|
| ↺ Regenerate | Re-runs AI generation with current data |
| ⎘ Copy Text | Copies the full plain-text report to clipboard |
| ↓ Download | Downloads as a `.txt` file named `SiteReport_[Project]_[Date].txt` |
| ✉ Send Email | Opens your mail client pre-filled with the report |

---

### 11. Digital Signatures

At the end of each shift, two parties must sign the report.

#### Signature Fields

**Owner / Field Inspector**
- Name input field for the inspector's full name
- Signature canvas — draw with finger (mobile) or mouse (desktop)

**Contractor Superintendent**
- Name input field for the superintendent's full name
- Signature canvas — draw with finger (mobile) or mouse (desktop)

Both signature images are embedded in the generated report output and visible in the on-screen report preview. The download and email export includes the signature block.

To clear a signature, tap **Clear** below the canvas.

> **Mobile Signing:** The signature canvas uses the browser's Pointer Events API with device pixel ratio scaling, ensuring crisp, accurate signature capture on all iPhone and Android devices. The page will not scroll while your finger is on the canvas.

---

### 12. Email Delivery

When a report is generated with an email address configured, the app opens your device's mail client with:

- **To:** the configured email address
- **Subject:** `Site Daily Report – [Project Name] – [Date]`
- **Body:** the full report text (first 1,900 characters, with a note that the full version was generated)

For complete report delivery, the engineer can copy the full text using **⎘ Copy Text** and paste it into the email body, or send the downloaded `.txt` file as an attachment.

#### Offline Email Queue

If the report is generated while offline, it is added to a **send queue** stored on the device. When the device comes back online, the queue is automatically processed — reports are generated and the mail client opens for each queued entry.

The queue count is shown as a badge in the offline banner: `2 queued`.

---

### 13. Offline Mode & Auto-Save

SiteLog AI is designed to work in areas with no internet connectivity — remote bridge sites, tunnels, underground work, and mountainous terrain.

#### Auto-Save

Every field change triggers an auto-save to the browser's **localStorage** after a 1.5-second debounce. This includes:

- All project info fields
- Weather selection and wind/temperature values
- GPS coordinates
- Equipment list (all rows, all fields, idle times)
- Labor list (all rows)
- Site notes text and selected language
- Signature names

The green dot and timestamp in the Configuration panel confirm the last save time.

#### Load Saved Draft

**📂 Load Saved Draft** restores all saved data — including the complete equipment and labor lists — exactly as they were when last saved. Useful for:

- Resuming after a browser crash or accidental close
- Carrying forward yesterday's equipment and crew list

#### Offline Report Generation

If you tap **⚡ Generate Full Report** while offline:

1. All current data is saved to the offline queue in localStorage
2. A message confirms the report is queued
3. When the device goes online, the queue processes automatically
4. The mail client opens with the generated report

The **online/offline badge** in the top header shows real-time network status (● ONLINE / ● OFFLINE).

---

## Mobile Usage Guide

SiteLog AI is optimized for use on a phone or tablet at the job site.

### Recommended Workflow (End of Shift)

1. **Open the page** — GPS acquires automatically
2. **Tap 🌬 Auto-fetch** — wind and temperature fill in
3. **Check equipment rows** — set statuses, log idle times
4. **Check labor rows** — verify everyone is listed
5. **Tap the photo zone** — photograph key activities (3–10 photos)
6. **Tap ⚡ AI Caption All** — all photos captioned in 30 seconds
7. **Tap the notes box** — speak or type the day's highlights
8. **Have both parties sign** — Inspector and Superintendent
9. **Tap ⚡ Generate Full Report** — report appears in ~10 seconds
10. **Tap ✉ Send Email** — report delivered

Total time for a typical daily report: **5–10 minutes.**

### Tips for Phone Use

- **GPS:** Allow location permission when prompted — tap the 📍 badge if it shows orange
- **Camera:** Tap the photo drop zone to open the rear camera directly
- **Signing:** Use your finger to draw your signature; the canvas prevents the page from scrolling while you sign
- **Voice:** Tap 🎙 Record Voice to dictate notes hands-free
- **Offline:** You can fill out the entire report without internet — only the AI generation step requires connectivity

---

## Offline Installation (PWA)

You can install SiteLog AI as a home screen app so it launches like a native app, even without internet.

### iPhone / iPad (Safari)

1. Open the page URL in **Safari**
2. Tap the **Share** button (box with arrow)
3. Scroll down and tap **Add to Home Screen**
4. Name it "SiteLog AI" and tap **Add**

### Android (Chrome)

1. Open the page URL in **Chrome**
2. Tap the three-dot menu (⋮)
3. Tap **Add to Home Screen**
4. Tap **Add**

The app will appear on your home screen and launch in full-screen mode without the browser toolbar.

> **Note:** Because all data entry works offline, the engineer can open the app at the start of the shift, fill it out throughout the day, and generate the report once WiFi or cell signal is available.

---

## Multi-Inspector Use

The current version is a **single-user tool** — one device, one daily report.

For projects with multiple field inspectors working simultaneously, each inspector can use the tool independently on their own device and generate separate reports for their area of responsibility.

**For true multi-user simultaneous reporting** (e.g., multiple inspectors contributing to one shared daily report), the tool would need to be upgraded to include a shared database backend. This would allow:

- Each inspector to submit their section from their own device
- A supervisor to merge all sections into a single master report
- Real-time visibility across the team

This upgrade would require a service like Firebase, Supabase, or a custom API and is a planned enhancement.

---

## API Key Setup

1. Go to [console.anthropic.com](https://console.anthropic.com)
2. Sign in or create an account
3. Navigate to **API Keys**
4. Click **Create Key** — copy the `sk-ant-...` value
5. In SiteLog AI, paste it into the **Anthropic API Key** field and click **Save Config**

### Cost Estimate

Each report generation uses approximately 1,000–2,000 input tokens and 1,000–2,000 output tokens. Photo captioning uses approximately 500–1,000 tokens per image (vision input).

At current Claude pricing, a typical daily report with 10 photos costs approximately **$0.03–$0.08 USD.**

---

## Privacy & Data Storage

| Data | Where It's Stored |
|---|---|
| API Key | Your device's localStorage only |
| Email address | Your device's localStorage only |
| Draft data (project info, equipment, labor, notes) | Your device's localStorage only |
| Site photos | In-memory only — never written to disk or uploaded except to the Anthropic API for captioning |
| GPS coordinates | In-memory and localStorage draft — never sent to any server except embedded in the AI prompt |
| Signatures | In-memory as canvas image data |
| Generated reports | Your device (download) and your email client |

**No data is stored on any server other than Anthropic's API** (which receives your prompts and photos solely for AI processing). The application has no backend, no database, and no analytics.

---

## Troubleshooting

### GPS not working on iPhone
- Make sure the page is accessed over **HTTPS** (required by iOS)
- When the page loads, tap **Allow** on the location permission prompt
- If you tapped **Don't Allow**, go to **iPhone Settings → Safari → Location** and set it to **Ask** or **Allow**
- Tap the 📍 badge in the top header to retry GPS acquisition

### Wind/Temperature not fetching
- GPS must be locked first — wait for `📍 GPS ✓` before tapping Auto-fetch
- The app uses the Open-Meteo API which requires internet connectivity
- If GPS is showing an error, resolve that first

### Equipment / Worker buttons not responding
- Scroll down to make sure the button is fully visible and not obscured by the mobile keyboard
- Try tapping slightly above center of the button
- If the page shows a JavaScript error in the browser console, try a hard refresh (hold Shift + reload on desktop, or close and reopen the tab on mobile)

### Signature canvas not working on mobile
- Use a single finger — multitouch is not supported for signing
- Make sure you're drawing on the white canvas area, not the surrounding dark background
- If signing isn't registering, try a slow deliberate stroke first

### Report generation fails
- Confirm your API key is saved (the placeholder should show `✓ API key saved`)
- Check that you have internet connectivity (● ONLINE badge in header)
- Make sure the Site Notes field is not empty — the AI requires notes to generate the report
- If you see an API error message, check your API key has sufficient credits at [console.anthropic.com](https://console.anthropic.com)

### Email not sending automatically
- The app uses your device's built-in mail client (Mail on iPhone, Gmail app on Android)
- Make sure a default mail app is configured on your device
- If the mail client doesn't open, use **⎘ Copy Text** to copy the report and paste it manually

---

## Technology Stack

| Component | Technology |
|---|---|
| UI Framework | Vanilla HTML/CSS/JavaScript — no dependencies |
| Fonts | Google Fonts: Bebas Neue, DM Sans, DM Mono |
| AI Model | Claude Sonnet (claude-sonnet-4-20250514) via Anthropic API |
| Weather API | [Open-Meteo](https://open-meteo.com/) — free, no API key required |
| GPS | Browser Geolocation API |
| Signatures | HTML5 Canvas with Pointer Events API + Device Pixel Ratio scaling |
| Offline Storage | Browser localStorage |
| Photo Handling | FileReader API (base64 in-memory) |
| Voice Recording | MediaRecorder API |
| Hosting | Any static file host — GitHub Pages, Netlify, Vercel, AWS S3, etc. |

---

## Version History

| Version | Changes |
|---|---|
| v3.0 | Equipment log with idle time, labor compliance log, multilanguage support, offline queue, GPS auto-capture, wind/temp auto-fetch, digital signatures with Pointer Events + DPR fix, email delivery |
| v2.0 | Site photo upload, AI captioning per photo, caption-all batch, photo category tags, photo log in report |
| v1.0 | Initial release — AI report generation, weather, voice input, section toggles, copy/download |

---

*SiteLog AI — Built for the field. Designed for the office.*
