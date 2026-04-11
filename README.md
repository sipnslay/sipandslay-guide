# Sip & Slay - Creator Guide Site

Static site mom bookmarks on her phone and laptop. All-in-one creator workflow tool.

## What's in it

| Tab | What it does |
|-----|-------------|
| Today's Picks | Daily trending clips from the pipeline, with YouTube + WhatsApp share buttons |
| Checklist | Interactive posting checklist with progress bar (saves state between visits) |
| Hashtags | Tap-to-select hashtag builder with copy + WhatsApp share |
| Captions | Copy-paste caption templates (Hinglish, on-brand) |
| Best Times | Posting schedule (IST) with peak time callouts |
| Tips | Algorithm hacks, do's/don'ts, ranked by impact |
| Overlay Guide | Character placement guide with visual reference + Premiere Pro setup |
| 30-Day Plan | Week-by-week targets for the first month |

## How suggestions get here

The pipeline writes `suggestions.json` when you run:

```bash
python3 pipeline/run.py --site          # just update site
python3 pipeline/run.py --site --send   # update site + email
python3 pipeline/run.py --site --whatsapp  # update site + WhatsApp
```

The site reads `suggestions.json` on page load. No server needed.

## Local preview

```bash
cd personal/mom/guide-site
python3 -m http.server 8080
```

Open http://localhost:8080 in browser.

## Deploy to GitHub Pages

1. Create a repo (e.g. `sipandslay-guide`) under mom's GitHub account (or yours, private)
2. Push the `guide-site/` contents to the `main` branch
3. Settings > Pages > Source: Deploy from branch > `main` > `/` (root)
4. Site goes live at `https://<username>.github.io/sipandslay-guide/`
5. Mom bookmarks this URL on her phone

## Updating daily suggestions

When the pipeline runs (manually or via cron), it writes fresh `suggestions.json`.
For GitHub Pages, you'd push the updated JSON. Or host on any static server where you can update the file.

Simplest daily flow:
1. Run pipeline: `python3 run.py --site --whatsapp --send --to sipnslay.official@gmail.com`
2. Push updated JSON: `cd guide-site && git add suggestions.json && git commit -m "daily picks" && git push`

Phase 2: automate this with a cron job or scheduled agent.
