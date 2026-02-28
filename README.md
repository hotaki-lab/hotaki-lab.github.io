# SiteLog AI — Construction Daily Report

**A mobile-first, AI-assisted daily site report tool for field engineers, inspectors, and superintendents.**  
No installation. No app store. No backend server. A single HTML file that runs on any phone or desktop browser.

---

## Table of Contents

1. [What Is SiteLog AI?](#1-what-is-sitelog-ai)
2. [Who It Is For](#2-who-it-is-for)
3. [System Requirements](#3-system-requirements)
4. [Hosting & Deployment](#4-hosting--deployment)
5. [First-Time Setup](#5-first-time-setup)
6. [Full Feature Reference](#6-full-feature-reference)
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

SiteLog AI is a complete construction daily report system packaged as a single `.html` file. The engineer opens it in their phone browser on site, fills in the day's data, and generates a formal report — including equipment registers with full vehicle details, labor compliance logs, GPS-stamped photos with map links, live weather data, company logos, and legally binding digital signatures from both the owner's inspector and the contractor's superintendent.

**As-Filled Report** — No API key. No internet. No waiting. Compiles every field instantly into a complete structured document. Works 100% offline.

**AI Professional Report** — Claude AI receives all entered data plus field notes and rewrites everything into formal construction industry prose. Requires an Anthropic API key and internet, but queues automatically if offline.

Both modes produce identical output: a live on-screen preview with company logos, a downloadable self-contained HTML file with all photos and signatures embedded, and an automatic email to the configured address.

---

## 2. Who It Is For

| Role | How They Use It |
|---|---|
| **Field Engineer / Site Engineer** | Primary user — fills in all daily data, captures GPS-tagged photos, types or speaks notes, scans vehicle VINs |
| **Owner's Field Inspector** | Reviews the report on-screen and signs the Inspector canvas at shift end |
| **Contractor Superintendent** | Counter-signs the Superintendent canvas at shift end |
| **Project Manager** | Receives the daily email with the HTML attachment containing all logos, photos, and signatures |
| **Safety Officer** | Accident documentation — equipment IDs, vehicle details, incident notes, GPS-stamped photo evidence |
| **Labor Compliance Officer** | Prevailing wage and headcount verification from the formatted labor register |

---

## 3. System Requirements

| Requirement | Detail |
|---|---|
| **Browser — iOS** | Safari 15.4 or later (recommended). Chrome for iOS also supported. |
| **Browser — Android** | Chrome 88 or later (recommended). Samsung Internet 14 or later. |
| **Browser — Desktop** | Chrome, Edge, or Safari. Firefox has limited voice support (see Troubleshooting). |
| **Voice transcription** | Chrome or Safari only. Requires microphone permission. Works fully offline after page load. |
| **AI features** | Anthropic API key + active internet. |
| **GPS** | Browser location permission. Accuracy improves outdoors. Required for photo GPS stamping. |
| **VIN camera scan (offline)** | Any browser with camera access. Tesseract.js OCR (~2MB, cached after first use). |
| **VIN camera scan (AI)** | API key + internet. |
| **EXIF photo metadata** | Camera app with location services enabled at capture time. |
| **Signatures** | Touch (single finger) or mouse. Multi-touch not supported on signature canvases. |
| **Email delivery** | Native email app configured and set as default on the device. |

---

## 4. Hosting & Deployment

SiteLog AI is a single static HTML file — no server, no database, no build process.

1. Upload `construction-daily-report.html` to any HTTPS-capable static host.
2. Share the URL with engineers. They open it in their phone browser and optionally add it to their home screen.

**Tested hosts:** GitHub Pages, Netlify, Vercel, AWS S3 + CloudFront, Cloudflare Pages.

The file must be served over **HTTPS** (not `file://` or plain HTTP). GPS, camera access, and voice transcription require a secure origin — browsers block these features on plain HTTP and local file:// paths.

---

## 5. First-Time Setup

**Step 1 — Open the file.** Navigate to the hosted URL in Safari (iPhone) or Chrome (Android).

**Step 2 — Install to home screen** *(strongly recommended)*. On iPhone: tap the Share button in Safari → **Add to Home Screen**. On Android: tap the three-dot menu in Chrome → **Add to Home Screen**. The app launches fullscreen and the browser caches it for offline use.

**Step 3 — Grant permissions.** The browser requests location, microphone, and camera on first use. Grant all three. These are remembered for future sessions.

**Step 4 — Enter configuration.** In the Configuration panel, enter your **Anthropic API key** and **report email address**. Tap **Save Config**.

**Step 5 — Upload company logos.** In the Project Info panel, tap the three logo slots (Owner, Project, Contractor) to upload logos from your gallery.

**Step 6 — Save a crew template** *(optional)*. Add your standing crew in the Labor panel, tap **Save Template**, name it. Load it in one tap at the start of every future shift.

**Step 7 — Save an equipment template** *(optional)*. Add your site equipment with VINs and plate data, tap **Save Template** in the Equipment panel. All NHTSA vehicle data is preserved.

---

## 6. Full Feature Reference

### 6.1 Sticky Header Bar

Fixed at the top while scrolling. Contains:

- **SiteLog AI** wordmark
- **GPS badge** — current coordinates and accuracy. Tap to force a fresh GPS fix.
- **ONLINE / OFFLINE badge** — live connectivity indicator, updates within 1–2 seconds.
- **Date badge** — today's date, set at page load.

---

### 6.2 Offline Banner & Queue Counter

A yellow banner appears when the device goes offline. A queue badge on the right counts AI report requests waiting to be submitted when connectivity resumes. The queue persists in `localStorage` across page refreshes.

---

### 6.3 Configuration Panel

| Field | Description |
|---|---|
| **Anthropic API Key** | `sk-ant-...` from [console.anthropic.com](https://console.anthropic.com). Required for AI report, AI photo captioning, and AI VIN scanning. Stored in `localStorage`. Sent only to `api.anthropic.com`. |
| **Email Report To** | Destination address for generated reports. Pre-fills the mailto link. |
| **Save Config** | Writes both values to `localStorage`. |
| **Load Saved Draft** | Restores project info, notes, equipment, labor, logos, and GPS from the last autosave. |
| **Clear Draft** | Deletes the draft from `localStorage` after confirmation. |

---

### 6.4 Project Info Panel

| Field | Detail |
|---|---|
| Project Name | Appears in report header and downloaded file name |
| Engineer Name | Report author |
| Report Date | Defaults to today |
| Overall Progress % | 0–100, included in header |
| Workers on Site | Total headcount |
| Shift | Day / Night / Full Day |
| GPS Location | Auto-populated from GPS capture |

All fields autosave 1.5 seconds after the last change.

---

### 6.5 Report Header Logos

Three logo slots in the Project Info panel accept any image from the gallery:

| Slot | Position in Report | Intended Use |
|---|---|---|
| **Left** | Left-aligned | Owner / client organisation logo |
| **Center** | Centred | Project logo or government agency seal |
| **Right** | Right-aligned | Contractor or engineering firm logo |

**To upload:** Tap the slot → gallery opens → select image → loads immediately.

**To remove:** Hover or tap the slot to reveal the red **×** button.

**Dimensions in report:** Maximum 150px wide × 60px tall, `object-fit: contain`. The three logos sit in a horizontal bar above the report title, separated by a rule line. Works with any logo shape (square, wide, tall) without distortion.

**Persistence:** Logos are saved as base64 in the autosave draft and restored when Load Saved Draft is tapped.

---

### 6.6 GPS Auto-Capture

GPS is acquired automatically on page load with `enableHighAccuracy: true`. The fix typically arrives in 3–10 seconds outdoors. The header badge and Project Info GPS field update when the fix arrives.

Tapping the GPS badge forces a fresh fix at any time. Page-load GPS is used in the report header. Per-photo GPS is captured separately at the moment each photo is taken (see section 6.12).

---

### 6.7 Weather Condition Selector

Six chips: Sunny, Partly Cloudy, Rainy, Storm, Windy, Cold. Tap to select. Only one active at a time. Included in the report header and AI prompt.

---

### 6.8 Wind Speed & Temperature Auto-Fetch

Manual entry or tap **Auto-Fetch** to call the [Open-Meteo](https://open-meteo.com) API (free, no key) using current GPS coordinates. Both fields populate from live weather station data. Once populated, values are saved in the draft and included in all report modes including offline.

---

### 6.9 Equipment Log

Each equipment row contains: **Eq ID**, **Name/Description**, **Make**, **Status** (Active / Idle / Off Site / Breakdown). All text fields have 🎙 mic buttons for voice input. Two template buttons sit at the top: **💾 Save Template** and **📋 Load Template**.

---

### 6.10 Vehicle Sub-Panel — Plate, VIN & NHTSA Lookup

Tapping **Add Vehicle** adds vehicle-specific fields to the row:

| Field | Detail |
|---|---|
| **License Plate** | Manual entry or **📷 Scan Plate** — opens camera, uses Claude AI vision to read plate characters |
| **VIN** | 17-character VIN — three entry methods (see section 6.11) |
| **🔍 NHTSA Lookup** | Submits VIN to NHTSA vPIC API; populates Make, Model, Year, Body Class, Drive Type, Fuel Type, GVWR, Axles, Axle Configuration |

A **🚛 VEHICLE** badge distinguishes vehicle rows from general equipment.

---

### 6.11 VIN Input — Three Entry Methods

**🎙 Speak** — Dictate the VIN character by character. Real-time transcription fills the field. Works fully offline.

**📷 Offline Camera Scan** — Tap to open the rear camera. Take a photo of the VIN sticker or plate. The image is processed entirely on-device:

1. Converted to greyscale and contrast-boosted (1.6× contrast stretch to improve legibility on metallic plates)
2. **Tesseract.js** runs OCR locally in the browser — no data leaves the device
3. Character whitelist restricted to valid VIN characters (A–Z excluding I/O/Q, and 0–9)
4. Single-line page segmentation mode (PSM 7) optimised for short character strings
5. A 17-character sequence is extracted and filled into the VIN field

Tesseract's language model (~2MB) downloads once on first use and is cached in IndexedDB. All subsequent scans are instant and offline.

**Best results:** Fill the frame with just the VIN label, hold steady, scan in shade to avoid glare on metallic plates.

**🤖 AI Scan (Online)** — Opens rear camera, compresses the image, sends to Claude API for high-accuracy recognition. Handles difficult lighting and unusual fonts better than Tesseract. Requires internet and API key.

---

### 6.12 Idle Time Capture

When a vehicle or equipment status is set to **Idle**, an orange row expands with Hours, Minutes, and Reason fields. The Reason field has a 🎙 mic. Idle time and reason appear in the equipment register section of the report.

---

### 6.13 Equipment Templates

**💾 Save Template** — Names and saves the current equipment list with all vehicle data (plate, VIN, NHTSA results) to `localStorage`. Overwrites existing templates with the same name after confirmation.

**📋 Load Template** — Lists saved templates with item count and save date. Load in **Replace** or **Append** mode. Status resets to Active on load; all other fields preserved.

**✕** — Deletes a template after confirmation. Key: `sitelog_eq_templates`.

---

### 6.14 Labor Compliance Log

Each worker row: **Full Name** (legal name for prevailing wage), **Trade / Role**, **Employer / Company**. All three fields have 🎙 mic buttons. Headcount in Project Info should match the total workers in this log.

---

### 6.15 Bulk Labor Entry Modal

Tap **Bulk Add** to open a text area. Paste one worker per line:

```
Full Name, Role
Full Name, Role, Company
```

Lines are parsed and added as individual worker rows. Useful when transferring a crew list from a spreadsheet.

---

### 6.16 Crew Templates

Identical to equipment templates but for the labor roster. Key: `sitelog_crew_templates`.

---

### 6.17 Per-Field Voice Input

Every text input in Equipment and Labor panels has a dedicated 🎙 mic button:

- Only one field mic active at a time — tapping a new one stops the previous
- Transcribed text is **appended** to the existing field value (does not overwrite)
- First letter of each recognition segment is auto-capitalised
- Autosave triggers after each committed segment
- Button pulses yellow while active
- Main voice recorder (Record Voice button) automatically stops any active field mic

---

### 6.18 Site Notes — Voice & Text Input

The main notes text area accepts free-form input by typing or live voice transcription.

**Record Voice** starts a continuous speech recognition session. Words appear in the notes box in real time.

- Runs continuously until the engineer taps **Stop**
- Auto-restarts on mobile browser 60-second inactivity timeout — sessions can run indefinitely
- Each committed utterance is auto-capitalised
- Stops cleanly if Generate Report is tapped while recording (400ms pause to commit final words)

---

### 6.19 Multi-Language Input Support

Language pills below Site Notes: **English**, **Español**, **中文**, **Tiếng Việt**.

Selecting a language sets the `SpeechRecognition.lang` property for all voice inputs (main recorder and all field mics), and instructs the AI to translate notes to English before drafting the report.

---

### 6.20 Quick-Start Hint Chips

Seven chips insert pre-typed phrases at the cursor position: `# Concrete pour`, `# Safety`, `# Delay`, `# Inspection`, `# Materials`, `# RFI`, `# Plan`.

---

### 6.21 Report Section Toggles

Six toggles control which sections appear in the generated report: Work Completed, Safety & HSE, Resources & Equipment, Delays & Issues, Quality & Inspections, Plan for Tomorrow. All active by default. Changes saved in the autosave draft.

---

### 6.22 Site Photos — Camera & Gallery

**📷 Take Photo**

1. Camera opens immediately (required synchronously inside the tap handler by iOS security policy)
2. A fresh GPS fix is requested in parallel (`enableHighAccuracy: true`, `maximumAge: 0` — never cached)
3. After the photo loads, a polling loop checks every 300ms for up to 12 seconds for the GPS result
4. The GPS map link appears in the photo card as soon as coordinates arrive (typically 1–5 seconds)

**🖼 Choose from Gallery**

1. Photo library opens with multiple selection enabled
2. **exifr** (full build) parses EXIF metadata from each selected photo:
   - `DateTimeOriginal` — exact shutter-fire time (not import time)
   - `GPSLatitude` / `GPSLongitude` — GPS coordinates embedded by the camera app
3. Photo timestamp shows the original capture time from EXIF (not the current time)
4. If EXIF GPS is present, the map link appears. If absent (location was off, or file is a screenshot), the GPS line is omitted.

**iOS privacy note:** If **Settings → Privacy → Location Services → Camera → Precise Location** is off, GPS in gallery photos is rounded to ~1km accuracy. This is an iOS system restriction.

---

### 6.23 Photo GPS Coordinates & Map Links

Each photo card shows a clickable blue coordinate pill below the timestamp, e.g.:

`📍 37.812456, -121.654321 ±4m`

Tapping opens **Apple Maps** on iPhone (or the default maps app in any browser) at the exact coordinates, zoomed to street level with satellite imagery. The URL format is `https://maps.apple.com/?ll={lat},{lng}&z=18&t=h`, which redirects to Google Maps on non-Apple platforms.

GPS for **Take Photo** = live fix at moment of capture.  
GPS for **Gallery** = EXIF coordinates from original photo capture (may be a different date and location).

---

### 6.24 Photo Voice Captions

Each photo card has a 🎙 **Speak** button. Tapping starts the field mic for that photo's caption text area. The inspector dictates while looking at the photo. Multiple photos can be captioned in sequence by tapping each card's Speak button.

---

### 6.25 Digital Signatures

Two canvases: **Owner / Field Inspector** and **Contractor Superintendent**. Both use the Pointer Events API with `setPointerCapture` for accurate stroke tracking on touch and mouse. DPR-scaled for crisp rendering on Retina screens. Page scroll is suppressed while a finger is on the canvas.

Signing changes the status from "Not signed" (grey) to "✓ Signed" (green). **Clear** erases the canvas.

**Session note:** Signatures are not saved in the autosave draft — they must be re-drawn if the page is refreshed.

---

### 6.26 Generate Report — Two-Path Choice Modal

Tapping **⚡ Generate Full Report** opens a modal:

| Path | Internet | API Key | Speed | Output |
|---|---|---|---|---|
| **📋 As-Filled** | No | No | Instant | All data compiled verbatim |
| **⚡ AI Professional** | Yes (or queued) | Yes | 5–20s | Formal narrative prose |

---

### 6.27 As-Filled Report

Assembles a complete structured report from form data. Includes: report header with logos, all toggled sections from site notes, numbered equipment register (ID, name, make, status, VIN, plate, NHTSA data, idle time and reason), column-aligned labor compliance table, photo log with GPS links, and sign-off block.

---

### 6.28 AI-Generated Professional Report

Sends all data to Claude Sonnet via the Anthropic Messages API. The prompt includes project info, weather, all equipment with NHTSA data, full labor roster, photo captions, active section list, and raw field notes. Claude rewrites everything into formal construction industry prose with narrative paragraphs per section.

If notes were entered in Spanish, Chinese, or Vietnamese, the AI translates before drafting. Output is always in English.

If offline when Generate is tapped, the request queues in `localStorage` and submits automatically on reconnection.

---

### 6.29 Report Output Panel

Appears after generation. Contains:

1. **Logo bar** — three company logos in left / center / right positions
2. **Report text** — full formatted content
3. **Photo thumbnails** — grid with category, caption, and GPS map link per photo
4. **Signature images** — both canvases with signer names and date

Action buttons: **↺ Regenerate**, **⎘ Copy Text**, **↓ Download**, **✉ Send Email**.

---

### 6.30 Email Delivery

When **Send Email** is tapped:

1. The self-contained HTML file is built in memory (logos + report body + photos + signatures, all as inline base64) and downloaded automatically to the device's Downloads folder
2. A `mailto:` link opens the native email client with To, Subject, and clean plain-text body pre-filled
3. The engineer attaches the downloaded `.html` file from Downloads before sending

Photos and signatures are in the HTML attachment — not in the email body — because binary image data cannot be encoded in a `mailto:` URL body (2,000-character practical limit).

---

### 6.31 HTML Report File

`SiteReport_{Project}_{Date}.html` — fully self-contained, opens in any browser, printable to PDF.

Contains: three company logos in a styled header bar, report title and info block, formatted report body with section headings, full-resolution photos with captions and clickable GPS map links, signature images with signer names and date, and a print stylesheet.

---

### 6.32 Auto-Save & Draft System

All text data, equipment, labor, configuration, logos, and GPS are autosaved to `localStorage` 1.5 seconds after the last change.

**Load Saved Draft** restores: project info, notes, weather, wind, temperature, equipment list (including all NHTSA data), labor roster, GPS, language setting, section toggles, and logos.

**Not saved:** Photos (too large for localStorage) and drawn signatures (session only).

---

### 6.33 Offline Mode & AI Report Queue

| Feature | Offline Status |
|---|---|
| As-Filled reports | ✅ Fully offline |
| Voice transcription | ✅ Fully offline (Web Speech API on-device) |
| Per-field voice mics | ✅ Fully offline |
| GPS | ✅ Fully offline (device hardware) |
| Tesseract VIN scan | ✅ Offline after first model load (~2MB cached) |
| EXIF reading | ✅ Fully offline (exifr runs in browser) |
| Weather auto-fetch | ❌ Requires internet (values retained once fetched) |
| AI report generation | ⏳ Queued offline, sent on reconnect |
| AI photo captioning | ❌ Requires internet + API key |
| AI VIN scan (🤖) | ❌ Requires internet + API key |
| NHTSA lookup | ❌ Requires internet |

---

## 7. Recommended End-of-Shift Workflow

1. **Before arriving on site** — open the app, confirm ONLINE badge is green. Load crew and equipment templates.
2. **On site** — tap Record Voice and speak observations, incidents, and progress notes as they happen. Add workers or remove as crew changes throughout the shift.
3. **Equipment** — add new equipment or vehicles. Use 📷 to scan VINs. Run 🔍 NHTSA lookup. Set status to Idle when applicable, record reason and duration.
4. **Photos** — tap 📷 Take Photo for GPS-tagged site photos. Tap 🎙 Speak on each card immediately after to dictate a caption while still at the location.
5. **End of shift** — verify labor headcount. Set final equipment statuses. Auto-Fetch weather if not already done.
6. **Signatures** — hand the phone to the Inspector for signature, then to the Superintendent.
7. **Generate** — tap ⚡ Generate Full Report. Choose report type. Wait for completion.
8. **Send** — tap ✉ Send Email. The HTML file downloads automatically. In your mail app, attach the file from Downloads and send.

---

## 8. Choosing Between the Two Report Types

| | As-Filled | AI Professional |
|---|---|---|
| **Internet required** | No | Yes (or queued) |
| **API key required** | No | Yes |
| **Speed** | Instant | 5–20 seconds |
| **Notes treatment** | Verbatim | Rewritten to formal prose |
| **Best for** | Standard daily reporting; low-connectivity sites; precise wording control | Client-facing reports; formal documentation requirements; polished language |
| **Content completeness** | Identical | Identical |

---

## 9. Email System — Step-by-Step Explanation

When **Send Email** is tapped, three things happen in sequence:

1. `buildHTMLReport()` assembles the self-contained HTML with all logos, photos, and signatures as inline base64.
2. `downloadHTMLReport()` saves it to the device's Downloads folder as `SiteReport_{Project}_{Date}.html`.
3. A `mailto:` URL opens the native email app with To, Subject, and a clean plain-text body pre-filled (truncated at 1,950 characters if the report is long, with a note that the full report is in the attachment).

The engineer then attaches the HTML file and sends. The project manager opens the `.html` attachment in any browser to view the complete report.

---

## 10. Installing as a Home Screen App (PWA)

**iPhone / iPad (Safari):**
1. Open the app URL in Safari
2. Tap the **Share** button → **Add to Home Screen** → **Add**

**Android (Chrome):**
1. Open the app URL in Chrome
2. Tap ⋮ → **Add to Home Screen** → confirm

After installation, the browser caches the app for offline access. The app opens fullscreen without browser chrome.

---

## 11. Mobile Tips & Best Practices

**Keep the screen on.** Raise Auto-Lock time in **Settings → Display & Brightness → Auto-Lock** during shifts to prevent the screen dimming while voice recording.

**Landscape mode for signatures.** The canvas fills better in landscape and produces a more natural signature.

**Take photos before leaving the area.** GPS is stamped at the moment the photo is taken. Moving to a different location and retaking gives incorrect coordinates.

**Record voice incrementally.** Tap Record → dictate a section → tap Stop. Repeat. More reliable than leaving the recorder running for a full shift.

**Scan VINs in shade.** Direct sunlight creates glare on metallic VIN plates. Angle the phone 10–15 degrees to eliminate reflection.

**Load templates at shift start.** Templates reduce setup to two taps.

**Confirm the autosave dot is green before navigating away.** Autosave fires 1.5 seconds after each change — confirm the timestamp is current.

---

## 12. Multi-Inspector Use

SiteLog AI is a single-user tool — one HTML file, one draft slot per device. For multiple inspectors:

- Each inspector uses their own copy of the HTML file on their own device.
- All reports email to the same project manager address.
- For combined reports, one inspector collects all notes; both parties sign on the same device at shift end.

---

## 13. API Key Setup & Cost Estimate

**Getting an API key:**
1. Go to [console.anthropic.com](https://console.anthropic.com) and sign in or create an account.
2. Navigate to **API Keys** → **Create Key**.
3. Copy the key (shown only once). Paste into Configuration and tap **Save Config**.

**Approximate costs per shift:**

| Operation | Approx. Cost |
|---|---|
| AI report generation | $0.05–$0.12 |
| AI photo caption (per photo) | $0.003 |
| AI VIN scan (per vehicle) | $0.002 |
| As-Filled report | Free |
| Voice transcription | Free |
| Tesseract VIN scan | Free |
| GPS | Free |
| NHTSA lookup | Free |
| Weather auto-fetch | Free |

A typical shift with 5 photos and 3 vehicle scans costs approximately **$0.08–$0.15**. Verify current pricing at [anthropic.com/pricing](https://www.anthropic.com/pricing).

---

## 14. Privacy & Data Storage

**What stays on the device:**
- All form data, notes, equipment, labor
- Photos (session memory), Signatures (session memory)
- Draft, API key, templates, logos (localStorage)
- Tesseract OCR language model (IndexedDB)

**What leaves the device:**

| Data | Destination | When |
|---|---|---|
| Notes + all entered data | Anthropic API | AI report mode only |
| Photos (base64) | Anthropic API | AI photo captioning or AI VIN scan only |
| GPS coordinates | Open-Meteo API | Auto-Fetch weather tap only |
| VIN | NHTSA vPIC API | NHTSA Lookup tap only |

No analytics. No telemetry. No third-party tracking scripts. The API key is stored locally and sent only to `api.anthropic.com`.

---

## 15. Troubleshooting

### Camera does not open after tapping Take Photo
Confirm the browser has camera permission: **Settings → Safari → Camera → Allow**. The page must be served over HTTPS — camera access is blocked on HTTP and `file://`.

### GPS badge shows orange / "Denied" error
Go to **Settings → Privacy & Security → Location Services** and enable location for Safari. Set to **While Using App** or **Always**. Tap the GPS badge to retry.

### GPS link does not appear under a photo
**Take Photo:** GPS is acquired in the background with a 12-second polling window. Poor indoor GPS may miss this window — move outdoors and retry. **Gallery:** The photo must have GPS EXIF tags. If location was disabled in the Camera app at capture time, no GPS is embedded and the link is correctly omitted.

### Tesseract VIN scan returns garbled characters or wrong length
Common causes: glare (angle to eliminate reflection), blur (hold steady with elbows braced), poor contrast in low light, worn or dirty VIN label. Try the 🤖 AI Scan instead when internet is available.

### Tesseract shows "Loading OCR engine" every time
The language model caches in IndexedDB on first use. If it re-downloads on every session, the browser is clearing IndexedDB storage (possible in low-storage situations). On iPhone, check **Settings → Safari → Advanced → Website Data** to ensure the site is not being restricted.

### Logo does not appear in the report
Confirm the slot shows the image preview (not the "＋" placeholder). Regenerate the report — the logo bar is built at generation time. Confirm the image is JPEG, PNG, GIF, or WebP (SVG is not supported).

### Voice transcription does not start
Confirm microphone permission: **Settings → Safari → Microphone → Allow** (iPhone) or tap the lock icon → Microphone → Allow (Android Chrome). Firefox does not support the Web Speech API — use Chrome or Safari. Reload the page after granting permission.

### Speech recognition says "not-allowed" or "service-not-allowed"
Microphone permission error. On Android, check both OS-level and browser-level microphone permissions. On iPhone with Screen Time enabled, check **Settings → Screen Time → Content & Privacy Restrictions → Microphone**.

### Signature canvas has no effect when drawing on mobile
Use a single finger only. Draw slowly for the first stroke. If stroke position is offset, rotate to landscape and back to portrait to trigger canvas resize, then retry.

### AI report generation returns an error
Confirm the API key is saved (Configuration panel shows `API key saved`). Check account credits at [console.anthropic.com](https://console.anthropic.com). Confirm ONLINE badge is green. Authentication error = key invalid or revoked — generate a new key from the console.

### Email client does not open
A default email account must be configured on the device. iPhone: **Settings → Mail → Accounts → Add Account**. Android: **Settings → Accounts → Add Account → Email**. If using Gmail or Outlook as default, confirm it is set as the default mail handler.

### HTML file does not appear in Downloads
iPhone: **Files → On My iPhone → Downloads** or iCloud Drive → Downloads. Android: **Files** app or **Downloads** folder. If the download did not trigger, tap **↓ Download** in the report output panel.

### Load Saved Draft does not restore photos or signatures
Photos and signatures are session-only and intentionally not stored in localStorage (photos at mobile resolution are 30–80 MB per session, far exceeding localStorage capacity). Re-upload photos and re-draw signatures each session. All text data, equipment, labor, notes, and logos are fully restored.

---

## 16. Technology Stack

| Component | Technology | Detail |
|---|---|---|
| **UI** | Vanilla HTML5 / CSS3 / ES6 JavaScript | Zero external frameworks; zero build tools |
| **Fonts** | Google Fonts CDN | Bebas Neue (headings), DM Sans (body), DM Mono (report output) |
| **AI model** | Claude Sonnet (`claude-sonnet-4-20250514`) | Anthropic Messages API v`2023-06-01` |
| **Vision — photo captions** | Claude Sonnet | Photos as base64 content blocks |
| **Vision — AI VIN scan** | Claude Sonnet | Character whitelist prompt; 17-char validation |
| **OCR — offline VIN scan** | Tesseract.js v5 | In-browser OCR; `eng` language; PSM 7; whitelist `ABCDEFGHJKLMNPRSTUVWXYZ0123456789` |
| **EXIF reading** | exifr v7 (full build) | Extracts `GPSLatitude`, `GPSLongitude`, `DateTimeOriginal` from gallery photos |
| **Weather API** | Open-Meteo | Free, no key; returns current wind speed, direction, temperature |
| **GPS** | Browser Geolocation API | `enableHighAccuracy: true`, `maximumAge: 0` (always fresh) |
| **Signatures** | HTML5 Canvas + Pointer Events API | DPR-scaled; `setPointerCapture`; touch-action suppressed |
| **Voice transcription** | Web Speech API | `SpeechRecognition` / `webkitSpeechRecognition`; `continuous: true`; auto-restart; `en-US`, `es-MX`, `zh-CN`, `vi-VN` |
| **Vehicle lookup** | NHTSA vPIC API | Decodes VIN → make, model, year, body, GVWR, axles, drive, fuel |
| **localStorage keys** | — | `sitelog_config`, `sitelog_draft`, `sitelog_queue`, `sitelog_crew_templates`, `sitelog_eq_templates` |
| **Photos** | FileReader API + exifr | Base64 data URIs; session memory only |
| **Logos** | FileReader API | Base64 stored in draft; embedded in HTML report |
| **Email** | `mailto:` URI | Native mail client; body stripped by `cleanForEmail()` |
| **HTML report** | Blob URL + `<a download>` | Self-contained; logos, photos, signatures as inline base64 |
| **PWA** | Inline `data:` URI manifest | Add to Home Screen; offline caching |
| **Hosting** | Any HTTPS static file host | GitHub Pages, Netlify, Vercel, AWS S3 + CloudFront |

---

## 17. Version History

| Version | What Changed |
|---|---|
| **v5.1** | **VIN offline OCR rebuilt** — `scanVinOffline()` now opens the rear camera directly, captures a photo, preprocesses the image (greyscale + 1.6× contrast boost), and runs **Tesseract.js v5** on-device OCR. Character whitelist restricted to valid VIN chars; PSM 7 single-line mode. Language model (~2MB) cached in IndexedDB after first use — all subsequent scans are instant and offline. Replaced prior passive iOS Live Text hint that did not open the camera. |
| **v5.0** | **Three report header logos** — Owner (left), Project (center), Contractor (right) logo slots in Project Info panel. Fixed-dimension display (150×60px max, `object-fit: contain`). Logos persist in autosave draft. Appear in on-screen report and downloaded HTML above the title. **VIN voice input** — 🎙 mic button on VIN field. **VIN AI camera scan** — 🤖 button; camera → Claude API → 17-char validation → auto-fill. **VIN offline hint** (upgraded to real camera OCR in v5.1). Hint labels added under VIN field. |
| **v4.5** | **Photo GPS map links** — GPS coordinates captured live at photo take time (`maximumAge: 0`); applied to photo card via polling loop. Gallery EXIF GPS read by exifr and shown as clickable Apple Maps link. **Take Photo flow fixed** — camera opens synchronously in tap handler (iOS security); GPS acquired in parallel, retroactively applied via `updatePhotoCardGPS()`. exifr upgraded from lite to full CDN build for GPS tag support. **Gallery EXIF timestamp** — photo card shows `DateTimeOriginal` from EXIF instead of import time. |
| **v4.4** | **Photo voice captions** — AI Caption button replaced with 🎙 Speak on all photo cards. **Per-field voice input** — 🎙 mic on every text input in Labor (name, role, company) and Equipment (eqId, name, make, idle reason) rows. Shared `SpeechRecognition` instance; auto-stop on new activation; conflicts with main recorder resolved via `stopFieldMic()` call in `toggleRecord()`. |
| **v4.3** | **Crew templates** — save/load named worker rosters; Replace or Append load modes. **Equipment templates** — save/load equipment lists with all NHTSA data preserved; status resets to Active on load. Template modals with name, count, date, Load and ✕ buttons. localStorage keys: `sitelog_crew_templates`, `sitelog_eq_templates`. |
| **v4.2** | **Voice transcription rebuilt** — MediaRecorder replaced with Web Speech API. Real-time on-device transcription. `continuous: true` with auto-restart on mobile timeout. Multi-language voice (`en-US`, `es-MX`, `zh-CN`, `vi-VN`). Voice-only workflow unblocked. Clean stop on Generate tap. Unsupported browser detection. |
| **v4.1** | **Email body symbols fixed** — `cleanForEmail()` strips Unicode box-drawing characters and `##` markers. Photos and signatures embedded in HTML attachment as inline base64. Auto-download on every Send and Download action. |
| **v4.0** | **Two-path report generation modal** — As-Filled and AI Professional. `generatePlainReport()` with numbered equipment register and column-aligned labor table. Automatic email trigger on generation. |
| **v3.1** | Mobile bug fixes — type-safe parameter guards, DOMContentLoaded init, GPS per-error-code messages, Pointer Events signature canvas with DPR scaling, Open-Meteo v1 `current=` parameter fix. |
| **v3.0** | Equipment log with idle time and vehicle fields. Labor compliance log with bulk paste modal. Multi-language input. Offline AI queue. GPS auto-capture. Weather auto-fetch. Dual signatures. Email via mailto. |
| **v2.0** | Site photo upload with drag-and-drop and camera capture. AI auto-captioning. Photo categories. Photo log in report. |
| **v1.0** | Initial release — AI report from field notes, weather chips, voice recording, section toggles, copy and download. |

---

*SiteLog AI · Built for the field. Designed for the office.*  
*Single HTML file · No installation · No backend · Works offline · Mobile-first*
