# NETA 65 Grapevine / La Viña Committee Website

A bilingual (English/Spanish) single-page website for the Northeast Texas Area 65 Grapevine and La Viña Committee. Everything lives in **one file** (`index.html`) — no special software needed.

---

## Table of Contents

1. [How This Website Works](#how-this-website-works)
2. [What You Need](#what-you-need)
3. [Quick Start](#quick-start)
4. [Google Drive Setup](#google-drive-setup)
5. [How to Update Content](#how-to-update-content)
   - [Announcements](#add-an-announcement)
   - [Events](#add-an-event)
   - [Reports](#add-a-monthly-report)
   - [Meeting Notes](#add-meeting-notes)
   - [Meeting Slides](#add-meeting-slides)
   - [Booth Photos](#add-a-booth-photo)
   - [Meeting Info / Zoom](#update-meeting-info)
   - [Weekly Open Meeting Info](#update-weekly-open-meeting-info)
   - [Editorial Calendar](#update-editorial-calendar)
   - [Subscription Prices, Tiers, Gift, and Phones](#update-subscription-prices)
   - [YouTube Videos](#add-a-youtube-video)
   - [Podcast Episodes](#add-a-podcast-episode)
   - [Instagram Posts](#add-an-instagram-post)
   - [Timeline Milestones](#add-a-timeline-milestone)
   - [Resource Links](#add-a-resource-link)
   - [Page Headers (Heroes)](#update-page-headers-heroes)
   - [Home Page Cards](#update-home-page-cards)
   - [Contribute Page — Submission Types](#update-what-you-can-submit-cards-contribute-page)
   - [Contribute Page — Submission Channels](#update-submission-methods-gv--lv)
   - [GVR/RLV Postcards & Flyers](#update-gvr--rlv-postcards--flyers)
6. [Language / Translation (EN ↔ ES)](#language--translation-en--es)
7. [File Naming Rules](#file-naming-rules)
8. [BASE_PATH Setting](#base_path-setting)
9. [Website Pages](#website-pages)
10. [What GVRs and RLVs Need to Know](#what-gvrs-and-rlvs-need-to-know)
11. [Monthly Checklist](#monthly-checklist)
12. [Quarterly Checklist](#quarterly-checklist)
13. [Annual Checklist](#annual-checklist)
14. [Deploy to GitHub Pages](#deploy-to-github-pages)
15. [Troubleshooting](#troubleshooting)
16. [Technical Details](#technical-details)

---

## How This Website Works

The entire website is a single HTML file. All the content you'll ever need to update is stored in clearly labeled configuration arrays near the top of the `<script>` section. You edit those arrays, save the file, and the website updates automatically.

**You do NOT need to know how to code.** You just need to follow the patterns shown below — copy an existing entry, change the text, and save.

### Key Features

- **Bilingual**: Full English/Spanish toggle — all page content, dates, buttons, and labels switch instantly
- **Responsive**: Works on every screen from 320px phones to 4K desktops
- **Accessible**: Skip-to-content link, keyboard focus ring, 44×44 touch targets, reduced-motion support, iOS safe-area handling
- **Auto-generated meetings**: Monthly committee meetings (3rd Wednesday) are calculated automatically
- **Countdown timer**: Live countdown to the next meeting on the home page
- **90-day announcements**: Old announcements automatically hide after 90 days
- **Random media picks**: Home page shows different podcast and YouTube selections each visit
- **PDF viewer**: Documents open in an inline viewer; Drive-hosted PDFs use Drive's native `/preview` endpoint, external PDFs use Google Docs Viewer
- **Google Drive smart links**: Paste any Drive sharing-link format (`/view`, `/preview`, `?id=`, docs.google.com URLs) — the site auto-transforms it to the right endpoint for iframes, images, and downloads
- **Calendar export**: Events can be added to any calendar app via .ics download
- **Share buttons**: Announcements and events can be shared via native share or clipboard

---

## What You Need

- **A text editor** — Notepad (Windows), TextEdit (Mac), or VS Code all work
- **Internet connection** — the site loads fonts and icons from the web
- **Google Drive** (optional) — for storing and sharing documents and photos
- **A web browser** — Chrome, Firefox, Edge, or Safari for testing

---

## Quick Start

1. Open `index.html` in your text editor
2. Find the section marked `CONFIGURATION — EDIT THESE ARRAYS TO UPDATE THE SITE` (around line 230)
3. Make your changes following the instructions below
4. Save the file
5. Double-click `index.html` to preview in your browser
6. When satisfied, push to GitHub (or ask someone who can)

> **Tip:** Use Ctrl+F (or Cmd+F on Mac) to search for the exact array name like `ANNOUNCEMENTS` or `SPECIAL_EVENTS`.

---

## Google Drive Setup

All documents (PDFs) and photos can be stored in Google Drive. This is the recommended approach so that multiple committee members can upload files without needing to edit code.

### Step 1 — Create Folders in Google Drive

Create a shared folder structure like this:

```
GV_NETA65 (shared folder)
├── reports/     ← monthly committee reports
├── notes/       ← meeting notes
├── slides/      ← meeting slide decks
├── flyers/      ← event flyer PDFs
└── photos/      ← booth and event photos
```

### Step 2 — Set Sharing Permissions

For each folder:
1. Right-click the folder in Google Drive
2. Click **Share**
3. Under "General access," change to **"Anyone with the link"**
4. Set permission to **"Viewer"**
5. Click **Copy link**

> **Important:** If sharing permissions expire or get changed, the documents will stop loading on the website. Check these at least once a year (see [Annual Checklist](#annual-checklist)).

### Step 3 — Add Folder Links to the Website

Open `index.html` and find this section near the top:

```js
const GOOGLE_DRIVE = {
  reports: "",   // folder link for monthly reports
  notes:   "",   // folder link for meeting notes
  slides:  "",   // folder link for slide decks
  flyers:  "",   // folder link for event flyers
  photos:  "",   // folder link for booth photos
};
```

Paste your Google Drive folder links between the quotes. Example:

```js
const GOOGLE_DRIVE = {
  reports: "https://drive.google.com/drive/folders/ABC123?usp=sharing",
  notes:   "https://drive.google.com/drive/folders/DEF456?usp=sharing",
  slides:  "https://drive.google.com/drive/folders/GHI789?usp=sharing",
  flyers:  "https://drive.google.com/drive/folders/JKL012?usp=sharing",
  photos:  "https://drive.google.com/drive/folders/MNO345?usp=sharing",
};
```

When these are filled in, the Documents and Photos pages will show "View on Google Drive" buttons.

### Step 4 — Link Individual Files

For every document, photo, and flyer in the site, you can use either:

- **Local file path** (just the filename in the matching folder): `"report-2026-04.pdf"`
- **Google Drive sharing link** (full URL): `"https://drive.google.com/file/d/FILEID/view?usp=sharing"`

Both forms drop in to the **same `filename` field** of the matching array — the website detects which one you pasted and routes it to the right place.

#### Getting a Drive sharing link

1. In Google Drive, right-click the file → **Share**
2. Set **General access** → "Anyone with the link" → **Viewer**
3. Click **Copy link**
4. Paste the entire URL as the value of the `filename` field

#### Any Drive link format works

The site contains a small `driveUrl()` helper that recognizes **all** of these sharing-link formats and converts them to the right form for each use case (iframe preview, image, download, etc.). You can paste any of these and it will just work:

| Pattern | Notes |
|---|---|
| `https://drive.google.com/file/d/FILE_ID/view?usp=sharing` | Default "Copy link" output — most common |
| `https://drive.google.com/file/d/FILE_ID/preview` | Preview URL |
| `https://drive.google.com/open?id=FILE_ID` | Older share format |
| `https://drive.google.com/uc?export=download&id=FILE_ID` | Direct-download URL |
| `https://docs.google.com/document/d/FILE_ID/edit` | Google Docs |
| `https://docs.google.com/spreadsheets/d/FILE_ID/edit` | Google Sheets |
| `https://docs.google.com/presentation/d/FILE_ID/edit` | Google Slides |

#### What the site does with each link

| Where it appears | What the site does with the link |
|---|---|
| Reports / Notes / Slides download buttons | Opens the Drive viewer page in a new tab |
| Inline PDF viewer modal (clicking a GVR PDF) | Embeds Drive's own `/preview` iframe (full PDF viewing inside the site) |
| Inline PDF viewer "Open" button | Drive viewer page in new tab |
| Inline PDF viewer "Download" button | Direct-download endpoint (forces a file download) |
| Booth photos `<img>` | Drive `thumbnail` endpoint (fast loading, sized to ~2000px wide) |
| Event flyer link | Drive viewer page in new tab |

> **Important:** All linked files **must** be set to "Anyone with the link → Viewer". Files with restricted permissions will load as broken images or empty PDF viewers.

#### Mixing local and Drive links

You can mix and match — for example, store reports locally but photos on Drive. Each `filename` field is independent.

---

## How to Update Content

Open `index.html` in any text editor. Scroll down to the `<script>` section and look for:

```
CONFIGURATION — EDIT THESE ARRAYS TO UPDATE THE SITE
```

Everything you need to change is in this section. Below are step-by-step instructions for every common task.

**Important:** Always keep the commas, quotes, and curly braces exactly as shown. If something breaks, compare your edit to the examples below.

---

### Add an Announcement

Find `const ANNOUNCEMENTS = [` and add a new entry **at the top** (newest first):

```js
{
  date: "2026-05-01",
  title: "Your Announcement Title",
  body: "Your announcement text here."
},
```

> Announcements older than 90 days are automatically hidden.

You can include HTML links in the `body` field:
```js
body: "Visit <a href=\"https://example.com\" target=\"_blank\" rel=\"noopener\" class=\"text-brand-600 underline hover:text-brand-700\">this link</a> for details."
```

---

### Add an Event

Find `const SPECIAL_EVENTS = [` and add:

```js
{
  date: "2026-06-15",
  title: "Event Name",
  location: "City, TX",
  description: "What the event is about.",
  flyerFile: "my-flyer.pdf"
},
```

- **flyerFile** can be a local filename (in the `flyers/` folder) or a full Google Drive link
- Use `""` (empty quotes) if there is no flyer
- Monthly committee meetings are generated automatically — you only add special events here
- Events have Share, Calendar (.ics), and View Flyer buttons in the detail modal

---

### Add a Monthly Report

Find `const REPORTS = [` and add **at the top**:

```js
{ month: "April 2026", filename: "report-2026-04.pdf" },
```

- **filename** can be a local file or a Google Drive link

---

### Add Meeting Notes

Find `const MEETING_NOTES = [` and add **at the top**:

```js
{
  month: "April 2026",
  date: "2026-04-15",
  filename: "notes-2026-04.pdf",
  summary: "Brief summary of what was discussed."
},
```

The newest entry automatically becomes the featured "Latest Meeting Notes" card on the Documents page.

---

### Add Meeting Slides

Find `const MEETING_SLIDES = [` and add **at the top**:

```js
{ month: "April 2026", filename: "slides-2026-04.pdf" },
```

---

### Add a Booth Photo

Find `const BOOTH_PHOTOS = [` and add:

```js
{ filename: "my-photo.jpg", caption: "Description — Event Name, City TX" },
```

- **filename** can be a local file (in `photos/`) or a Google Drive link
- The gallery auto-cycles through all photos every 5 seconds
- Previous/next arrows and dot indicators are generated automatically

---

### Update Meeting Info

Find `const MEETING_INFO = {` and change any of these fields:

| Field | What it controls |
|-------|-----------------|
| `schedule` | Text like "3rd Wednesday of Every Month" |
| `time` | Text like "7:00 PM – 8:00 PM (Central)" |
| `zoomLink` | The full Zoom join URL |
| `meetingId` | Zoom Meeting ID |
| `passcode` | Zoom passcode |
| `chair` | Chair's title or name |
| `chairEmail` | Chair's email address |
| `additionalNotes` | Extra note shown on the Meeting page |

> The next meeting date and countdown timer are calculated automatically — you do not need to update them. They always point to the next 3rd Wednesday.

---

### Update Weekly Open Meeting Info

Find `const WEEKLY_OPEN = {` and update:

```js
const WEEKLY_OPEN = { zoomId: "871 2036 8287", passcode: "238047", day: "Wednesdays", time: "11 AM Central" };
```

This info appears on the About page and in the Resources page under "GV Weekly Open Meeting."

---

### Update Editorial Calendar

Find `const EDITORIAL_CALENDAR = [` and replace with current topics from [aagrapevine.org/contribute](https://www.aagrapevine.org/contribute):

```js
{ issueMonth: "Month Year", topic: "Topic Name", deadline: "YYYY-MM-DD" },
```

- Leave `deadline: ""` for issues with no deadline (e.g., "Classic Grapevine")
- The Contribute page automatically highlights the next upcoming deadline
- Past deadlines are shown with a "Past" badge

---

### Update Subscription Prices

All Subscribe page pricing lives in the `SUBSCRIPTION_TIERS` array. **You do not need to touch any render code.** Each tier is one entry that produces one pricing card:

```js
{
  section:"gv",                                  // "gv" or "lv"
  theme:"brand",                                 // "brand" | "amber" | "brand-highlight" | "amber-highlight"
  name:"Print Only", name_es:"Solo Impresa",
  price:"$36",
  period:"per year (12 issues)", period_es:"por año (12 ediciones)",
  features:[
    { ok:true,  text:"12 monthly print issues mailed",   text_es:"12 ediciones impresas mensuales por correo" },
    { ok:true,  text:"Stories from AA members worldwide", text_es:"Historias de miembros de AA en todo el mundo" },
    { ok:false, text:"No digital/app access",             text_es:"Sin acceso digital/app" },
  ],
  ctaUrl:"https://www.aagrapevine.org/store/us-subscriptions",
  ctaLabel:"Subscribe", ctaLabel_es:"Suscribirse",
  badge:null, badge_es:null,                     // optional ribbon e.g. "Best Value" / "Promo"
},
```

| Field | What it controls |
|---|---|
| `section` | `"gv"` puts the card under the Grapevine section header; `"lv"` under La Viña |
| `theme` | Color: `brand` = blue, `amber` = orange, `*-highlight` adds a colored ring |
| `price` | Big number shown (any string — `$36`, `$2.99`, `$69`, etc.) |
| `features` | List of bullet items. Set `ok:false` to render an X icon (e.g. "No app access") |
| `badge` | Optional ribbon at top of card (e.g. `"Best Value"`, `"Promo"`). Set to `null` for no ribbon |
| `ctaUrl` | URL the Subscribe button opens |

Current pricing reference: [aagrapevine.org/store/us-subscriptions](https://www.aagrapevine.org/store/us-subscriptions)

#### Update Section Headers

The "AA Grapevine" and "La Viña" group headers above the tier cards are in `SUBSCRIPTION_SECTIONS`:

```js
const SUBSCRIPTION_SECTIONS = {
  gv: { icon:"bi-journal-richtext", iconBg:"bg-brand-50 text-brand-600",
        name:"AA Grapevine", name_es:"AA Grapevine",
        tagline:"Monthly magazine — print, digital, or both",
        tagline_es:"Revista mensual — impresa, digital o ambas" },
  lv: { ... },
};
```

#### Update the Gift Subscription Card

The gift card next to the LV tiers is `SUBSCRIPTION_GIFT`:

```js
const SUBSCRIPTION_GIFT = {
  icon:"bi-gift",
  title:"Gift Subscriptions & Carry the Message", title_es:"Suscripciones de Regalo y Lleva el Mensaje",
  body:"Give the gift of Grapevine or La Viña...", body_es:"Regala una suscripción...",
  bullets:[
    { text:"Anniversary gifts", text_es:"Regalos de aniversario" },
    ...
  ],
  ctaUrl:"https://www.aagrapevine.org/carry-the-message",
  ctaLabel:"Carry the Message", ctaLabel_es:"Lleva el Mensaje",
  ctaIcon:"bi-heart",
};
```

#### Update Subscription Phone Numbers

The phone numbers shown at the bottom of the Subscribe page live in `SUPPORT_CONTACT`:

```js
const SUPPORT_CONTACT = {
  prompt:"Need help with subscriptions?", prompt_es:"¿Necesitas ayuda con suscripciones?",
  lines:[
    { label:"USA:",           label_es:"EE.UU.:",        value:"(800) 631-6025" },
    { label:"International:", label_es:"Internacional:", value:"+1 (570) 567-0437" },
    { label:"En Español:",    label_es:"En Español:",    value:"(800) 640-8781" },
  ],
};
```

Add or remove `lines` entries freely — the card auto-resizes.

---

### Add a YouTube Video

Find `const YOUTUBE_VIDEOS = [` and add:

```js
{ id: "VIDEO_ID", title: "Video Title" },
```

The `VIDEO_ID` is the part after `v=` in a YouTube URL.
Example: `youtube.com/watch?v=ABC123` → ID is `"ABC123"`

Videos are organized in sections:
- Original curated videos at the top
- Podcast episodes by season
- Personal stories
- La Vina (Spanish) videos
- Informational videos

Add new videos to the appropriate section.

---

### Add a Podcast Episode

Find `const PODCAST_EPISODES = [` and add:

```js
{ id: "EPISODE_ID", title: "Episode Title" },
```

Find episode IDs at the [AA Grapevine Apple Podcasts page](https://podcasts.apple.com/us/podcast/aa-grapevines-podcast/id1591924167) — open any episode and copy the numeric value after `?i=` in the URL (e.g. `1000756687022`). Apple's embed plays full episodes anonymously, unlike Spotify's 30-second preview.

---

### Add an Instagram Post

Find `const INSTAGRAM_POSTS = [` and add the post shortcode:

```js
"POST_SHORTCODE",
```

The shortcode is the part after `/p/` in an Instagram URL.
Example: `instagram.com/p/ABC123/` → shortcode is `"ABC123"`

---

### Add a Timeline Milestone

Find `const TIMELINE = [` and add in chronological position:

```js
{
  year: "2026",
  title: "Milestone Title",
  desc: "Description of what happened.",
  type: "grapevine"
},
```

**type** must be one of: `"grapevine"`, `"lavina"`, or `"both"`

The timeline appears on the About page with filtering by type and decade grouping.

---

### Add a Resource Link

Find `const RESOURCES = [` and add:

```js
{
  title: "Resource Name",
  url: "https://example.com",
  icon: "bi-globe",
  description: "Short description.",
  cat: "sites"
},
```

**cat values** (determines which section the link appears in):

| Value | Section |
|-------|---------|
| `"sites"` | Grapevine & La Vina |
| `"digital"` | Digital Tools & Apps |
| `"involve"` | Get Involved |
| `"gvr"` | GVR / RLV Tools |
| `"listen"` | Listen & Follow |
| `"aa"` | AA & NETA 65 |

Icon names from [icons.getbootstrap.com](https://icons.getbootstrap.com) — use the `bi-` prefix.

---

### Update Page Headers (Heroes)

The big gradient banner at the top of every page is driven by the `PAGE_HEROES` object. To rename a page or change its subtitle, edit only this object — no template editing required.

```js
const PAGE_HEROES = {
  about: { icon:"bi-info-circle-fill",
           title:"About Grapevine & La Viña", title_es:"Acerca de Grapevine y La Viña",
           sub:"AA's Meeting in Print — 80+ years of history, {milestones} milestones",
           sub_es:"La Reunión Impresa de AA — Más de 80 años de historia, {milestones} hitos" },
  events: { icon:"bi-calendar-event-fill",
            title:"Events", title_es:"Eventos",
            sub:"{up} upcoming · {pa} past", sub_es:"{up} próximos · {pa} pasados" },
  ...
};
```

- `icon` — any [Bootstrap Icon](https://icons.getbootstrap.com) name (`bi-` prefix)
- `title` / `title_es` — page title (HTML allowed)
- `sub` / `sub_es` — subtitle. Curly-brace `{placeholders}` are filled in by the render function with values like the upcoming-event count or milestone count
- The `home` page has a custom layout with countdown + CTAs but still pulls its title/sub from `PAGE_HEROES.home`

---

### Update Home Page Cards

The two grids of dashboard cards on the Home page are arrays — `HOME_QUICK_CARDS` (top row) and `HOME_BROWSE_CARDS` (lower grid). To add, remove, or reorder a card, edit the array.

```js
const HOME_QUICK_CARDS = [
  { id:"meeting", icon:"bi-camera-video-fill", bg:"bg-sky-50 text-sky-600",
    title:"Next Meeting", title_es:"Próxima Reunión",
    desc:"{date}<br>{time}",         desc_es:"{date}<br>{time}",
    count:"Zoom: {meetingId}",       count_es:"Zoom: {meetingId}" },
  ...
];
```

| Field | Notes |
|---|---|
| `id` | Page id the card navigates to (must match a `NAV_SECTIONS.id`) |
| `icon` | Bootstrap Icon class (e.g. `bi-camera-video-fill`) |
| `bg` | Tailwind classes for the icon background and color (e.g. `"bg-sky-50 text-sky-600"`) |
| `title` / `title_es` | Card title |
| `desc` / `desc_es` | Card description. May include `{placeholders}` filled at render time |
| `count` / `count_es` | Optional small badge text below the description |

The placeholders available for each card are listed inside `renderHome()` in the `quickVars` and `browseVars` objects. Currently:

| Card id | Available placeholders |
|---|---|
| `meeting` | `{date}`, `{time}`, `{meetingId}` |
| `events` | `{nextLine}` (next event title + date), `{n}` (count of upcoming) |
| `documents` | `{r}` (report count), `{n}` (notes count) |
| `photos` | `{p}` (photo count) |
| `resources` | `{n}` (link count) |

---

### Update "What You Can Submit" Cards (Contribute Page)

The three cards on the Contribute page describing what to send come from `SUBMISSION_TYPES`:

```js
const SUBMISSION_TYPES = [
  { icon:"bi-journal-text",
    title:"Stories", title_es:"Historias",
    body:"Most articles are first-person accounts...",
    body_es:"La mayoría de los artículos son relatos en primera persona...",
    note:"Emotional Sobriety, Sponsorship, ...",      // optional small subtext
    note_es:"Sobriedad Emocional, Padrinazgo, ..." },
  ...
];
```

Add or remove cards freely. The grid auto-flows.

---

### Update Submission Methods (GV / LV)

The "How to Submit" and "Contribute to La Viña" boxes on the Contribute page come from `SUBMIT_CHANNELS`. Each entry is one full block with its own heading, intro, numbered methods, footer note, and optional extra CTA.

```js
const SUBMIT_CHANNELS = {
  gv: {
    theme:"brand",                                  // "brand" (blue) or "amber"
    heading:"How to Submit", heading_es:"Cómo Enviar",
    headingIcon:"bi-send",
    items:[
      { num:1, label:"Online (easiest)", label_es:"En línea (lo más fácil)",
        text:"aagrapevine.org/share", url:"https://www.aagrapevine.org/share" },
      { num:2, label:"Email", label_es:"Correo electrónico",
        text:"editorial@aagrapevine.org", url:"mailto:editorial@aagrapevine.org" },
      { num:3, label:"Mail", label_es:"Correo postal",
        text:"Grapevine Editorial, 475 Riverside Drive, New York, NY 10115",
        url:"" },                                   // empty url = plain text (no link)
    ],
    footer:"Include your full name, address, phone, and email...",
    footer_es:"Incluye tu nombre completo...",
  },
  lv: { ... same shape, plus optional `intro` paragraph and `extraCta` ... },
};
```

To change the GV mailing address, edit `SUBMIT_CHANNELS.gv.items[2].text`. To change the LV email, edit `SUBMIT_CHANNELS.lv.items[1]`. Each `item` can be a clickable link (`url:"..."`) or plain text (`url:""`).

---

### Update GVR / RLV Postcards & Flyers

The GVR Corner page has four tabs of downloadable materials:
1. **GV Postcards** — English promotional postcards from aagrapevine.org
2. **LV Tarjetas Postales** — Spanish promotional postcards from aalavina.org
3. **GV Tools & Forms** — English catalogs, flyers, and forms
4. **LV Recursos & Formularios** — Spanish resources and forms

These are hardcoded links in the `renderGVR()` function. To update:
1. Search for `renderGVR` in the file
2. Find the tab section you want to update (look for `id="gvr-gvpc"`, `id="gvr-lvpc"`, `id="gvr-gvtool"`, or `id="gvr-lvtool"`)
3. Copy an existing link block and update the URL, title, and description
4. New postcards/flyers are published at [aagrapevine.org/gvr-resources](https://www.aagrapevine.org/gvr-resources) and [aalavina.org/recursos](https://www.aalavina.org/recursos)

---

## Language / Translation (EN ↔ ES)

The website is fully bilingual. Users click the **ES/EN** button in the header to switch languages.

### How Translation Works

The site uses **two complementary translation mechanisms**:

1. **Inline strings** — `t("English text", "Spanish text")` is used inside render functions for one-off labels, button text, empty-state messages, etc. It returns the right string based on the current language.

2. **Data-array fields** — Each entry in `ANNOUNCEMENTS`, `SPECIAL_EVENTS`, `RESOURCES`, `TIMELINE`, `PAGE_HEROES`, `HOME_QUICK_CARDS`, `SUBSCRIPTION_TIERS`, `SUBMISSION_TYPES`, `SUBMIT_CHANNELS`, etc. carries both languages with the suffix convention `field` (English) and `field_es` (Spanish). The helper `tx(obj, "field")` automatically picks the right one based on the current language. When you add a new entry to any data array, always include both the plain and `_es` fields.

Additionally:

- **Dates** automatically format in the correct locale (English or Spanish)
- **Static HTML elements** (header, footer, modal button labels) are updated by the `applyLang()` function using the `I18N` object
- **Navigation labels** are translated via the `NAV_ES` object
- **Language preference** is saved to the browser's localStorage, so it persists between visits
- **Placeholder templates** in `PAGE_HEROES` subtitles and `HOME_QUICK_CARDS`/`HOME_BROWSE_CARDS` text (like `"{n} upcoming"`) are substituted by the `fmt()` helper at render time

### What's Translated

- All page titles, headings, and descriptions
- All button labels (Share, Calendar, Copy, Close, etc.)
- Navigation menu items
- Countdown timer labels (Days, Hours, Min, Sec)
- Date formatting (months appear in Spanish when ES is active)
- Relative dates ("Today", "Tomorrow", "In X days")
- Footer text and copyright
- Modal buttons (event detail, PDF viewer)
- Toast messages (clipboard feedback)

### What Stays in English/Spanish

Some items intentionally remain in their original language:
- **Product names**: "AA Grapevine", "La Vina", book titles
- **PDF document titles**: Match the actual PDF filename/title
- **GVR postcard titles**: Match the official postcard names from aagrapevine.org
- **Resource link titles**: Many are proper names of websites or products
- **La Vina contribution section**: The submission instructions for La Vina are in Spanish since La Vina is a Spanish publication

### Adding New Translated Content

**For a new data-array entry** (the common case — announcements, events, resources, subscription tiers, etc.), include both language fields:

```js
{ title: "English title", title_es: "Título en español",
  body:  "English body",  body_es:  "Cuerpo en español" }
```

Any field the render code pulls via `tx(obj, "field")` will automatically fall back to the English version if `field_es` is empty, so incomplete translations fail gracefully instead of blanking.

**For a new inline string inside a render function**, use the `t()` helper:

```js
t("English text here", "Spanish text here")
```

**For a new static element** in the header, footer, or modal (text that doesn't come from a render function), add an entry to the `I18N` object used by `applyLang()`:

```js
const I18N = {
  my_key: { en: "English", es: "Spanish" },
  ...
};
```

Then update `applyLang()` to apply your new key to its target element.

---

## File Naming Rules

If storing files locally (not on Google Drive):

| Folder | Pattern | Example |
|--------|---------|---------|
| `reports/` | `report-YYYY-MM.pdf` | `report-2026-04.pdf` |
| `notes/` | `notes-YYYY-MM.pdf` | `notes-2026-04.pdf` |
| `slides/` | `slides-YYYY-MM.pdf` | `slides-2026-04.pdf` |
| `flyers/` | `descriptive-name.pdf` | `spring-assembly-2026.pdf` |
| `photos/` | `descriptive-name.jpg` | `booth-spring-2026.jpg` |

Rules: lowercase, hyphens instead of spaces, no special characters.

---

## BASE_PATH Setting

Find `const BASE_PATH = "";` near the top of the script.

| Scenario | Value |
|----------|-------|
| Testing locally (double-click file) | `""` |
| GitHub Pages (repo URL) | `"/GV_NETA65"` |
| Custom domain (grapevine.neta65.org) | `""` |

---

## Website Pages

| Page | Menu Label (EN) | Menu Label (ES) | What's on it |
|------|----------------|-----------------|-------------|
| Home | Home | Inicio | Dashboard cards, announcements, media preview, countdown timer |
| Meeting | Meeting | Reunion | Schedule, Zoom details, chair contact, copy-to-clipboard |
| Events | Events | Eventos | Upcoming/past events, flyer links, calendar export, share |
| Subscribe | Subscribe | Suscribirse | GV & LV pricing, gift subscriptions, phone numbers |
| Contribute | Contribute | Contribuir | How to submit stories, editorial calendar with deadlines |
| About | About GV/LV | Acerca de GV/LV | History, timeline (40+ milestones), humor books, service structure |
| GVR Corner | GVR Corner | Rincon del RLV | GVR/RLV role, responsibilities, downloadable guides & postcards |
| Documents | Documents | Documentos | Reports, notes, slides with inline PDF viewer |
| Photos | Event Gallery | Galeria de Eventos | Auto-cycling photo gallery with captions |
| Listen & Watch | Listen & Watch | Escuchar y Ver | Podcast, YouTube, Instagram embeds |
| Resources | Resources | Recursos | Categorized links to external AA & Grapevine sites |

---

## What GVRs and RLVs Need to Know

This website is designed to be a **one-stop resource** for Grapevine Representatives (GVRs) and La Vina Representatives (RLVs). Here's what's available:

### For GVRs (English)

- **GVR Corner page**: Role description, responsibilities checklist, and ideas for promoting Grapevine at your homegroup
- **Downloadable guides**: GVR Handbook, GV Workbook, P-52 Pamphlet
- **Postcards & flyers**: 20+ printable promotional materials (Carry the Message, podcast, apps, books, etc.)
- **Registration link**: Register as a GVR at aagrapevine.org
- **Carry the Message**: Info on sponsoring gift subscriptions for facilities
- **Editorial calendar**: Current topics and deadlines for story submissions
- **Subscription info**: Current pricing for print, digital, and bundle options

### For RLVs (Spanish)

- **Rincon del RLV**: Same content as GVR Corner, fully translated
- **Manual del RLV**: Official RLV handbook from aalavina.org
- **Libro de Trabajo LV**: La Vina workbook
- **Tarjetas Postales**: Spanish-language promotional postcards
- **Registration link**: Register as an RLV at aalavina.org
- **Lleva el Mensaje**: Spanish version of the Carry the Message project

### For District Chairs

- **Meeting page**: Zoom info with one-click copy for sharing with district members
- **Events page**: All upcoming events with share buttons
- **Documents page**: Access to all committee reports, notes, and slides
- **Announcements**: Shareable announcements that can be forwarded to groups

### Key External Links Included

| Resource | URL | Purpose |
|----------|-----|---------|
| GVR Resources | aagrapevine.org/gvr-resources | Official GVR materials |
| RLV Recursos | aalavina.org/recursos | Official RLV materials |
| Submit a Story | aagrapevine.org/share | Story submission portal |
| Editorial Calendar | aagrapevine.org/contribute | Upcoming topics & deadlines |
| Carry the Message | aagrapevine.org/carry-the-message | Gift subscription program |
| GV Podcast | aagrapevine.org/grapevine-variety-hour | Free weekly podcast |
| GV Weekly Open Meeting | aagrapevine.org/grapevine-weekly-open | Live Zoom meeting info |
| Sobriety Calculator | aagrapevine.org/sobriety-calculator | Free sobriety date tool |
| GV App | aagrapevine.org/apps | Mobile app download |
| NETA 65 | neta65.org | Area website |
| GV/LV Committee | neta65.org/trusted-servants/grapevine-la-vina/ | Official committee page |

---

## Monthly Checklist

After each committee meeting, do these steps:

- [ ] Upload report PDF to Google Drive `reports/` folder (or local `reports/`)
- [ ] Upload meeting notes PDF to `notes/` folder
- [ ] Upload slides PDF to `slides/` folder
- [ ] Open `index.html` in your text editor
- [ ] Add new entry to `REPORTS` array (at the top)
- [ ] Add new entry to `MEETING_NOTES` array (at the top, include date and summary)
- [ ] Add new entry to `MEETING_SLIDES` array (at the top)
- [ ] Add any new announcements to `ANNOUNCEMENTS`
- [ ] Add any new special events to `SPECIAL_EVENTS`
- [ ] Add any new booth photos to `BOOTH_PHOTOS`
- [ ] Remove old announcements that are no longer relevant (though they auto-hide after 90 days)
- [ ] Save the file and test locally (double-click `index.html`)
- [ ] Test the Spanish version (click ES button) to make sure everything looks right
- [ ] Push to GitHub

---

## Quarterly Checklist

- [ ] Check that all Google Drive sharing permissions are still active
- [ ] Review upcoming events in `SPECIAL_EVENTS` — remove past events if desired
- [ ] Add any new YouTube videos or podcast episodes
- [ ] Check the GVR/RLV postcard links — aagrapevine.org occasionally updates these
- [ ] Verify the Zoom meeting link and passcode are still current
- [ ] Update the `WEEKLY_OPEN` info if the GV Weekly Open Meeting details change

---

## Annual Checklist

- [ ] Update `EDITORIAL_CALENDAR` from [aagrapevine.org/contribute](https://www.aagrapevine.org/contribute) — add the new year's topics
- [ ] Verify subscription prices and update `SUBSCRIPTION_TIERS` if changed (check [aagrapevine.org/store/us-subscriptions](https://www.aagrapevine.org/store/us-subscriptions))
- [ ] Update phone numbers in `SUPPORT_CONTACT` if they've changed
- [ ] Add new YouTube videos and podcast episodes
- [ ] Review `RESOURCES` links for broken URLs — click each one to verify
- [ ] Add new timeline milestones to `TIMELINE` if applicable
- [ ] Verify Google Drive sharing permissions are still active on all folders
- [ ] Check if aagrapevine.org has new postcards/flyers and update the GVR Corner tabs
- [ ] Review the `ANNOUNCEMENTS` array and clean out anything outdated
- [ ] Update the GV Workbook link if a newer version is published (check [aagrapevine.org/gvr-resources](https://www.aagrapevine.org/gvr-resources))
- [ ] Check for new GV/LV catalog PDFs and update their entries in `RESOURCES` — the Subscribe page reads the catalog buttons from `RESOURCES` automatically

---

## Transition to a New Committee Chair

When the Grapevine/La Vina Committee Chair rotates:

1. **Update `MEETING_INFO`** — change `chair` and `chairEmail` fields
2. **Update Zoom info** — if the new chair uses a different Zoom account, update `zoomLink`, `meetingId`, and `passcode`
3. **Transfer Google Drive access** — share the Google Drive folders with the new chair and grant Editor permissions
4. **Transfer GitHub access** — add the new chair as a collaborator on the GitHub repository (Settings > Collaborators)
5. **Walk them through this README** — especially the [Quick Start](#quick-start) and [Monthly Checklist](#monthly-checklist)

---

## Deploy to GitHub Pages

1. Create a GitHub repository (e.g., `GV_NETA65`)
2. Push all files to the `main` branch
3. Go to **Settings > Pages > Source**: Deploy from branch > `main` > `/ (root)`
4. Site goes live at `https://yourusername.github.io/GV_NETA65/`

### Custom Domain (grapevine.neta65.org)

1. In repo **Settings > Pages > Custom domain**: enter `grapevine.neta65.org`
2. Add a **CNAME** DNS record: `grapevine` → `yourusername.github.io`
3. GitHub auto-creates a `CNAME` file
4. Set `BASE_PATH = ""` in index.html
5. Enable **Enforce HTTPS** in the Pages settings

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Website is blank | Check for missing commas or quotes in the config section. Open browser console (F12) for errors. |
| Document link doesn't work | Make sure the filename matches exactly (case-sensitive) or the Google Drive link is correct. |
| Photos don't show | Check the filename in `BOOTH_PHOTOS` matches the actual file. Google Drive links must be direct sharing links. |
| Google Drive buttons not showing | Make sure the folder URL is pasted between the quotes in `GOOGLE_DRIVE`. |
| Changes not showing on live site | Clear your browser cache (Ctrl+Shift+R) or wait a few minutes for GitHub Pages to update. |
| Spanish translation missing | Make sure the text uses `t("English","Spanish")` wrapper. See [Language section](#language--translation-en--es). |
| Countdown shows "coming soon" | The meeting date may have passed. The countdown auto-advances to the next 3rd Wednesday. |
| PDF viewer shows blank | The file is not publicly shared. Open it in Drive → Share → set to "Anyone with the link → Viewer". |
| Drive PDF won't preview inside the modal | Make sure the URL is the actual Drive sharing link (contains `/file/d/...` or `?id=...`). The site auto-detects all standard sharing-link formats. |
| Drive image shows as broken icon | Image must be publicly shared AND must be a real image file (jpg/png), not a Google Doc. The site fetches images via Drive's `thumbnail` endpoint. |
| "Forbidden" or 403 on a Drive file | Sharing was changed or the file was moved. Re-copy the share link and re-paste it into the array. |
| Events not showing | Check that the `date` field is in `YYYY-MM-DD` format. Future events show under "Upcoming." |
| YouTube video thumbnail broken | Verify the video ID is correct. Private or deleted videos won't show thumbnails. |
| Instagram embeds not loading | Instagram embeds may be blocked by ad blockers. This is normal. |
| Sidebar menu shows wrong language | Click the ES/EN toggle button — the sidebar rebuilds when language changes. |

### How to Debug

1. Open `index.html` in your browser
2. Press **F12** to open Developer Tools
3. Click the **Console** tab
4. Look for red error messages — they usually point to the exact line with the problem
5. Common errors:
   - `Unexpected token` — missing comma or quote
   - `Unexpected end of input` — missing closing brace `}` or bracket `]`
   - `is not defined` — typo in a variable name

---

## Technical Details

- **Single HTML file** — all CSS, JS, and content in one file (~270KB)
- **No build tools** — no npm, no bundler, no server needed
- **CDN dependencies:** Tailwind CSS (Play CDN), Bootstrap Icons, Google Fonts (Inter)
- **SPA routing** via `hashchange` — browser back/forward works, bookmarkable URLs
- **Bilingual:** Full EN/ES toggle with localStorage persistence
- **Google Drive aware:** `driveFileId()` / `driveUrl()` auto-transform any Drive sharing-link format into the right endpoint for iframes, images, and downloads
- **Offline-capable structure:** Content renders from local data arrays; the only external dependencies are the CDN CSS/fonts and embedded media (Apple Podcasts, YouTube, Instagram)

### Responsive design

Tested and working from **320px** (iPhone SE portrait) up to **2560px+** (ultra-wide desktop). Key details:

- Single set of Tailwind breakpoints (`sm` 640, `md` 768, `lg` 1024, `xl` 1280) — every grid uses `grid-cols-1 sm:grid-cols-2 …` patterns to collapse gracefully
- Mobile-first sidebar navigation (slides in from the right with `max-w-[85vw]`)
- Page content is capped at `max-w-[1600px]` so it stays readable on 4K/5K monitors
- Header is transparent over page heroes, solid on scroll, and stacks tightly on narrow viewports (brand subtitle hides below 400px wide)
- Home page hero uses a 2-col grid above `md` (title + countdown) and stacks on mobile
- Timeline collapses from its desktop alternating left/right layout to a single left-aligned rail on `< md` via dedicated mobile CSS
- Modals (`max-h-[90vh]`) scroll internally on small screens instead of clipping
- `body { overflow-x: hidden }` and `p, li, td { overflow-wrap: break-word }` guarantee no accidental horizontal scroll from long URLs or wide content
- `html { scroll-padding-top: 80px }` so `#anchor` jumps clear the fixed header

### Accessibility

Built to meet WCAG 2.1 Level AA where reasonable:

- **Skip-to-content link** — first element in the tab order
- **ARIA labels** on every icon-only button (menu, lang toggle, close, prev/next, etc.)
- **Semantic HTML** — `<header>`, `<nav>`, `<footer>`, `<button type="button">`, proper heading hierarchy
- **`:focus-visible` ring** — 2px brand-blue outline shown only for keyboard focus (not mouse clicks); follows each element's own border-radius
- **44×44 touch targets** — gallery dots/arrows, sidebar nav items, modal close buttons all meet the WCAG minimum
- **Reduced-motion support** — all animations and transitions collapse to 0.01ms when the user sets `prefers-reduced-motion: reduce`
- **iOS safe-area-inset** — the floating "back-to-top" button, sidebar, and footer respect the home-indicator safe area on notched iOS devices
- **iOS Safari auto-zoom protection** — `text-size-adjust:100%` stops Safari from enlarging text on rotate
- **`loading="lazy"`** on photos and YouTube thumbnails
- **Keyboard shortcut**: `Esc` closes the sidebar, event modal, and PDF modal

### Configuration Arrays Reference

| Array/Object | Location | Purpose |
|-------------|----------|---------|
| `BASE_PATH` | Line ~233 | URL prefix for local file paths |
| `GOOGLE_DRIVE` | Line ~240 | Google Drive folder links (shown as "View on Drive" buttons) |
| `NAV_SECTIONS` | Line ~247 | Navigation menu items and icons |
| `ANNOUNCEMENTS` | Line ~260 | Time-sensitive announcements (auto-expire 90 days) |
| `MEETING_INFO` | Line ~266 | Committee meeting Zoom details + chair contact |
| `WEEKLY_OPEN` | Line ~276 | GV Weekly Open Meeting Zoom details |
| `SPECIAL_EVENTS` | Line ~293 | Non-recurring events (assemblies, workshops, etc.) |
| `REPORTS` | Line ~301 | Monthly committee report PDFs |
| `MEETING_NOTES` | Line ~311 | Monthly meeting notes with summaries |
| `MEETING_SLIDES` | Line ~317 | Monthly meeting slide decks |
| `BOOTH_PHOTOS` | Line ~323 | Event and booth photo gallery |
| `RESOURCES` | Line ~331 | Categorized external links shown on Resources page |
| `EDITORIAL_CALENDAR` | Line ~370 | GV submission topics and deadlines |
| `TIMELINE` | Line ~398 | Historical milestones for About page |
| `APPLE_SHOW_ID` / `APPLE_SHOW_SLUG` | Line ~440 | Apple Podcasts show identifier (for embeds) |
| `YOUTUBE_VIDEOS` | Line ~442 | YouTube video IDs and titles |
| `PODCAST_EPISODES` | Line ~577 | Apple Podcasts episode IDs and titles |
| `INSTAGRAM_POSTS` | Line ~596 | Instagram post shortcodes |
| `PAGE_HEROES` | Line ~612 | Hero banner title + subtitle for every page (en/es) |
| `HOME_QUICK_CARDS` | Line ~632 | Home page action cards (top row) |
| `HOME_BROWSE_CARDS` | Line ~638 | Home page navigation cards (lower grid) |
| `SUBSCRIPTION_TIERS` | Line ~654 | Subscribe page pricing cards (GV + LV) |
| `SUBSCRIPTION_SECTIONS` | Line ~718 | Subscribe page section headers (GV / LV groupings) |
| `SUBSCRIPTION_GIFT` | Line ~723 | Subscribe page gift / Carry the Message card |
| `SUPPORT_CONTACT` | Line ~743 | Subscribe page phone numbers |
| `SUBMISSION_TYPES` | Line ~755 | Contribute page "What You Can Submit" cards |
| `SUBMIT_CHANNELS` | Line ~781 | Contribute page submission methods (GV + LV) |
| `NAV_ES` | Line ~893 | Spanish navigation labels |
| `I18N` | Line ~1637 | Static HTML translation strings (header, footer, modals) |

### Helper functions reference

| Function | Purpose |
|---|---|
| `t("English","Español")` | Picks the right inline string based on the current language |
| `tx(obj,"field")` | Picks `obj.field_es` when in Spanish mode, else `obj.field`. Used by all data-array render code |
| `fmt(str, vars)` | Replaces `{key}` placeholders in a string with `vars[key]`. Used for hero subtitles and home cards |
| `heroHtml(key, vars)` | Builds the standard gradient page hero from a `PAGE_HEROES` entry |
| `fp(folder, name)` | Returns full URL if `name` is already an `http(s)://` URL, else builds a local path |
| `driveFileId(url)` | Extracts the Drive file ID from any standard sharing-link format. Returns `null` if not a Drive URL |
| `driveUrl(url, mode)` | Transforms a Drive URL to the right format for the use case (`view`, `preview`, `image`, `download`). Pass-through for non-Drive URLs |

### Translation pattern

Every entry in the data arrays above carries both languages with the
suffix convention `field` (English) and `field_es` (Spanish). The
helper `tx(obj, "field")` automatically picks the right one based on
the current language. Render functions use `tx()` for object fields
and `t("English","Español")` for inline strings. Subtitle templates
inside `PAGE_HEROES` use `{placeholder}` syntax for runtime values
(e.g. `"{up} upcoming · {pa} past"`) which are substituted by `fmt()`.
