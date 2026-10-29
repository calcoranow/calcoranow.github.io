# Calcora

**Live site: [https://calcoranow.com](https://calcoranow.com)**

Calcora is a collection of online calculators: 386 tools across 17 categories — math, finance, health, unit conversion, time and dates, developer utilities, electronics, physics, astronomy, and more. Open the page and start calculating. No sign-up, nothing to install.

---

## What's inside

| Category | What you'll find |
| --- | --- |
| **Finance** | Mortgages, auto and personal loans, amortization schedules, compound interest, APR / APY, savings and CDs, retirement, VAT, tips, credit card payoff |
| **Math** | General and scientific calculators, percentages, fractions, exponents and logs, roots, ratios, primes, combinations and permutations, quadratic equations, significant figures |
| **Health** | BMI, TDEE and calories, BMR, macros, body fat, protein needs, ideal weight, pregnancy and cycle dates |
| **Conversions** | Length, weight, temperature, volume, area, speed, time, data storage, plus one unified multi-dimension converter |
| **Timers** | Date difference, age, business days, duration arithmetic, world clocks, time zones, countdowns |
| **Computer** | JSON formatting, hashing, Base64, cron expressions, color conversion, aspect ratio, UUIDs, IBAN validation |
| **Electricity** | Ohm's law, power and energy cost, voltage drop, kVA to amps, wire gauge, resistor networks |
| **Physics** | Velocity, acceleration, force, energy, power, pressure, density, free fall |
| **Space** | Orbital period, escape velocity, relativistic time dilation, astronomical distances and angular size |
| **AI** | Model memory footprint, training compute and time, token and API cost, perplexity, learning rate |
| **Geometry** | Area and perimeter of plane shapes, volume and surface area of solids, triangle solving |
| **Statistics** | Mean and variance, distributions, confidence intervals, z and t values, probability |
| **RF & Antenna** | Antenna length, link budget, VSWR, wavelength to frequency |
| **Network** | Subnetting, bandwidth and download time, Wi-Fi channels, port reference |
| **Security** | Password strength and generation, JWT decoding, hash comparison, WebAuthn reference |
| **Education** | GPA conversion, GRE / SAT / ACT score conversion, study time planning, reading level |
| **Everyday** | Square footage, concrete and tile quantities, timesheets, fuel cost, roof pitch, pet age |

Every tool is searchable by name or alias from the homepage search box (typing `hcf` brings up GCD / LCM), and you can browse by category. The full list lives at [/all](https://calcoranow.com/all).

## How it feels to use

- **A result on first load.** Every tool opens with a sensible set of example values already filled in, so you see an answer immediately and watch it update as you change a number.
- **The formula is on the page.** Tools use the standard published formulas for their field — amortizing loan payment, WHO adult BMI bands, Mifflin–St Jeor for metabolism — and say which one they use.
- **Results are shareable.** Your inputs are written into the URL, so you can bookmark a result or send the link to someone and they'll see the same numbers and the same answer. Reloading keeps them.
- **It works on a phone.** Single-column layout; inputs and result panels reflow to the screen width.
- **Nothing gets in the way.** No pop-ups, no "sign in to see your result", no app to download.

## Privacy

All calculations run in your browser. The numbers you type are not uploaded or stored, and there are no accounts. Tools don't use cookies or analytics scripts to build a profile of you. In a shareable link the values sit after the `#` in the URL, which browsers don't send when a page is opened normally.

## A note on the results

Calcora gives estimates and reference figures — useful for day-to-day planning, studying, and quick sanity checks. It is not financial, legal, or medical advice. For contracts, diagnoses, or tax filings, rely on a qualified professional or the official rules.

---

## Changelog

Newest first. Each entry describes what actually shipped, not what was planned.

### 2026-10-29

**Documentation**

- Restructured the README and added this changelog. Tool count corrected from "380+" to 386, which is the real number in the catalog.

### 2026-10-28

**New app icon and favicon set**

- The old mark was a dark green square with two horizontal bars. At 16 px it read as a hamburger menu more than as a calculator, and there was nothing else in the icon set — no touch icon, no manifest, no PWA assets.
- Replaced with a calculator: rounded verdigris square (`#0E6B56`), off-white body, screen, 3×2 keypad.
- Keypad density was tested, not guessed. Nine keys smeared into stripes at 16 px; four looked like a card with a heading. Six is the only count that stays legible from 512 px down to 16 px.
- All assets come from a single SVG, so the icon can't drift between formats: `favicon.svg`, `favicon.ico` (16 / 32 / 48 in one file), `apple-icon.png` (180), `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` (glyph scaled to 78% for Android's safe zone), and `manifest.webmanifest`.
- The navbar and footer mark now render the same glyph, from one component — the tab icon and the site logo can't disagree.

**Footer**

- Added the Twelve Tools "Featured on" badge to the footer's left column, below About / Privacy / All tools. Hotlinked, because directory sites verify placement by image URL; 148×40 with explicit width and height to avoid layout shift; lazily loaded so it costs nothing on first paint.

**Search Console round: seven pages that had impressions but no clicks**

- Ten queries had real impressions and almost no clicks: `weight loss calculator` (160), `cement calculator` (112), `business loan calculator` (87), `unsecured personal loan calculator` (84), `boat loan` (65), `boat payment` (53), `hash identifier` (41), `cement mix calculator` (39), `boat finance` (31), `cross product calculator` (29).
- The cause was structural, not stylistic — three separate problems. Five of the pages had no article at all, just a form and a one-line note. One had an H1 that didn't match the query: `cross product calculator` landed on a page titled *Vector Calculator*. One page was the target of three different queries at once.
- Five pages written from scratch, 900–1,200 words each with a comparison table and nine FAQs: cement, business loan, boat loan, hash identifier, cross product.
- Two pages expanded from roughly 190 words: weight loss, personal loan. The personal loan page now leads with *unsecured*, which is how people actually phrase the search.
- The cross product page's title and H1 became *Cross Product Calculator*; six meta descriptions were rewritten so the query's own wording appears in the snippet.

### 2026-10-23

**Grade Calculator is now a weighted grade calculator**

- The page was titled *Grade Calculator* — the head term — but only asked for four numbers: current grade, weight completed, target grade, final weight. That is a final-exam calculator, a much narrower question than the title promised. Someone with three homework rows to average had nowhere to put them.
- Rebuilt around assignment rows: name, score, weight. It returns a live percentage, a letter grade, and GPA points, up to 16 rows, with weights optional.
- The original "what do I need on the final" calculation is kept as a panel below, with a cleaner formula: `needed = (target − current × (1 − final weight)) ÷ final weight`.
- Blank weights fall back to a plain average; weights that don't sum to 100 are divided by the total entered and labelled as the grade so far, rather than silently normalised.
- Inputs live in the URL like every other tool, so a mid-semester estimate can be bookmarked or sent to someone.

### 2026-10-19

**Freight class was off by one class — corrected**

- The density-to-class lookup used the pre-2025 NMFC scale. NMFTA Docket 2025-1 took effect on 19 July 2025 and replaced it with a 13-step scale, so 9.00 lb/ft³ maps to class 100, not 110. Anyone quoting from the old table was a class high.
- Five classes — 77.5, 110, 150, 200 and 500 — can no longer be derived from density at all; they come only from a specific NMFC item.
- The page was rewritten around the current table, with a section on the classes density can't reach, worked examples of a pallet crossing a class boundary on a one-inch change in height, and the difference between class and rate (class is an input to a quote, not the price).

### 2026-10-18

**SEO content system**

- Established one fixed structure for the article under each calculator: opening paragraphs that state what can be computed, how to calculate it, the formula with each variable solved for, how to use the tool, themed sections with tables, common mistakes, FAQ, related tools.
- FAQs render both as visible text and as `FAQPage` structured data from a single source, so the two can't disagree.
- Fifteen pages written to the standard across finance, health, math and conversions; the format has since been applied to 44 of the 386 tools.
