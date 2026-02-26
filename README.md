# SiteLog AI — Construction Daily Report

**A mobile-first, AI-assisted daily site report tool for field engineers, inspectors, and superintendents.**  
No installation. No app store. No backend server. A single HTML file hosted anywhere, running on any phone or desktop browser.

---

## Table of Contents

1. [What Is SiteLog AI?](#1-what-is-sitelog-ai)
2. [Who It Is For](#2-who-it-is-for)
3. [System Requirements](#3-system-requirements)
4. [Hosting & Deployment](#4-hosting--deployment)
5. [First-Time Setup](#5-first-time-setup)
6. [Full Feature Reference](#6-full-feature-reference)
   - [6.1 Sticky Header Bar](#61-sticky-header-bar)
   - [6.2 Offline Banner & Queue Counter](#62-offline-banner--queue-counter)
   - [6.3 Configuration Panel](#63-configuration-panel)
   - [6.4 Project Info Panel](#64-project-info-panel)
   - [6.5 GPS Auto-Capture](#65-gps-auto-capture)
   - [6.6 Weather Condition Selector](#66-weather-condition-selector)
   - [6.7 Wind Speed & Temperature Auto-Fetch](#67-wind-speed--temperature-auto-fetch)
   - [6.8 Equipment Log](#68-equipment-log)
   - [6.9 Idle Time Capture](#69-idle-time-capture)
   - [6.10 Labor Compliance Log](#610-labor-compliance-log)
   - [6.11 Bulk Labor Entry Modal](#611-bulk-labor-entry-modal)
   - [6.12 Site Notes — Voice & Text Input](#612-site-notes--voice--text-input)
   - [6.13 Multi-Language Input Support](#613-multi-language-input-support)
   - [6.14 Quick-Start Hint Chips](#614-quick-start-hint-chips)
   - [6.15 Report Section Toggles](#615-report-section-toggles)
   - [6.16 Site Photos with AI Auto-Captioning](#616-site-photos-with-ai-auto-captioning)
   - [6.17 Digital Signatures](#617-digital-signatures)
   - [6.18 Generate Report — Two-Path Choice Modal](#618-generate-report--two-path-choice-modal)
   - [6.19 As-Filled Report (No AI, No Internet Required)](#619-as-filled-report-no-ai-no-internet-required)
   - [6.20 AI-Generated Professional Report](#620-ai-generated-professional-report)
   - [6.21 Report Output Panel](#621-report-output-panel)
   - [6.22 Email Delivery — How It Actually Works](#622-email-delivery--how-it-actually-works)
   - [6.23 HTML Report File — Embedded Photos & Signatures](#623-html-report-file--embedded-photos--signatures)
   - [6.24 Auto-Save & Draft System](#624-auto-save--draft-system)
   - [6.25 Offline Mode & AI Report Queue](#625-offline-mode--ai-report-queue)
7. [Recommended End-of-Shift Workflow](#7-recommended-end-of-shift-workflow)
8. [Choosing Between the Two Report Types](#8-choosing-between-the-two-report-types)
9. [Email System — Step-by-Step Explanation](#9-email-system--step-by-step-explanation)
10. [Installing as a Home Screen App (PWA)](#10-installing-as-a-home-screen-app-pwa)
11. [Mobile Tips & Best Practices](#11-mobile-tips--best-practices)
12. [Multi-Inspector Use](#12-multi-inspector-use)
13. [API Key Setup & Cost Estimate](#13-api-key-setup--cost-estimate)
14. [Privacy & Data Storage](#14-privacy--data-storage)
15. [Troubleshooting](#15-troubleshooting)
16. [Technology Stack](#16-technology-stack)
17. [Version History](#17-version-history)

---

## 1. What Is SiteLog AI?

SiteLog AI is a complete construction daily report system packaged as a single `.html` file. The engineer opens it in their phone browser on site, fills in the day's data, and generates a formal report — including equipment registers, labor compliance logs, site photos with professional captions, GPS-stamped location, live weather data, and legally binding digital signatures from both the owner's inspector and the contractor's superintendent.

The tool has two report generation modes available to every user:

**As-Filled Report** — No API key needed. No internet needed. No waiting. Tapping the button immediately compiles every field the engineer entered into a complete, structured, professionally formatted document. This mode works 100% offline and is available to all inspectors regardless of whether they use AI.

**AI Professional Report** — The Claude AI model receives all entered data plus the engineer's rough field notes and rewrites everything into formal construction industry prose, with full narrative paragraphs for each section. This requires an Anthropic API key and an active internet connection, but queues automatically if the device is offline.

Both modes produce identical output: a live on-screen preview, a downloadable self-contained HTML file with all photos and signatures embedded, and an automatic email to the configured address.

---

## 2. Who It Is For

| Role | How They Use It |
|---|---|
| **Field Engineer / Site Engineer** | Primary user — fills in all daily data, captures photos, types or speaks notes |
| **Owner's Field Inspector** | Reviews the report on-screen and signs the Inspector canvas at shift end |
| **Contractor Superintendent** | Counter-signs the Superintendent canvas at shift end |
| **Project Manager** | Receives the daily email with the HTML attachment containing all photos and signatures |
| **Safety Officer** | Accident documentation — equipment IDs, vehicle details, incident notes, photo evidence |
| **Labor Compliance Officer** | Prevailing wage and headcount verification from the formatted labor register |

---

## 3. System Requirements

| Item | Requirement |
|---|---|
| **Browser** | Chrome, Safari, Firefox, or Edge — on any phone, tablet, or desktop. **Voice recording requires Chrome or Safari** — Firefox does not support the Web Speech API; all other features work in Firefox normally |
| **Hosting** | Must be served over **HTTPS** — required by browsers for GPS and camera access |
| **Anthropic API key** | Only needed for the AI report option and AI photo captioning — not required for As-Filled reports |
| **Internet connection** | Only required for: AI report generation, AI photo captioning, weather auto-fetch, and email sending |
| **Data entry** | Fully functional offline — all fields, equipment, labor, photos, and signatures work without internet |

---

## 4. Hosting & Deployment

The entire application is one `.html` file with no build process, no Node modules, no dependencies, and no server-side code. Upload the file to any static hosting service and share the URL with the team.

**Free hosting options that provide HTTPS automatically:**

- **GitHub Pages** — push the file to a repository, enable Pages in repository Settings → Pages → Deploy from branch
- **Netlify** — drag and drop the file directly at [netlify.com/drop](https://app.netlify.com/drop)
- **Vercel** — import a repository or use the CLI (`vercel deploy`)
- **AWS S3 + CloudFront** — suitable for enterprise deployments with access control

> The file **must** be served over HTTPS, not plain HTTP. All of the options above provide HTTPS automatically. GPS and camera access are blocked by browsers on plain HTTP pages — this is a browser security policy that cannot be overridden.

To update the tool, replace the `.html` file on the host. All user data lives in the browser's `localStorage` on each device and is completely unaffected by file updates on the server.

---

## 5. First-Time Setup

1. Open the hosted HTTPS URL in your browser on the device you will use in the field
2. In the **Configuration** panel, enter your Anthropic API key — paste the full `sk-ant-...` value (optional; skip entirely if using As-Filled reports only)
3. Enter the email address that should receive completed reports — this can be a personal address, a team inbox, or a distribution list
4. Tap **Save Config** — both values are stored permanently on the device in `localStorage`
5. When the browser asks for location permission, tap **Allow** — this enables GPS auto-capture
6. The tool is now fully configured for daily use

On every subsequent visit, the API key and email address are restored automatically from `localStorage`. You will never need to re-enter them on the same device unless you clear your browser data.

---

## 6. Full Feature Reference

---

### 6.1 Sticky Header Bar

The header bar is fixed at the top of the screen at all times while scrolling. It contains three live status indicators plus the application name.

**GPS Badge**

Shows the current GPS status in real time. Tappable at any time to trigger a fresh location request.

| Badge Text | Colour | Meaning |
|---|---|---|
| `GPS Getting GPS...` | Blue | Initial acquisition in progress after page load |
| `GPS (tap to refresh)` | Blue | Location successfully locked |
| `Tap to get GPS` | Orange | Permission denied, position unavailable, or timed out — tap to retry |
| `Updating...` | Blue | Refresh actively in progress after tap |

**Online / Offline Badge**

Updates in real time as the device detects or loses internet connectivity.

| Badge | Meaning |
|---|---|
| `ONLINE` (green) | Internet available — all features active |
| `OFFLINE` (red) | No internet — offline mode active, AI features queued |

**Date Badge**

Displays today's date in plain text for reference while filling in the form.

---

### 6.2 Offline Banner & Queue Counter

When the device has no internet, a red warning banner appears immediately below the header:

> You are offline. All data is saved locally on this device. AI reports will be generated and emailed automatically when internet is restored.

If AI reports have been queued while offline, an orange badge next to the banner shows the number of pending reports (e.g. `2 queued`). The moment the device reconnects to any network, the queue is processed automatically without any action from the engineer — the AI generates each report and opens the mail client.

---

### 6.3 Configuration Panel

This panel contains persistent settings that are stored in `localStorage` and survive page reloads and browser restarts.

**Anthropic API Key**

Paste your `sk-ant-...` key here. It is stored in `localStorage` and is only ever transmitted to the Anthropic API endpoint when generating AI reports or requesting photo captions. Once saved, the field clears itself and the placeholder changes to `API key saved` — the key is never displayed again for security. It persists across all future sessions on this device.

**Email Report To**

The destination address for all generated reports. Can be a personal address, a team project inbox, or a full distribution list. Stored in `localStorage` alongside the API key. Updated by saving the config.

**Save Config**

Persists both fields to `localStorage` under the key `sitelog_config` as a JSON object. Confirms the save with an alert. This is a one-time setup action per device.

**Load Saved Draft**

Restores all field data from the most recent auto-save checkpoint. The following are restored:

- All six project info fields (project name, engineer, date, progress, workers, shift)
- Weather condition chip selection
- Wind speed value and temperature value
- GPS coordinates from the last successful fix
- The complete equipment list — all rows, all fields, idle times, idle reasons, vehicle details
- The complete labor list — all rows, all name/role/company fields
- Site notes text content
- Selected input language
- Inspector and superintendent name fields (text inputs only — drawn signatures are not stored)

Photos and drawn signature canvas data are **not** restored by Load Draft because they are session-only data held in browser memory, not `localStorage` (photos are large binary data; signature canvas images are not serialised to avoid storage bloat).

**Clear Draft**

Deletes the saved draft from `localStorage` after a confirmation prompt. Does not affect the API key, email address, or offline queue.

**Auto-Save Status Indicator**

A small dot and timestamp display below the buttons shows the state of the in-progress draft:

| Dot Colour | Text Example | State |
|---|---|---|
| Grey | `No draft saved` | No draft exists yet |
| Green | `Draft saved: Thu 26 Feb, 3:47 PM` | A prior draft exists |
| Green | `Auto-saved: 3:52 PM` | Just auto-saved |

---

### 6.4 Project Info Panel

Six fields that populate the header block of every generated report.

| Field | Input Type | Description |
|---|---|---|
| **Project Name** | Text | Full project name, e.g. `I-80 Bridge Deck Replacement – Span 4` |
| **Engineer Name** | Text | Full name of the reporting engineer as it should appear on the report |
| **Report Date** | Date picker | Defaults to today's date on every page load |
| **Overall Progress %** | Number (0–100) | Percentage of total project work completed to date |
| **Workers on Site** | Number | Total headcount present and working during this shift |
| **Shift** | Dropdown | Day Shift / Night Shift / Full Day |

The GPS coordinates display also lives in this panel directly below the six fields — see section 6.5.

Every field in this panel triggers an auto-save 1.5 seconds after the last keystroke.

---

### 6.5 GPS Auto-Capture

GPS coordinates are requested automatically when the page finishes loading (`DOMContentLoaded` event) via `navigator.geolocation.getCurrentPosition()` with the following options:

- `enableHighAccuracy: true` — requests the most precise fix available (satellite GPS rather than cell tower triangulation)
- `timeout: 15000` — 15-second maximum wait before triggering an error callback
- `maximumAge: 60000` — will accept a cached position up to 60 seconds old to avoid delays on re-opens

**What is captured:**

- Latitude to 6 decimal places (approximately 0.1 metre precision)
- Longitude to 6 decimal places
- Accuracy radius in metres as reported by the device's GPS hardware

**Display format in the project panel:**

```
37.812456, -121.654321  (±8m)
```

**On success:** The GPS badge turns blue. Coordinates are stored in the auto-save draft.

**On failure**, the badge turns orange and the project panel displays a specific, actionable error message:

| Error Code | Display Message |
|---|---|
| 1 — Permission Denied | `Location denied — tap GPS button & allow access` |
| 2 — Position Unavailable | `Location unavailable — check GPS signal` |
| 3 — Timeout | `GPS timed out — tap GPS to retry` |

Tapping the GPS badge at any time — whether it's blue or orange — clears the error state and fires a fresh location request.

**Why GPS matters on construction reports:** GPS coordinates provide legally defensible proof that the report was physically created at the job site. Many owner inspection protocols, State DOT specifications, and OSHA record-keeping requirements mandate GPS location documentation on daily reports for infrastructure and bridge projects.

> **iOS note:** Safari on iPhone requires the user to tap **Allow** when the location permission prompt appears. If it was previously denied, the engineer must go to **Settings → Privacy & Security → Location Services → Safari → Allow While Using App**, then tap the GPS badge to retry.

---

### 6.6 Weather Condition Selector

Six pill-shaped tap-to-select chips. Only one can be active at a time. The active condition is highlighted in yellow with a filled border.

| Chip | Condition | Use When |
|---|---|---|
| Sunny | Clear sky, full sun | Visibility good, no precipitation |
| Cloudy | Overcast or partly cloudy | No precipitation but reduced sun |
| Rainy | Rain present | Rain at any point during the shift |
| Storm | Thunderstorm or severe weather | Lightning, heavy rain, or work stoppage due to weather |
| Windy | Elevated wind, no precipitation | Affects crane operations or elevated work |
| Cold | Freezing or near-freezing | Affects concrete placement or curing |

The selection is stored in the auto-save draft and appears verbatim in the report header block.

---

### 6.7 Wind Speed & Temperature Auto-Fetch

**Wind Speed (mph)** and **Temperature (°F)** both have manual number entry fields. Both can also be auto-populated from a live weather API with a single tap.

**Auto-fetch button**

Calls the [Open-Meteo API](https://open-meteo.com/) — a free weather service requiring no API key — using the site's GPS coordinates. The API request fetches:

- Current wind speed at 10 metres, converted to mph
- Current wind direction in degrees
- Current air temperature, converted to °F

On success, the status line displays:

```
Live data: Wind 14 mph @ 248° · Temp 72°F
```

Both the wind speed field and temperature field are populated automatically. The engineer can override either value manually after auto-fetch if conditions have changed.

**Requirements for auto-fetch to succeed:**

1. GPS coordinates must be locked first — if GPS has not been captured, the button shows an alert instructing the engineer to tap the GPS badge first
2. Internet connection must be available — if offline, enter values manually

**Why wind speed documentation is critical for bridge and infrastructure projects:**

OSHA 29 CFR 1926 Subpart R (Steel Erection) and most State DOT construction specifications require wind speed to be documented in the daily report for the following operations: crane picks and rigging, elevated platform work, structural steel connection, concrete placement on structures, post-tensioning operations, and driven pile installation. The auto-fetch eliminates the need for a separate handheld anemometer reading and manual transcription.

---

### 6.8 Equipment Log

Every piece of equipment present on the site during the shift must be documented daily. This is a non-negotiable compliance requirement for OSHA accident investigation, insurance liability documentation, rental billing verification, and fleet management reporting.

**Adding equipment:**

- **Add Equipment** — adds a general equipment row for non-vehicle, non-licensed machinery: tower cranes, concrete pumps, generators, air compressors, welding machines, temporary lighting, formwork systems, vibrators, and any other on-site plant
- **Add Vehicle** — adds a vehicle-specific row with the additional fields required for licensed motor vehicles

**General equipment fields:**

| Field | Placeholder | Purpose |
|---|---|---|
| Equipment ID | `EQ-001` | Internal asset tag, rental contract number, or fleet ID |
| Name / Type | `Tower Crane` | Descriptive name identifying the piece of equipment |
| Status | Dropdown | See status table below |

**Vehicle-specific additional fields (shown when Add Vehicle is used):**

| Field | Placeholder | Purpose |
|---|---|---|
| Equipment ID | `EQ-001` | Fleet asset number |
| Name / Type | `Dump Truck` | Vehicle description |
| Make & Model | `Caterpillar 777G` | Manufacturer and model number for insurance records |
| License Plate | `ABC-1234` | State license plate number for traffic and liability records |
| Status | Dropdown | See below |

A yellow `VEHICLE` badge appears at the bottom of each vehicle row for visual identification in the list.

**Equipment status options:**

| Status | Meaning |
|---|---|
| Active | Equipment operating normally during the shift |
| Idle | Equipment on site but not working — triggers idle time capture (see section 6.9) |
| Off Site | Equipment left the site and was not available during this shift |
| Breakdown | Equipment present but inoperable due to mechanical failure |

Rows can be removed with the red Remove button. All equipment data triggers auto-save on every change.

---

### 6.9 Idle Time Capture

When any equipment row's Status is set to **Idle**, an orange-highlighted sub-row expands automatically below that entry without any additional tap required. This sub-row captures:

| Field | Input | Purpose |
|---|---|---|
| Hours | Number (0–24) | Full hours the equipment was idle |
| Minutes | Number (0–59) | Additional minutes of idle time |
| Reason | Text | Plain-language cause of the idleness |

**Common idle reasons:**

- Waiting for inspection
- No material delivery
- Rain delay / weather hold
- Operator unavailable
- Waiting for surveyor
- Equipment breakdown of an interdependent unit

The idle time data flows directly into the Equipment Register section of the generated report. For the AI report path, Claude includes narrative commentary on idle time causes and their productivity impact. For the As-Filled path, idle hours, minutes, and reason are listed in the numbered equipment register.

This data directly supports rental billing dispute resolution, daily productivity analysis, schedule delay documentation, and insurance claim substantiation.

---

### 6.10 Labor Compliance Log

A daily record of every worker present on site during the shift. Required by Federal and State labor law for prevailing wage projects, OSHA record-keeping, union contract compliance, and general liability insurance audits.

**Adding workers:**

- **Add Worker** — adds a single blank row for manual entry
- **Bulk Add (paste list)** — opens the Bulk Entry modal for fast entry of large crews (see section 6.11)

**Worker row fields:**

| Field | Placeholder | Legal / Compliance Use |
|---|---|---|
| Legal Full Name | `First Last` | Must match government-issued ID; required for wage determination and audit |
| Role / Trade | `Carpenter, Electrician...` | Trade classification for prevailing wage rate determination |
| Company / Sub | `ABC Contractors` | Identifies the employing contractor for payroll audit purposes |

Each row has a red Remove button. Rows trigger auto-save on every keystroke.

The generated report's Labor Compliance Register presents all workers as a sequentially numbered, column-aligned table with a total worker count line at the bottom, suitable for direct inclusion in owner-required daily compliance submittals.

---

### 6.11 Bulk Labor Entry Modal

Opened by tapping **Bulk Add (paste list)**. Designed for fast crew entry when the crew is large, when the list is maintained in a separate document, or when copying from a prior day's roster.

**Input format:** Paste one worker per line, comma-separated values:

```
John Martinez, Ironworker, ABC Steel Co.
Maria Nguyen, Electrician, XYZ Electric
Wei Chen, Carpenter, General Contractor
David Kim, Operating Engineer
Sam Torres, Laborer, General Contractor
```

**Parsing rules:**

- First value before the first comma = Legal Full Name (required)
- Second value = Role / Trade (optional — left blank if omitted)
- Third value = Company / Sub (optional — left blank if omitted)
- Lines with no non-whitespace content are silently skipped
- All matching entries are added to the labor list simultaneously when **Add Workers** is tapped

**Tip for repeat projects:** Maintain a plain-text file with the full permanent crew roster. Each morning, copy it, add any new workers, remove anyone absent that day, paste into the modal, and submit. For a 30-person crew, this takes under 30 seconds.

---

### 6.12 Site Notes — Voice & Text Input

The notes panel is the primary free-form input area. It is the core content the AI transforms into formal report prose, and for As-Filled reports it is the verbatim record of the day's activities.

**The engineer does not need to write in complete sentences.** The AI report path accepts shorthand, abbreviations, incomplete thoughts, mixed language, technical codes, and rough fragments. The AI is explicitly instructed to interpret and formalise the content.

**Example input (deliberately rough):**

```
c1-c8 cols poured 40m3 C3 done noon. mixer broke 2hr delay morning.
lvl3 scaffold near-miss worker no harness corrected tbx talk given.
rebar delivery 3pm laydown B. DOT inspector Jones visit 2:30 all pass.
tmrw formwork lvl3 6am start crew 18
```

The AI converts this into a six-section formal report with complete sentences, technical terminology, and compliant language.

**Voice recording — real-time live transcription:**

Tap **🎙 Record Voice** to begin. The microphone activates and the words you speak appear in the notes text box **live as you talk** — no waiting, no post-processing step. The button pulses red with a "Recording… (tap to stop)" label while active.

How transcription works:
- Each sentence is processed incrementally as it's spoken
- Once a sentence is recognised as complete ("final"), it is committed to the text area, auto-capitalised, and punctuated
- In-progress words appear as a grey preview while the engine is still listening to the current phrase
- The engine automatically re-starts if it times out on mobile (handles the browser's default 60-second silence cutoff)

Tap the button again to stop recording. Everything spoken is already in the text field — the inspector can then type any corrections or additions before generating the report.

**Voice-only workflow:** Inspectors who prefer not to type at all can record their entire shift notes by voice, select their report type, and tap Generate. The transcript in the notes field is used exactly like typed notes — the AI formalises it or it is reproduced verbatim depending on which path is chosen.

**If Generate is tapped while still recording:** The recording is stopped cleanly, a short pause allows the final spoken words to be committed to the text area, and report generation proceeds automatically. No manual stop is required.

**Browser support for voice:**

| Browser / Platform | Voice Transcription |
|---|---|
| Chrome on Android | ✅ Full support — recommended for Android |
| Chrome on Desktop (Windows/Mac) | ✅ Full support |
| Safari on iPhone / iPad (iOS 14.1+) | ✅ Full support — recommended for iOS |
| Safari on macOS | ✅ Full support |
| Firefox (any platform) | ❌ Not supported — a clear message is shown directing the user to Chrome or Safari |
| Samsung Internet | ⚠ Partial — may work on newer versions |

On unsupported browsers, a clear alert explains which browsers to switch to rather than failing silently.

**What the engineer does not need:** An API key. An internet connection. Post-processing. The Web Speech API runs entirely on-device using the browser's built-in speech engine, at zero cost.

**Clear button:** Clears only the notes text area. Does not affect any other field or stop an active recording.

All changes to the notes area trigger auto-save after a 1.5-second debounce.

---

### 6.13 Multi-Language Input Support

Field crews on US construction projects frequently include workers and engineers for whom Spanish, Chinese (Mandarin), or Vietnamese is their primary language. The engineer can speak or write site notes in their preferred language and the system handles transcription and translation automatically.

**Language selection pills (above the notes text area):**

| Pill | Language | Speech Recognition Code | Notes Placeholder |
|---|---|---|---|
| 🇺🇸 English | English (default) | `en-US` | English construction example |
| 🇪🇸 Español | Spanish | `es-MX` | Spanish construction example |
| 🇨🇳 中文 | Chinese (Mandarin) | `zh-CN` | Chinese construction example |
| 🇻🇳 Tiếng Việt | Vietnamese | `vi-VN` | Vietnamese construction example |

**Critical:** Select the language pill **before** tapping Record Voice. The speech recognition engine is configured at start time — changing the pill mid-recording does not affect the current session.

**How multi-language works end to end:**

1. Inspector selects their language pill (e.g. 🇪🇸 Español)
2. Inspector taps **🎙 Record Voice** — the browser's speech engine switches to `es-MX` (Mexican Spanish)
3. Inspector speaks in Spanish — Spanish text appears live in the notes box
4. Inspector taps Generate and selects **AI Professional Report**
5. The AI prompt includes the instruction: *"The site notes below are written in Spanish. Translate to English and use in the report."*
6. The generated report is in formal English — ready to submit to the owner or DOT

**Language-specific notes:**

**Spanish (`es-MX`):** Works reliably across Chrome and Safari. Construction terms like *concreto, andamio, grúa, columna, losa* are recognised accurately. The `es-MX` locale (Mexico) is used rather than `es-ES` (Spain) as it best represents the dialect most common on US job sites. Engineers and crews from Central America will also get good results with this locale.

**Vietnamese (`vi-VN`):** Works in Chrome on Android and Safari on iPhone. Accuracy is best on devices with Vietnamese keyboard input installed, as this improves the local speech model. Technical construction terms borrowed from English (crane, pump, concrete) are generally transcribed in English within the Vietnamese text, which is normal.

**Chinese (`zh-CN`):** Works well in both Chrome and Safari for Mandarin speakers. The `zh-CN` locale targets Simplified Chinese / Mainland Mandarin. If your engineers primarily speak Cantonese, recognition accuracy will be lower — `zh-CN` is still usable but designed for Mandarin.

**As-Filled reports:** Translation does **not** apply. Notes are reproduced exactly as entered — in whatever language they were spoken or typed. The As-Filled report is for records that will be reviewed by someone who reads the same language.

**AI Professional reports:** The generated report is always in English, regardless of the input language.

The selected language is included in the auto-save draft and is restored with Load Saved Draft.

---

### 6.14 Quick-Start Hint Chips

Seven pill-shaped chips below the voice controls provide one-tap sentence starters for the most commonly reported site events. Each tap appends the starter text to the end of whatever is already in the notes field.

| Chip Label | Text Appended to Notes |
|---|---|
| `# Concrete pour` | `Poured concrete on ` |
| `# Safety` | `Safety incident: ` |
| `# Delay` | `Delay caused by ` |
| `# Inspection` | `Inspection by ` |
| `# Materials` | `Materials delivered: ` |
| `# RFI` | `RFI submitted for ` |
| `# Plan` | `Tomorrow we plan to ` |

Chips can be tapped multiple times to log multiple events of the same type. They never overwrite existing content. After tapping, the engineer completes the sentence by typing the specifics.

---

### 6.15 Report Section Toggles

Six toggle tiles sit between the notes panel and the photo upload section. They control which narrative sections appear in the generated report. All six are **active by default** (yellow border, checkbox filled).

| Section | Content Covered |
|---|---|
| Work Completed | Tasks performed, quantities installed, crew assignments, milestones reached |
| Safety & HSE | Incidents, near-misses, corrective actions taken, PPE compliance observations, toolbox talks given |
| Resources & Equipment | Labor deployed by trade, machinery utilisation, materials received or consumed |
| Delays & Issues | Schedule impacts, causes of delay, RFIs submitted, change order triggers |
| Quality & Inspections | Tests conducted, third-party inspector visits, non-conformances, sign-offs received |
| Plan for Tomorrow | Next shift schedule, daily targets, crew and equipment requirements |

Tapping any tile toggles it off — it turns grey, loses its border, and its checkbox empties. Tapping again re-activates it.

For the **AI report**, only active sections receive AI-generated prose. For the **As-Filled report**, the notes content is placed under the first active section, and all remaining active sections are marked `(See field notes above / Not separately reported)`. Inactive sections are omitted entirely from both report types.

**The following are always included regardless of toggle state:**

- Equipment Register
- Labor Compliance Register
- Photo Log (when photos have been uploaded)
- Signatures & Sign-Off block

---

### 6.16 Site Photos with AI Auto-Captioning

**Uploading photos:**

- **Tap the photo drop zone** — on mobile this opens the device camera directly using the rear-facing lens for immediate on-site capture; it also offers gallery / library access for uploading previously taken photos
- **Drag and drop** — on desktop, drag one or more image files from Explorer or Finder directly onto the drop zone
- **Multiple selection** — selecting multiple files from the gallery or file picker uploads them all in one action
- **Accepted formats:** JPEG, PNG, HEIC, WebP — any format supported by the browser's FileReader API

Photos are loaded as base64 strings held in browser session memory. They are never written to the device file system by the application.

**Photo cards:**

Each uploaded photo appears as a card in the grid below the upload zone.

| Card Element | Description |
|---|---|
| Thumbnail image | 130px tall crop, fills full card width |
| Caption text area | Editable free text; auto-filled when AI captioning runs |
| Category dropdown | For classification and labelling in the photo log |
| AI Caption button | Sends this individual photo to Claude Vision for automated captioning |
| Remove button | Permanently removes the photo from the session and photo log |
| AI badge | Orange badge that appears after a successful AI caption is applied |

**Photo categories:**

| Category | Intended Subject Matter |
|---|---|
| General | Miscellaneous site documentation not fitting another category |
| Progress | Completed work, milestones reached, overall site view |
| Safety | Active hazards, near-miss locations, PPE compliance, corrective actions |
| Quality | Inspection results, measurement verification, sample testing |
| Defect | Non-conforming work, damage, punch list items, rework required |
| Material | Delivered materials, storage conditions, batch tickets, product labels |
| Equipment | Equipment on site, operational status, breakdown condition |

**AI Auto-Captioning:**

Tapping **AI Caption** on any photo sends that photo to Claude's vision model as a base64 image with a prompt requesting a 1–2 sentence professional construction caption using technical site terminology.

Example AI-generated captions:

- *"Reinforced concrete columns C1 through C4 at Level 2 with formwork in place and vertical rebar tied, awaiting pour."*
- *"Scaffolding platform at Gridline E, Level 3 — guardrail and toe board installed per OSHA 1926.502."*
- *"High-strength bolt installation at structural steel splice connection, mid-span — impact wrench and torque verification tag applied."*
- *"Freshly placed concrete slab on Grade A, Grid 1–4, screeded and floating in progress, plastic shrinkage covers staged."*

**AI Caption All Photos** button appears as soon as the first photo is uploaded. It runs AI captioning on every photo in the session sequentially — recommended when uploading a batch of photos at end of shift.

AI captioning requires an API key and an active internet connection. Without them, captions can be typed manually into each card's text area. Photos still appear in the report with their manually entered captions.

---

### 6.17 Digital Signatures

Two signature panels are displayed side by side at the bottom of the form (stacked vertically on narrow mobile screens). Each captures the end-of-shift sign-off from one authorised party.

**Owner / Field Inspector panel (left):**

- Name text input for the inspector's full legal name
- Signature canvas — draw with finger, stylus, or mouse

**Contractor Superintendent panel (right):**

- Name text input for the superintendent's full legal name
- Signature canvas — draw with finger, stylus, or mouse

**Technical implementation for accurate mobile signature capture:**

The canvas uses the **Pointer Events API** (`pointerdown`, `pointermove`, `pointerup`, `pointercancel`, `pointerleave`) — the modern unified event standard that works for finger touch, passive stylus, and mouse cursor across all browsers and devices without separate code paths for each input type.

`setPointerCapture` is called on `pointerdown` so the stroke tracks correctly even when the finger briefly loses perfect contact with the screen surface during fast signature strokes.

The canvas is scaled by `window.devicePixelRatio` before drawing begins. On Retina and high-DPI screens — all iPhones and most modern Android devices — the physical pixel grid is 2× or 3× denser than the CSS pixel grid. Without DPR scaling, lines render blurry. With it, lines are crisp at full physical pixel resolution.

`touchstart` and `touchmove` events are intercepted with `{passive: false}` and `preventDefault()` to prevent the page from scrolling while the finger is drawing on the canvas.

The **Clear** button below each canvas performs a full canvas reset, re-applies the DPR scale, and resets the stroke style correctly so subsequent re-signing is as sharp as the first.

**Status text** below the Clear button shows `Not signed` (grey) until any drawing occurs, then switches to `Signed` (green).

**Where signature data goes:**

- **On-screen report preview:** Both signature images appear as `<img>` elements in the report's signature panel
- **HTML file download:** Both signatures are embedded as base64 PNG data directly inside the HTML file — fully self-contained, no external references
- **Email plain-text body:** A note reads `[Digital signatures captured — see HTML attachment]`

---

### 6.18 Generate Report — Two-Path Choice Modal

Tapping **Generate Full Report** opens a modal dialog presenting two clearly distinct report generation options. The same modal also opens when tapping **Regenerate** in the report output panel.

```
┌──────────────────────────────────────────────────────────────┐
│  Generate Report                                             │
│  Choose how to generate your daily report.                   │
│  Both options will email the report to your address.         │
│                                                              │
│  ┌────────────────────┐    ┌──────────────────────────────┐  │
│  │  📋                 │    │  ⚡          [AI POWERED]    │  │
│  │  As-Filled Report   │    │  AI Professional Report     │  │
│  │                     │    │                             │  │
│  │  Compiles all your  │    │  Claude AI rewrites your    │  │
│  │  entries exactly    │    │  rough notes into formal    │  │
│  │  as entered into a  │    │  construction language      │  │
│  │  structured report  │    │  with full narrative        │  │
│  │                     │    │  sections                   │  │
│  │ ✅ No API key       │    │ ⚡ Requires API key          │  │
│  │ ✅ Works offline    │    │ ⚡ Requires internet         │  │
│  │ ✅ Instant          │    │ ⚡ ~10 seconds               │  │
│  └────────────────────┘    └──────────────────────────────┘  │
│                                                              │
│                     Cancel — go back                         │
└──────────────────────────────────────────────────────────────┘
```

- Tapping either card immediately closes the modal and begins that report generation path
- Tapping **Cancel — go back** dismisses the modal without generating anything
- Both paths automatically trigger email delivery upon completion

This modal was introduced to solve the problem where the original single-button approach silently did nothing when no API key was present, leaving inspectors unable to generate any report. Now every inspector can generate a complete daily report regardless of API key or internet availability.

---

### 6.19 As-Filled Report (No AI, No Internet Required)

The As-Filled report compiles all entered data directly into a structured document using only JavaScript running in the browser. It produces output instantly, requires no API key, and works fully offline.

**Complete structure of the generated report:**

**Header block:**

```
CONSTRUCTION DAILY REPORT
====================================================
Project:  I-80 Bridge Deck - Span 4
Date:     2026-02-26     Shift: Day
Engineer: James R. Chen
GPS:      37.812456, -121.654321  (+/-8m)
Workers:  24   Progress: 42%
Weather:  Sunny   Wind: 14 mph   Temp: 72°F
====================================================
```

**Enabled section handling:**

The full text of the site notes field is placed verbatim under the first enabled section. All remaining enabled sections receive the placeholder `(See field notes above / Not separately reported)`. If no sections are enabled, notes are placed under a `FIELD NOTES` heading.

**Equipment Register:**

All logged equipment presented in a numbered list. Each entry shows Equipment ID, Name / Type, and Status. Vehicles include Make/Model and License Plate. Equipment with Idle status includes hours, minutes, and reason.

**Labor Compliance Register:**

All logged workers presented in a column-aligned table with sequential numbering, with a total worker count line at the bottom. Column headers: `# / Legal Full Name / Role / Trade / Company`.

**Photo Log:**

Each uploaded photo listed with sequential number, category tag in brackets, and caption text.

**Signatures & Sign-Off block:**

Inspector name, date, and note `[See digital signature — HTML attachment]`. Superintendent name, date, and same note.

**Footer:**

`Report generated by SiteLog AI · [full timestamp]`

---

### 6.20 AI-Generated Professional Report

The AI report path sends all form data to the Claude Sonnet model and receives fully formed construction prose in return.

**What the AI prompt contains:**

- Full project header: project name, date, shift, engineer name, GPS coordinates, workers, progress
- Weather condition, wind speed with direction, temperature
- Complete equipment register with all fields and idle times
- Complete labor register with all fields
- The list of enabled report sections
- The full site notes field content
- If a non-English language is selected: explicit instruction to detect the input language and translate before writing

**What Claude produces:**

- Formal narrative paragraphs for each enabled section, written in professional construction industry English
- An Equipment Register section with structured entries and prose commentary on equipment utilisation
- A Labor Compliance Register in formatted tabular form
- A sign-off block

The header block is prepended by the application code — not by the AI — so the report header format is identical between both report types.

**Language handling:** When Spanish, Chinese, or Vietnamese is selected, the prompt includes: *"IMPORTANT: The site notes below are written in [Language]. Translate to English and use in the report."* The generated output is always English regardless of input language.

**If no API key is configured:** The tool does not silently fail. It scrolls to the Configuration panel, highlights the API key warning banner, and displays a status message directing the engineer to add a key or choose As-Filled Report instead.

**If the device is offline:** The report data is serialised and queued in `localStorage` for automatic processing when internet is restored — see section 6.25.

---

### 6.21 Report Output Panel

After generation completes, the report output panel animates into view below the signatures section. It persists on screen until a new report is generated.

**Report action bar (top of the panel):**

| Button | What It Does |
|---|---|
| **Regenerate** | Re-opens the two-path choice modal to generate a new version of the report |
| **Copy Text** | Copies the plain-text report body to the system clipboard; the button label changes to `Copied!` for 2 seconds |
| **Download** | Builds and downloads the full self-contained HTML report file with all photos and signature images embedded as base64 |
| **Send Email** | Runs the complete email sequence: cleans text → builds HTML file → downloads HTML file → opens mail client (see section 6.22) |

**Report body (on-screen):**

The monospaced plain text report with section headers and horizontal dividers. Scrollable. Rendered exactly as it will appear in the email body.

**Photo thumbnail grid (below the text body):**

All uploaded photos displayed in a responsive grid with each photo's category label and caption. This is the visual preview of the photo log section.

**Signature panels (below the photo grid):**

Side-by-side panels showing each signer's label, name, and drawn signature image. Shows a dashed "Not signed" box if the canvas was not used.

---

### 6.22 Email Delivery — How It Actually Works

**The fundamental constraint of browser-based email:**

Browser applications cannot send email directly. They have no access to SMTP servers, mail credentials, or email APIs without a backend. SiteLog AI uses the `mailto:` URI scheme, which passes control to the device's native mail application (Mail on iPhone, Gmail or Outlook on Android, Outlook or Mail on desktop). The `mailto:` link pre-fills the To address, Subject line, and email body text — but the engineer must tap Send in their mail app.

**Why photos and signatures cannot appear directly in the email body:**

A `mailto:` URL body is limited to approximately 2,000 characters of plain text. A single mobile photo compressed to JPEG is typically 1–4 MB of data, which as a base64 string is 1.3–5 million characters — thousands of times the limit. Signatures are smaller but are PNG images that still cannot be inlined in plain text. The solution is a separate self-contained HTML file that embeds all binary data, which downloads automatically and is then attached to the email by the engineer in their mail client.

**Why extra symbols appeared in older versions and how they are fixed:**

The raw report text contains Unicode box-drawing characters (`═`, `─`) used as visual dividers on screen, and `##` markdown-style section headers. Many email clients render these as `?` symbols or garbled text. The `cleanForEmail()` function now processes the entire report text before building the `mailto:` URL:

- Strips `##` prefixes from section headers, keeping only the label text
- Replaces runs of four or more `═` or `─` characters with plain `----` ASCII dashed lines
- Maps remaining Unicode box-drawing block characters (U+2500–U+257F, U+2550, U+2551) to `-` or `=`
- Collapses three or more consecutive blank lines to a maximum of two
- Leaves all other content — accented letters, punctuation, numbers, report text — completely unchanged

**Complete sequence every time a report is generated or Send Email is tapped:**

**Step 1 — Text cleaning:** `cleanForEmail()` converts the raw report to clean plain ASCII.

**Step 2 — Attachment notes appended:** If photos were uploaded, the body text gets: `[N site photo(s) included — see HTML attachment]`. If signatures were captured: `[Digital signatures captured — see HTML attachment]`. If either is true, a visible instruction block is appended telling the engineer to attach the downloaded file.

**Step 3 — HTML report built and downloaded:** `buildHTMLReport()` assembles a complete styled HTML document with inline base64 photos and signatures. `downloadHTMLReport()` triggers a browser download of `SiteReport_[Project]_[Date].html` to the device's Downloads folder.

**Step 4 — Mail client opened:** `window.open(mailto:...)` opens the native mail app with To, Subject, and Body pre-filled. The body is capped at 1,950 characters with `[Report continues in HTML attachment]` appended if needed.

**Step 5 — Engineer attaches and sends:** In the mail app, tap the attachment button, navigate to Downloads, select the HTML file, and tap Send.

**What the recipient receives:**

- A clean, readable plain-text email body with the full report summary, displaying correctly in any email client
- An HTML file attachment that opens in any browser and shows the complete formatted report with all site photos at full resolution and both digital signature images

---

### 6.23 HTML Report File — Embedded Photos & Signatures

The downloaded HTML file is a fully self-contained document. It requires no internet connection to open or display — all data is embedded inline.

**HTML file structure:**

The file contains a styled header block with all project metadata (project name, date, engineer, GPS, weather, wind, temperature), followed by the full formatted report body with section headings styled in gold/amber and body text as HTML paragraphs, followed by a responsive photo grid with every photo embedded as an inline base64 `<img>` tag showing the category label and caption beneath each image, followed by a two-column signature panel embedding both signature images with the signer names and sign-off date.

**Key properties of the HTML file:**

- Opens in any browser on any device — Windows, Mac, iOS, Android — with no additional software
- All images load instantly — no network requests are made when opening the file
- Can be archived permanently as the official daily report record
- Can be printed directly from the browser using File → Print for a paper copy
- File size varies by number and resolution of photos — typically 2–20 MB for a shift with 5–15 photos

The **Download** button in the report output panel produces this same HTML file on demand.

---

### 6.24 Auto-Save & Draft System

SiteLog AI continuously saves all entered data to `localStorage` so that no work is lost if the browser closes, the phone locks, or the page is accidentally navigated away from.

**Auto-save trigger:**

Every input event on any field in the form triggers the auto-save debounce timer. After 1.5 seconds of inactivity following the last change, `saveDraft()` serialises the entire form state to `localStorage['sitelog_draft']` as a JSON object.

**What is saved in the draft:**

| Data Type | Saved | Notes |
|---|---|---|
| Project info (all 6 fields) | Yes | Full text/values |
| Weather condition selection | Yes | String value |
| Wind speed and temperature | Yes | Numeric values |
| GPS coordinates | Yes | lat/lng/accuracy object |
| Equipment list | Yes | Full array with all fields, vehicle data, idle times |
| Labor list | Yes | Full array with all fields |
| Site notes text | Yes | Full text content |
| Input language selection | Yes | Language code string |
| Inspector name | Yes | Text field value |
| Superintendent name | Yes | Text field value |
| Photos | No | Session memory only — too large for localStorage |
| Drawn signatures | No | Session memory only — canvas data not serialised |
| Report output | No | Re-generated on each report action |

**Auto-save status** (Configuration panel): The green dot and timestamp update immediately after every successful save, giving the engineer visual confirmation that their data is protected.

**Draft persistence:** The draft survives browser restarts, phone reboots, and clearing of session storage. It is only removed by the **Clear Draft** button or by manually clearing `localStorage` through browser settings.

---

### 6.25 Offline Mode & AI Report Queue

SiteLog AI is designed for job sites with intermittent or no internet connectivity — remote locations, tunnels, underground work, mountainous terrain, and areas with poor cell coverage.

**What works without any internet:**

- All data entry: project info, equipment, labor, notes, language selection
- GPS (satellite-based — no internet required once the OS has a location fix)
- All form auto-save operations
- Photo upload and manual captioning
- Signature drawing
- As-Filled report generation
- As-Filled report HTML file download
- Draft load and restore

**What requires internet:**

- AI Professional Report generation (Anthropic API)
- AI photo captioning (Anthropic API)
- Weather/wind/temperature auto-fetch (Open-Meteo API)
- Email delivery via mail client

**Offline AI report queue:**

If the engineer selects **AI Professional Report** while the device is offline:

1. `buildPrompt()` serialises all current form data into the full AI prompt string
2. An entry containing the timestamp, prompt, email address, project name, and date is added to `offlineQueue`
3. The queue is persisted to `localStorage['sitelog_queue']`
4. The queue badge counter updates in the offline banner
5. A status message confirms the report is queued and will auto-process on reconnection

**Automatic queue processing on reconnection:**

The application listens for `window.addEventListener('online', ...)`. The moment the device detects network connectivity:

1. `processQueue()` runs automatically without any engineer action required
2. For each queued entry, the AI is called with the serialised prompt
3. On success, the mail client opens with the generated report
4. The processed entry is removed from the queue and `localStorage` is updated
5. The badge counter updates to reflect remaining items

If an API call fails for a queued entry, the entry remains in the queue for the next connectivity window.

---

## 7. Recommended End-of-Shift Workflow

| Step | Action | Time |
|---|---|---|
| 1 | Open the page — GPS acquires automatically; tap **Allow** if the location prompt appears | 30 sec |
| 2 | Tap **Auto-fetch** for live wind speed and temperature | 10 sec |
| 3 | Tap the correct weather condition chip | 5 sec |
| 4 | Review equipment rows — verify statuses; set any to **Idle** and log idle hours and reason | 2–3 min |
| 5 | Review labor rows — add any new workers, remove anyone absent today | 1–2 min |
| 6 | Tap the photo zone and photograph key activities, completed work, safety items, deliveries | 2–5 min |
| 7 | Tap **AI Caption All** — all photos captioned in approximately 30 seconds | 30 sec |
| 8 | Select language pill if not English, then tap **🎙 Record Voice** and speak the day's events — text appears live. Or type notes directly. Tap record button again to stop. | 1–3 min |
| 9 | Inspector draws signature; Superintendent draws signature | 30 sec each |
| 10 | Tap **Generate Full Report** and choose report type | 5 sec |
| 11 | HTML file downloads; mail client opens with pre-filled email | Instant / ~10 sec |
| 12 | Attach `SiteReport_*.html` file to the email in the mail app and tap Send | 30 sec |
| **Total** | | **8–15 minutes** |

---

## 8. Choosing Between the Two Report Types

| Factor | As-Filled Report | AI Professional Report |
|---|---|---|
| Internet required | No | Yes |
| API key required | No | Yes |
| Generation time | Instant (< 1 second) | ~10 seconds |
| Works fully offline | Yes | No (queued if offline) |
| Site notes in output | Verbatim — exactly as typed | Rewritten in formal professional prose |
| Section narrative quality | Direct reproduction of notes | Full formal paragraph per section |
| Language translation | No — notes reproduced as-is | Yes — translates to English |
| Equipment register | Numbered list with all fields | Structured entries with prose commentary |
| Labor register | Formatted numbered table | Formatted numbered table |
| Photos in output | Yes — in HTML file | Yes — in HTML file |
| Signatures in output | Yes — in HTML file | Yes — in HTML file |
| Email delivery | Automatic on generation | Automatic on generation |
| Offline generation | Yes | Queued (generates when online) |
| Cost | Free | Approx. $0.01–$0.11 per report |

**Choose As-Filled when:** notes are already written clearly, the engineer prefers not to use AI, the device has no internet, no API key is available, or speed is more important than formal prose style.

**Choose AI Professional when:** notes are rough or abbreviated, notes are in Spanish/Chinese/Vietnamese, the report is going to a DOT inspector or owner's representative who expects formal language, a complete narrative paragraph is needed for every section, or consistent tone and terminology across all daily reports is required.

---

## 9. Email System — Step-by-Step Explanation

This section explains the email system in detail because it involves an HTML file download step that can be unexpected on first use.

**Why there is a download step:**

A `mailto:` URL body can carry approximately 2,000 characters of plain text. A typical mobile site photo is 1–4 MB — as base64 text, that is 1.3 million to 5.3 million characters per photo. A 10-photo report would require 13–53 million characters, which is entirely impossible to transmit via a `mailto:` URL. Signature images face the same constraint. The solution is to generate a self-contained HTML file that embeds all binary data as inline base64, download it to the device, and have the engineer attach it to the email in their mail client.

**Complete sequence when Send Email is tapped:**

1. `cleanForEmail()` converts the raw report text to clean plain ASCII suitable for all email clients — removing `##` markers, replacing Unicode box-drawing characters with plain dashes, and collapsing excess blank lines

2. Photo count and signature capture notes are appended to the body text, along with a visible instruction block directing the engineer to attach the downloaded file

3. `buildHTMLReport()` assembles a complete styled HTML document with all project data, the formatted report body, all photos as inline base64 images, and both signature images

4. `downloadHTMLReport()` creates a Blob URL and triggers a browser download — the file `SiteReport_[Project]_[Date].html` saves to the device's Downloads folder automatically

5. `window.open(mailto:...)` opens the native mail app with the To, Subject, and Body fields pre-filled

6. A status message shows: `Email client opened · HTML report downloaded — attach the file to your email`

**Engineer's final action:** In the mail app, tap the attachment icon → navigate to Downloads → select the HTML file → tap Send.

**What the email recipient sees:**

- A clean, formatted plain-text email body with the complete report summary, readable in any email client without opening any attachments
- An attached HTML file — when opened in any browser, it displays the full formatted report with all site photos at full resolution and both digital signatures visible

---

## 10. Installing as a Home Screen App (PWA)

Installing to the home screen makes SiteLog AI launch in full-screen standalone mode without any browser address bar or navigation chrome — identical in appearance to a native app. The page also loads faster from the home screen because the browser caches the entire HTML file after the first online load.

### iPhone / iPad (Safari only)

1. Open the page URL in **Safari** — must be Safari; iOS Chrome does not support home screen PWA installation
2. Tap the **Share button** (box with upward arrow) at the bottom of the screen
3. Scroll the share sheet down and tap **Add to Home Screen**
4. Accept the default name `SiteLog AI` or type a custom name
5. Tap **Add** in the top-right corner

### Android (Chrome)

1. Open the page URL in **Chrome**
2. Tap the three-dot menu in the top-right corner
3. Tap **Add to Home Screen**
4. Tap **Add** in the confirmation dialog

### After Installation

- The SiteLog AI icon appears on the home screen alongside native app icons
- Tapping it launches the app in full-screen standalone mode with no browser chrome
- After the first successful online load, the HTML file is cached — the app loads instantly even without any internet connection
- All `localStorage` data — config, drafts, queue — persists normally across home screen launches

---

## 11. Mobile Tips & Best Practices

| Situation | Recommended Action |
|---|---|
| GPS badge is orange | Tap the GPS badge and allow location permission when prompted — see Troubleshooting section 15 for denied permission recovery |
| **Wearing gloves on site** | Tap 🎙 Record Voice and dictate notes — words appear live. Select language pill first. Use Chrome on Android or Safari on iPhone |
| Large crew entry | Use Bulk Add — paste from a note or spreadsheet; 30 workers entered in under 30 seconds |
| Photographing defects | Tap AI Caption — the model identifies non-conformances and construction defects with technical precision |
| Working at a remote site with no signal | Fill the entire report offline; choose As-Filled Report for instant output; choose AI Report to queue it for auto-processing when back in range |
| Phone screen locks mid-report | No data is lost — auto-save runs every 1.5 seconds; tap Load Saved Draft on the next session |
| Returning at the start of a new shift | Tap Load Saved Draft — entire equipment list and crew list carry forward; update statuses and make today's changes |
| Signing on a small phone screen | Use landscape orientation for a wider canvas; draw slowly for the first stroke |
| Email client does not open automatically | Ensure a default mail account is set up in phone Settings — see Troubleshooting section 15 |
| Report has many high-resolution photos | The HTML file may be 10–20 MB; allow a moment for the mail client to load the attachment before sending |

---

## 12. Multi-Inspector Use

**Current architecture:** SiteLog AI is a single-device, single-session tool. One engineer produces one report per shift from one device. `localStorage` is device-specific — there is no synchronisation between devices.

**For projects with multiple field inspectors working in different areas simultaneously:**

Each inspector runs SiteLog AI independently on their own device and generates a separate report covering their scope of work. The project manager receives multiple daily emails and consolidates information manually or files the reports separately by area.

**For true real-time multi-user reporting** — where multiple inspectors simultaneously contribute different sections to a single shared daily report — a backend server component would be required. This would enable each inspector to submit their section from their own device in real time, a project supervisor to view all active submissions on a consolidated dashboard, automatic merging of all sections into a single master daily report, and role-based access control for inspectors, superintendents, and project managers. A suitable backend for this would be Firebase Realtime Database, Supabase, or a custom REST API. This is a potential future enhancement outside the scope of the current single-file design.

---

## 13. API Key Setup & Cost Estimate

### Getting an Anthropic API Key

1. Go to [console.anthropic.com](https://console.anthropic.com)
2. Sign in or create an account — no credit card required for account creation
3. Click **API Keys** in the left sidebar
4. Click **Create Key**, enter a descriptive name such as `SiteLog Field`, and click **Create Key**
5. Copy the full key value immediately — it is shown only once
6. In SiteLog AI, paste it into the **Anthropic API Key** field in the Configuration panel and click **Save Config**

The key is stored in `localStorage` on the device. It is never displayed again after saving. To update it, paste a new key into the field and save again.

### Token Usage and Cost Per Operation

| Operation | Approx. Input Tokens | Approx. Output Tokens | Approx. Cost (USD) |
|---|---|---|---|
| AI Report Generation | 800–1,500 | 1,000–2,000 | $0.01–$0.03 |
| Single Photo Caption | 500–800 | 40–80 | $0.003–$0.008 |
| 10 Photo Captions (batch) | ~6,000 | ~600 | $0.03–$0.08 |
| Typical full daily report + 10 AI photos | ~7,500 | ~2,600 | **$0.04–$0.11** |

At one AI report per working day, five days per week, fifty weeks per year, the annual cost per engineer is approximately **$10–$28 USD** at current Claude Sonnet pricing. Check [anthropic.com/pricing](https://www.anthropic.com/pricing) for current rates before estimating project costs.

---

## 14. Privacy & Data Storage

| Data | Where It Is Stored | Who Can Access It |
|---|---|---|
| Anthropic API Key | Device `localStorage` only | Device owner only |
| Email address | Device `localStorage` only | Device owner only |
| Draft data (all form fields) | Device `localStorage` only | Device owner only |
| Offline AI report queue | Device `localStorage` only | Device owner only |
| Site photos | Browser session memory (RAM) only | Not persisted after page close |
| GPS coordinates | Session memory + `localStorage` draft | Device owner only |
| Drawn signatures | Browser session memory (RAM) only | Not persisted after page close |
| Generated HTML report file | Device Downloads folder | Engineer + anyone they share it with |
| AI prompts sent for report generation | Anthropic API (processing only) | Anthropic per their privacy policy |
| Photos sent for AI captioning | Anthropic API (processing only) | Anthropic per their privacy policy |

**There is no application backend, no database, no analytics, and no third-party tracking in SiteLog AI.** The only external services contacted are:

1. **Anthropic Messages API** — only when AI report generation or photo captioning is explicitly triggered
2. **Open-Meteo weather API** — only when the Auto-fetch button is tapped
3. **Google Fonts CDN** — on every page load for typography

Anthropic does not use API inputs to train its models by default. Review [anthropic.com/privacy](https://www.anthropic.com/privacy) for your organisation's data protection and compliance requirements before deploying to projects with sensitive or confidential project information.

---

## 15. Troubleshooting

### GPS shows orange / "Location denied" on iPhone

The page must be served over HTTPS — iOS Safari blocks geolocation on HTTP pages. When the location permission prompt appears on first load, tap **Allow**. If it was previously denied: open iPhone **Settings → Privacy & Security → Location Services → Safari → While Using the App**, then return to SiteLog AI and tap the GPS badge to request a fresh fix.

### Wind and Temperature auto-fetch shows an error

GPS must be locked first — the weather API requires coordinates to identify the site. Wait for the GPS badge to show a successful fix before tapping Auto-fetch. Also confirm the ONLINE badge is green. If both GPS and internet are confirmed available but the fetch still fails, the Open-Meteo API may be temporarily unavailable — enter both values manually.

### Equipment buttons (Add Equipment, Add Vehicle) do nothing

Ensure the button is fully visible on screen and not obscured by the on-screen keyboard. Scroll the page slightly and tap again. If the problem persists, hard-refresh the page (hold Shift and reload on desktop; close the tab and reopen on mobile) — all data is protected in the auto-save draft; tap **Load Saved Draft** to restore everything immediately.

### Worker button (Add Worker) does nothing

Same cause and resolution as the equipment buttons above.

### Voice recording does nothing / button has no effect

The most common cause is using a browser that does not support the Web Speech API. Firefox does not support it on any platform. Switch to Chrome (Android or desktop) or Safari (iPhone/iPad iOS 14.1+). A clear alert message is shown if the browser is unsupported.

### Voice recording starts but nothing appears in the text box

The microphone permission may have been denied. Check the browser's address bar for a microphone icon with a blocked indicator. Tap it and set microphone access to **Allow**, then reload the page and try again.

On iPhone: **Settings → Privacy & Security → Microphone → Safari → Allow**.  
On Android: **Settings → Apps → Chrome → Permissions → Microphone → Allow**.

### Voice recognition is inaccurate or keeps stopping

On mobile browsers, the speech recognition engine has a default timeout after approximately 5–10 seconds of silence. SiteLog AI handles this by automatically restarting the recognition engine when it stops — you do not need to tap the button again. Just keep speaking.

For best accuracy: speak clearly at a normal pace, hold the phone 20–30cm from your face, and minimise background noise (engine sounds, wind, radio). Construction site environments are noisy — if accuracy is poor, type notes instead or move to a quieter area.

### Voice transcription works but words are in the wrong language

Select the correct language pill **before** tapping Record Voice. The speech engine is set to the selected language at the moment recording starts — changing the pill while recording is active does not affect the current session. Stop recording, select the correct pill, and start a new recording.

### Speech recognition says "not-allowed" or "service-not-allowed" error

This is a microphone permission error. On some Android devices, the browser may need microphone permission both at the OS level and within the browser app settings. Check both. On iPhones, if Screen Time restrictions are enabled, they may block microphone access in Safari — check **Settings → Screen Time → Content & Privacy Restrictions → Microphone**.

### Signature canvas has no effect when drawing on mobile

Use a single finger only — the canvas does not support multi-touch drawing. The page will not scroll while your finger is on the dark rectangular canvas area. Draw slowly and deliberately for the first stroke. If strokes appear in the wrong position relative to where you are drawing, rotate the phone to landscape orientation and back to portrait to trigger a canvas resize and DPR recalibration, then try again.

### AI report generation returns an error

Confirm the API key field placeholder shows `API key saved`. If not, re-enter and save the key. Check the account has available credits at [console.anthropic.com](https://console.anthropic.com) in the Usage section. Confirm the ONLINE badge is green. An authentication error in the status bar means the key is invalid or has been revoked — generate a new key from the console.

### Email client does not open when generating the report

A default email account must be configured and active on the device. On iPhone: **Settings → Mail → Accounts → Add Account**. On Android: **Settings → Accounts → Add Account → Email**. If using a third-party mail app (Gmail, Outlook) as the default, ensure it is set as the default mail handler in the phone's settings.

### The email body has garbled symbols or question marks

This issue is resolved in the current version. The `cleanForEmail()` function converts all Unicode box-drawing characters and `##` markers to plain ASCII before building the `mailto:` URL. If symbols still appear, confirm you are using the latest version of the HTML file by performing a hard refresh or clearing the browser cache for the site.

### Photos are not visible in the email

This is by design — not a bug. Photos are binary image data that cannot fit in a `mailto:` URL body. The HTML file that downloads automatically when you tap Send Email contains all photos embedded at full resolution. In your mail app, tap the attachment button, navigate to Downloads, select `SiteReport_*.html`, and attach it to the email before sending. The recipient opens the file in any browser to see all photos.

### Signatures are not visible in the email body

Same as photos — signature images are embedded in the HTML attachment, not in the plain-text email body. Attach the downloaded HTML file to the email in your mail client.

### The HTML file does not appear in Downloads after sending

On iPhone, files are in **Files → On My iPhone → Downloads** or in iCloud Drive → Downloads. On Android, files are in the **Files** app or **Downloads** folder. On desktop, files appear in the browser's standard Downloads location. If the download did not trigger, tap **Download** in the report output panel to manually trigger a fresh download.

### Load Saved Draft does not restore my photos or signatures

Photos and drawn signatures are session-only data held in browser memory. They are intentionally not stored in `localStorage` because photos at full mobile resolution can be 30–80 MB for a typical session — far exceeding localStorage capacity. Re-upload photos and re-draw signatures at the start of each session. All text data, equipment, labor, notes, and project info are fully restored.

### Page does not load offline

Install the app to your home screen (see section 10). The browser caches the HTML file after the first successful online load. Without home screen installation, mobile browsers may not cache the page reliably for consistent offline access.

---

## 16. Technology Stack

| Component | Technology | Detail |
|---|---|---|
| **UI** | Vanilla HTML5 / CSS3 / ES6 JavaScript | Zero external frameworks; zero build tools; zero npm dependencies |
| **Fonts** | Google Fonts CDN | Bebas Neue (headings/labels), DM Sans (body text), DM Mono (report output) |
| **AI model** | Claude Sonnet (`claude-sonnet-4-20250514`) | Anthropic Messages API, version `2023-06-01` |
| **Vision (photo captions)** | Claude Sonnet vision input | Same model; photos passed as base64 content blocks |
| **Weather API** | Open-Meteo | Free, no API key required; returns current wind speed, wind direction, and temperature |
| **GPS** | Browser Geolocation API | `navigator.geolocation.getCurrentPosition()` with `enableHighAccuracy: true` |
| **Signatures** | HTML5 Canvas + Pointer Events API | DPR-scaled canvas; `setPointerCapture` for accurate stroke tracking on mobile |
| **Local storage** | `localStorage` | Config key `sitelog_config`, draft key `sitelog_draft`, queue key `sitelog_queue` |
| **Photos** | FileReader API | Base64 data URIs; held in session memory only |
| **Voice** | Web Speech API (`SpeechRecognition` / `webkitSpeechRecognition`) | Real-time on-device transcription; no API key or internet required; `continuous: true` with auto-restart; language codes: `en-US`, `es-MX`, `zh-CN`, `vi-VN` |
| **Email** | `mailto:` URI scheme | Passes to device native mail client; body cleaned by `cleanForEmail()` |
| **HTML report** | Blob URL + `<a download>` attribute | Self-contained file; all photos and signatures embedded as inline base64 |
| **Email body cleaning** | `cleanForEmail()` | Strips Unicode box-drawing chars (U+2500–U+257F, U+2550, U+2551), removes `##` markers, collapses blank lines |
| **PWA** | Inline `data:` URI manifest | Enables Add to Home Screen on iOS Safari and Android Chrome |
| **Hosting** | Any HTTPS static file host | GitHub Pages, Netlify, Vercel, AWS S3 + CloudFront |

---

## 17. Version History

| Version | What Changed |
|---|---|
| **v4.2** | **Voice transcription completely rebuilt** — replaced MediaRecorder (audio blob capture with no transcription) with the browser's built-in **Web Speech API** (`SpeechRecognition` / `webkitSpeechRecognition`). Words now appear live in the notes text box as the inspector speaks — real-time, on-device, zero cost, no API key required. `continuous: true` keeps the session open until the inspector taps Stop. Auto-restart on `onend` handles mobile browser silence timeouts transparently. Each committed sentence is auto-capitalised and punctuated. **Voice-only workflow enabled** — the hard "notes required" block in `generateAIReport()` is removed; inspectors who record by voice only can tap Generate immediately. If Generate is tapped while recording is still active, the recording stops cleanly, a 400ms pause lets the final words commit, and generation proceeds automatically. **Multi-language voice** — language pills now set the `SpeechRecognition.lang` property directly (`en-US`, `es-MX`, `zh-CN`, `vi-VN`) so transcription is done in the correct language on-device. Spanish and Vietnamese transcription work in Chrome and Safari without any server round-trip. **Unsupported browser handling** — Firefox and other non-supporting browsers receive a clear alert naming the supported browsers instead of a silent failure. |
| **v4.1** | **Email body symbols fixed** — `cleanForEmail()` strips all Unicode box-drawing characters (U+2500–U+257F, U+2550, U+2551) and `##` markdown markers from the plain-text email body so it renders cleanly in all email clients without garbled symbols or question marks. **Photos in email** — `buildHTMLReport()` generates a fully styled self-contained HTML document with all photos embedded as inline base64 `<img>` tags at full resolution. **Signatures in email** — both signature canvas images are embedded as base64 PNG data in the HTML file. **Auto-download on every send or download action** — `downloadHTMLReport()` triggers an automatic browser download of the self-contained HTML file every time Send Email or Download is tapped. **Download button updated** — `downloadReport()` now produces the rich HTML report with embedded photos and signatures instead of a plain `.txt` file. Both report generation paths (As-Filled and AI) automatically trigger the complete email sequence immediately on generation. |
| **v4.0** | **Two-path report generation modal** — Generate Full Report now opens a choice modal with two clearly described options. **As-Filled Report path** — `generatePlainReport()` assembles a complete structured report from all form data instantly with no AI dependency, including numbered equipment register, column-aligned labor compliance table, photo log, and sign-off block with footer timestamp. **AI path** — `generateAIReport()` shows a specific guidance message and scrolls to Configuration when no API key is present instead of silently failing. Both paths automatically trigger email delivery on completion. Regenerate button also opens the choice modal. |
| **v3.1** | **Mobile bug fixes** — Equipment and labor button functions given type-safe parameter guards to prevent silent JavaScript failures on mobile browsers. Init code moved to `DOMContentLoaded` event listener for iOS Safari timing compatibility. GPS function given specific per-error-code messages and orange badge state with retry UX. Signature canvas rewritten to use Pointer Events API with `setPointerCapture` for reliable stroke tracking. Canvas DPR scaling added for crisp rendering on Retina and high-DPI screens. `fetchWind()` updated to Open-Meteo v1 `current=` parameter format to correctly return and auto-populate both wind speed and temperature. |
| **v3.0** | Equipment log with idle time capture and vehicle-specific fields. Labor compliance log with bulk paste entry modal. Multi-language input support — Spanish, Chinese, Vietnamese — with AI translation. Offline AI report queue with automatic processing on reconnection. GPS auto-capture with specific error code messages. Wind speed and temperature auto-fetch from Open-Meteo. Dual digital signature canvases. Email delivery via mailto. |
| **v2.0** | Site photo upload with drag-and-drop and mobile camera capture. AI auto-captioning per photo and batch captioning. Photo category tags. Photo log section in report output with thumbnail grid. |
| **v1.0** | Initial release — AI report generation from rough field notes, weather condition chip selector, voice recording, section toggles, copy to clipboard, plain-text download. |

---

*SiteLog AI · Built for the field. Designed for the office.*  
*Single HTML file · No installation · No backend · Works offline · Mobile-first*
