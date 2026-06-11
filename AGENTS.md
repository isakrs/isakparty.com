# AGENTS.md — isakparty.com

This file tells any AI agent (Claude, Gemini, GPT, Codex, etc.) how to create and publish a new event page on isakparty.com.

---

## What this site is

A personal event site at isakparty.com. Each event lives at its own path:
- `isakparty.com/summer-party-2025/`
- `isakparty.com/birthday-june/`
- etc.

The homepage (`index.html` at root) lists all events as cards linking to each page.

---

## How to create a new event page

### Step 1 — Choose a slug

Pick a short, lowercase, hyphenated slug for the event. Example: `summer-party-2025`, `office-drinks-june`.

### Step 2 — Create the event folder and files

Create a new folder `<slug>/` at the root. Inside it, create at minimum:
- `index.html` — the full event page (self-contained: all CSS and JS inline or in the same folder)

You may also add:
- `styles.css` — if styles are long enough to warrant a separate file
- `app.js` — if there is meaningful interactivity (animations, charts, etc.)

### Step 3 — Design guidelines

Model the page after this reference: https://vipps.janschill.de/
Key principles:
- Mobile-first, clean, minimal
- Strong typographic hierarchy — big event title, clear date/location
- A hero section at the top that sets the mood (could be a photo, gradient, or SVG illustration)
- Use Google Fonts — Inter is a solid default
- Color palette: pick one or two accent colors that fit the event mood; no more
- If photos are provided, display them in a responsive grid or masonry layout
- If data/results are provided (race times, scores, etc.), visualize them clearly — a table or animated chart
- No JavaScript frameworks — vanilla JS only
- No external dependencies beyond Google Fonts

### Step 4 — Update the homepage

Open `index.html` at the root and add a new event card inside the `<ul class="events">` list. Each card looks like:

```html
<li class="event-card">
  <a href="/<slug>/">
    <span class="event-date">June 2025</span>
    <span class="event-name">Summer Party</span>
  </a>
</li>
```

### Step 5 — Commit and push

```bash
git add <slug>/ index.html
git commit -m "Add <slug> event page"
git push
```

GitHub Pages deploys automatically within about 30 seconds of the push.

---

## Deployment

- Hosted on GitHub Pages, repo: https://github.com/isakrs/isakparty.com
- Branch: `main`, root folder `/`
- Custom domain: `isakparty.com` (configured via `CNAME` file)
- No build step — all files are served as-is

---

## Phone workflow (GitHub Actions)

From a phone or any browser, go to:
`https://github.com/isakrs/isakparty.com/actions/workflows/create-page.yml`

Click **Run workflow**, fill in:
- `prompt` — describe the event in plain language, include any relevant details
- `slug` — the URL slug for the page

The workflow calls an AI model, generates the page, commits it, and deploys it.

---

## Notes for agents

- Always use relative paths (e.g. `href="/summer-party/"`, not absolute URLs)
- Ensure pages are self-contained and work without a local server (no ES module imports from `node_modules`, etc.)
- Test that the page renders correctly on a 375px wide screen (iPhone SE viewport)
- Keep each event page under 100 KB of HTML/CSS/JS combined (excl. images)
