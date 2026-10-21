# Clean-Label & E-Number Replacement Finder v1.0 — Test Report

**What it is:** A single-file browser app for the Asif SaaS Studio catalogue: a curated, searchable knowledge base of **36 additives and 79 natural replacement swaps** that helps food formulators reformulate away from synthetic additives. Each additive carries its E-number, function(s), typical applications, origin, the factual reason brands move away from it, and status notes; each replacement carries its label declaration, an indicative dosage range, a Strong/Partial functional-match grade, best-fit product categories, a one-line regulatory note and the trade-off. Three low-concern entries (citric acid E330, ascorbic acid E300, xanthan gum E415) carry an honest **"keep as-is" verdict** instead of forced swaps. A reformulation-plan builder collects chosen swaps with their declarations for copying or CSV download. By Dr. Asif Ahmad.

## Features

1. **Live search** — matches E-number with or without the "E" (319, e319, E319 all find TBHQ), additive names, function names, and replacement names/declarations (searching "rosemary" or "stevia" finds the additives they can replace). Friendly "no matches" state.
2. **Function filter chips** — All + Preservative, Antioxidant, Emulsifier, Stabiliser & thickener, Colour, Sweetener, Acidity regulator, Raising agent, Flavour enhancer, Anti-caking & humectant.
3. **Product-category selector** — Bakery / Meat & seafood / Beverages / Sauces & dressings / Dairy & alternatives / Snacks / Confectionery. Each replacement card is flagged "Good fit" or "Poor fit" for the chosen category based on its curated best-fit list.
4. **Additive detail panel** — profile (function, uses, origin, why brands move away, status note) plus replacement cards with declaration, dosage (always labelled "starting point — validate in trials"), best fit, regulatory note, trade-off, and an Add-to-plan button. Keep-verdict entries show a green verdict box instead of swap cards.
5. **Reformulation plan** — in-page plan table (replaces → replacement → declaration → dosage → match), duplicate additions rejected, per-row remove, Copy plan (plain text with a validation disclaimer), Download plan CSV, Clear plan. State is page-only; nothing is stored.
6. **Honest-scope banner** — states up front that "clean label" is not a legal category, that natural replacements may carry E-numbers themselves, that preservative/antioxidant efficacy must be proven by challenge tests and shelf-life studies, and that regulatory status varies by market and changes over time.

## Data sources & knowledge basis — and the honesty rules applied

The database was curated from established food-science and regulatory knowledge, not generated numbers:

- **E-number ↔ name ↔ function assignments** follow the EU Union list of food additives (Regulation (EC) No 1333/2008, Annex II) and standard references (Codex GSFA). Anchor assignments were re-verified in testing (E319 TBHQ, E250 sodium nitrite, E171 titanium dioxide, E621 MSG, E1422 acetylated distarch adipate).
- **Status anchors** are matters of public record: E171 titanium dioxide — EFSA's 2021 opinion and removal from EU authorisation in 2022 (still permitted in the US); the "Southampton six" colours (E102, E110, E129 among them) — mandatory EU warning "may have an adverse effect on activity and attention in children"; sulphites — allergen declaration above 10 mg/kg; aspartame — IARC Group 2B (2023) alongside JECFA's retained ADI, worded as a debate, not a ban; EU polyol laxation statement above 10% added polyols.
- **The nitrite entry states the central nuance explicitly, both ways:** celery powder delivers the *same* nitrite chemically; the US (USDA) accepts the "uncured / no nitrates or nitrites added except those naturally occurring" route, while the EU treats vegetable-derived nitrite used for curing as an additive function. Cherry/acerola powder is described correctly as a cure *accelerator* (ascorbate source), not a nitrite source.
- **The MSG entry is equally explicit:** yeast extract, tomato and mushroom swaps keep glutamate — the swap changes the declaration, not the chemistry.
- **Dosages** are conservative, commonly published starting ranges (e.g. rosemary extract 0.02–0.1% on the fat basis, standardised on carnosic acid; cultured wheat flour 0.5–2%; celery powder 0.2–0.5% standardised to nitrite-equivalent targets) and are labelled everywhere as "indicative starting points — validate in trials". No dosage is presented as a guarantee or a legal limit.
- **Regulatory notes** are one-line, hedged guidance ("generally authorised in the EU/US; confirm category limits") — never a claim of legal advice. Where a replacement's status is unsettled (monk fruit and allulose novel-food status in the EU; rice-hull anti-caking naming), the card says so.

**Entries where facts needed care (and how they were hedged):**
- *E150c 4-MEI* — described as a public concern with a California Prop 65 listing for 4-MEI, not as an EU/US ban (there is none).
- *BHA / Prop 65* — worded as "a labelling trigger, not a food ban".
- *Carrageenan* — notes that degraded carrageenan (poligeenan) is a different, non-food substance, and that removal is usually a marketing decision.
- *Stevia* — dosage given for high-purity glycoside grades; notes whole-leaf/crude extracts are not GRAS in the US.
- *Xylitol* — carries the dog-toxicity flag relevant to pet-adjacent products.
- *GSO/regional specifics* — deliberately not asserted; all regulatory notes stay at EU/US level with "confirm locally" hedging.

## File

- `~/workspace/your_files/clean-label-replacement-finder/index.html` — **62,632 bytes** (limit 150 KB), all CSS/JS inline, no external assets, no localStorage/service workers/permissions/parent-window access (grep-verified clean). Responsive; the additive list and detail stack on narrow screens.

## How to run

Open `index.html` in any modern browser (double-click, or paste the file's contents into the Wix CMS `appHtml` field — see below). No build step, no server, no backend, no API keys: the knowledge base is curated data shipped inside the file.

## Testing

**Method:** the app's PURE CORE (database + search/filter/plan logic) was extracted from the page and run in Node against hand-set expectations, including the factual anchors above. Both inline scripts were extracted and syntax-checked with `node --check` — **OK**.

**Results: 69 / 69 checks passed.**

| Group | Checks | Result |
|---|---|---|
| Data integrity — DB size 36, unique E-numbers, format valid (3–4 digits: the modified-starch family is genuinely 4-digit, e.g. E1422), every additive profiled, every additive has ≥1 replacement or a keep verdict, every replacement fully specified (declaration, dosage, Strong/Partial match, valid categories, regulatory note, trade-off) | 10 | ✅ |
| Factual anchors — E319 TBHQ → rosemary (dosage string "0.02…0.1" present), tocopherols, green tea; E250 nitrite → celery with US + EU positions and the "chemically the same nitrite" nuance, all nitrite swaps meat-fit; E171 status cites EU + 2022; E621 MSG with honest glutamate note + yeast extract; E960 stevia replaces ≥2 sweeteners; E322 lecithin appears as a replacement; modified starch → pulse flours; DATEM → lecithin + enzymes; sorbitol → erythritol with laxation note; silica → rice anti-caking; E129 → colouring foods; Southampton warning on tartrazine | 24 | ✅ |
| Keep verdicts — exactly 3 (E330, E300, E415 with fermentation note) | 4 | ✅ |
| Search & filters — "319"/"e319"/"E319" all find TBHQ; replacement-name search (rosemary, stevia, sorbat→E202); nonsense query returns empty; empty query returns all; TBHQ under Antioxidant and NOT under Colour; every function filter returns ≥1 additive; category fit flags (celery fits Meat & seafood, poor fit for Beverages; colouring foods fit Beverages and Confectionery somewhere) | 17 | ✅ |
| Plan builder — 3 adds give 3 unique rows; duplicate rejected; unknown additive/replacement rejected; CSV = header + 3 rows containing the declarations; plan text lists all swaps + challenge-test disclaimer; remove deletes exactly one row; empty-plan text/CSV are friendly | 14 | ✅ |

## Wix upload steps

1. In the Wix dashboard, open the CMS collection **SaasProducts**.
2. Edit (or add) the item with slug `clean-label-replacement-finder`.
3. Paste the full contents of `index.html` into the **appHtml** field; set Title, Category (Food Science), Version 1.0, Published = on.
4. Save, open the live app page, and run the smoke test: the header counts should read **"36 additives · 79 swaps · 3 honest "keep as-is" verdicts"** and the detail panel opens on **E319 TBHQ** — its first replacement card is **Rosemary extract, Strong match, dosage 0.02–0.1% on the fat/oil basis**. Search `250` → **E250 Sodium nitrite** appears with the celery powder swap and the US/EU nuance. Pick function **Colour** → TBHQ disappears, E171 Titanium dioxide is listed. Add the rosemary swap to the plan → the plan table shows 1 row whose declaration mentions rosemary extract (E392).

## Listing

- **Title:** Clean-Label & E-Number Replacement Finder
- **Description:** Search 36 additives and 79 natural swaps — with label declarations, indicative dosages, trade-offs and regulatory notes for clean-label reformulation.
- **Category:** Food Science
- **Slug:** `clean-label-replacement-finder`
- **Version:** 1.0
