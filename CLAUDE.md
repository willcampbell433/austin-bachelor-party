# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-page, static HTML site for a bachelor party trip ("So Long Partner") to Austin, TX, April 23-26, 2026. The page serves as a hub for the 11-person crew with the itinerary, logistics (Airbnb code, address, host info), waivers, links (Venmo, photo album, Google Maps), gun-range loadouts, and a few interactive gags (shot roulette, emoji rain, "test fire" flash).

## Architecture

The entire project is one file: `index.html`. It contains:

- **HTML structure** — the page sections (SOS button, waivers, squad list, logistics, day-by-day itinerary, rules, shot roulette, armory, photo dump).
- **`<style>` block** — all CSS is inline at the top of the file. The aesthetic is intentional: retro/Western/arcade — orange (`#ff6b35`), navy (`#004e89`), cream (`#f7c59f`) on a dark maroon (`#1a0f14`) gradient, Courier New monospace, `<marquee>` tags, dashed borders, hard drop-shadow buttons, hover rotations.
- **`<script>` block** — all JS is inline at the bottom. Five small functions (`checkShot`, `makeItRain`, `whoOwesGroom`, `clearDebt`, `testFire`) wired up via `onclick` attributes directly on elements. No framework, no modules, no build step.

There is no `package.json`, no bundler, no test suite, no linter config, and no backend. There are no external JS or CSS dependencies — only outbound `<a href>` links to third-party services (Airbnb, FareHarbor/SmartWaiver waivers, Google Maps, Venmo, iCloud shared album, Party On Delivery).

## Running / Previewing

Open `index.html` directly in a browser, or serve it locally:

```sh
python3 -m http.server 8000
# then visit http://localhost:8000
```

There is nothing to build or compile.

## Conventions

- **Keep everything in `index.html`.** Don't introduce a build system, framework, external CSS/JS files, or split into components unless explicitly asked. The single-file constraint is the design.
- **Inline event handlers** (`onclick="..."`) are the established pattern for new interactivity — match it rather than adding `addEventListener` blocks.
- **Reuse existing CSS classes** (`.btn`, `.day`, `.info-box`, `.warning`, `.crew-member`, `.loadout-card`) and the established palette before adding new styles. New buttons typically override colors via inline `style="background:...; border-color:..."` on top of `class="btn"`.
- **Tone is irreverent and chaotic** (emojis, all-caps warnings, jokes about the "Rainey Street Ripper", "HYDRATE OR DIE"). Preserve it when editing copy.
- **Real, load-bearing data lives in this file** — Airbnb door code (5215), address (901 Spence St), Sam's phone number, Venmo handle, waiver URLs, marina dock, Fetii pickup times. Treat changes to those values like config changes: only edit when the user gives you the new value, and don't invent or "tidy up" them.

## Git Workflow

Commit messages in this repo are short, imperative, and describe the user-visible change (e.g. "Move SOS button to the top of the page", "Add Waymo only rule to Rules of Engagement"). No prefix conventions, no body, no issue refs. Match that style.
