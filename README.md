# Clean-Label & E-Number Replacement Finder

By **Dr. Asif Ahmad** — Asif SaaS Studio

Category **Food Science** · Version **1.0** · MIT License

A curated, searchable knowledge base of **36 food additives and 79 natural replacement swaps** for clean-label reformulation. Look up any additive by E-number (with or without the "E"), name, function or replacement name; read its profile; and choose swaps that carry their **label declaration, an indicative dosage range, a Strong/Partial functional-match grade, best-fit product categories, a hedged regulatory note and the trade-off — stated plainly**. Three low-concern entries (citric acid E330, ascorbic acid E300, xanthan gum E415) carry an honest **"keep as-is" verdict** instead of forced swaps. A reformulation-plan builder collects chosen swaps for copying or CSV export. **100% in your browser**: no uploads, no accounts, and no data ever leaves your device.

**▶ Live on Asif SaaS Studio:** open the tools catalogue and choose *Clean-Label & E-Number Replacement Finder* (slug `clean-label-replacement-finder`).

## Run it

Open `index.html` in any modern browser — or from this repo via any static host. No build step, no dependencies, no server. The app opens on the additive list with the detail panel showing E319 TBHQ.

## What it does

1. **Live search, four ways** — by E-number (`319`, `e319`, `E319` all find TBHQ; the matcher normalises spaces, hyphens and the leading "E"), by additive name, by function, and by replacement name or declaration (searching "rosemary" or "stevia" finds the additives they can replace). Friendly "no matches" state.
2. **Function filter chips** — All + Preservative, Antioxidant, Emulsifier, Stabiliser & thickener, Colour, Sweetener, Acidity regulator, Raising agent, Flavour enhancer, Anti-caking & humectant. Every filter returns at least one additive.
3. **Product-category fit flags** — choose Bakery / Meat & seafood / Beverages / Sauces & dressings / Dairy & alternatives / Snacks / Confectionery and every replacement card is flagged **"Good fit"** or **"Poor fit"** for that context from its curated best-fit list (celery powder is a meat fit and a beverage nonsense — the flag says so before the swap reaches a plan).
4. **Additive profiles** — E-number, function(s), typical applications, origin, the *factual* reason brands move away (a Prop 65 listing is recorded as a labelling trigger, not a food ban), and a status note with the hard constraints: legal maxima, mandatory warnings, allergen thresholds.
5. **Swap cards, one honest format** — replacement name, **Strong/Partial** match grade, the exact **label declaration** (showing the E-number where the replacement itself has one — E392, E306, E322, E960), an **indicative dosage** always labelled "starting point — validate in trials" ("supplier-guided" where dosing is standardised, e.g. celery powder to a nitrite-equivalent target), a one-line **regulatory note**, and the **trade-off**. Every card has one — a card without a trade-off would be marketing.
6. **The two declaration swaps, named as such** — nitrite → celery powder states in full that celery-derived nitrite *is* nitrite chemically, that the US (USDA) accepts the "uncured / no nitrates or nitrites added except those naturally occurring" route, and that the EU treats vegetable nitrite used for curing as an additive function. MSG → yeast extract states that the swap "changes the declaration, not the glutamate".
7. **Keep-as-is verdicts** — E330 citric acid, E300 ascorbic acid and E415 xanthan gum show a green verdict box explaining why removal would cost pH control, protection or texture for zero label gain — and what the fallback is if an external standard forces the issue.
8. **Reformulation plan builder** — add swaps to an in-page plan table (replaces → replacement → declaration → dosage → match), with duplicate protection and per-row removal; **Copy plan** (plain text, ending with the validation disclaimer), **Download plan CSV**, and Clear. State is page-only; nothing is stored.

## Sources & honest scope

- **Knowledge basis:** E-number ↔ name ↔ function assignments follow the EU Union list of food additives (Regulation (EC) No 1333/2008, Annex II) and standard references (Codex GSFA). Status anchors are matters of public record: E171 titanium dioxide (EFSA 2021 opinion; removed from EU authorisation in 2022; still permitted in the US); the "Southampton six" colours' mandatory EU activity-and-attention warning; sulphite allergen declaration above 10 mg/kg; aspartame's IARC Group 2B (2023) recorded as a debate alongside JECFA's retained ADI; EU polyol laxation statements.
- **Dosages are starting points, never specifications or guarantees.** They are conservative, commonly published ranges for first trials; supplier grades vary and the correct dose is the one established by the user's own trials.
- **Efficacy must be proven, not presumed.** Preservative swaps are graded Partial because fermentates and acids are narrower-spectrum than sorbate/benzoate systems; a reformulated product needs challenge tests and validated shelf-life studies. The exported plan ends with this disclaimer, deliberately.
- **"Clean label" is not a legal category**, and natural replacements may carry E-numbers themselves — the app shows them. Regulatory notes are one-line EU/US-level guidance ("generally authorised; confirm category limits"), never legal advice; regional systems beyond EU/US are deliberately not asserted, and unsettled statuses (monk fruit and allulose novel-food status in the EU) are flagged in the cards rather than resolved by assertion.
- **Regulatory status changes** — the E171 story is the standing example. This database is a snapshot; confirm current status in each destination market.
- No backend is needed or faked — the knowledge base is curated data shipped inside the file: no server, no storage, no API keys.

## Files

- `index.html` — the complete app, self-contained: all CSS and JavaScript inline, 62,632 bytes. No localStorage, no service workers, no browser permissions, no parent-window access — safe in a sandboxed iframe, and it works fully offline.
- `clean-label-replacement-finder-test-report.md` — the full test report: features, data sources and the honesty rules applied, the entries where facts needed care (and how each was hedged), testing summary and the Wix listing details.
- Documentation (PDF) → `docs/clean-label-replacement-finder-docs.pdf`

## Testing

69 automated checks run against the shipped PURE CORE — all passed. Coverage: data integrity (10 — database size exactly 36, E-numbers unique and format-valid, every additive profiled with ≥1 replacement or a keep verdict, every replacement fully specified), factual anchors (24 — TBHQ → rosemary at "0.02…0.1", nitrite → celery with both US and EU positions and the chemical-identity nuance, E171 citing EU + 2022, MSG's honest glutamate note, stevia E960 replacing ≥2 sweeteners, lecithin E322 as a replacement, modified starch → pulse flours, DATEM → lecithin + enzymes, sorbitol → erythritol with the laxation note, silica → rice anti-caking, Southampton warning on tartrazine), keep verdicts (4 — exactly 3: E330, E300, E415), search & filters (17 — "319"/"e319"/"E319" all find TBHQ, replacement-name search, TBHQ under Antioxidant and NOT under Colour, every function filter non-empty, category fit flags), and the plan builder (14 — unique rows, duplicate rejection, CSV shape, disclaimer present, single-row removal, friendly empty states). Both inline scripts passed `node --check`. Full report: `clean-label-replacement-finder-test-report.md`.

**Smoke test:** the header counts read **"36 additives · 79 swaps · 3 honest "keep as-is" verdicts"** and the detail panel opens on **E319 TBHQ** — first card **Rosemary extract, Strong match, dosage 0.02–0.1% on the fat/oil basis**. Search `250` → **E250 Sodium nitrite** with the celery swap and the US/EU nuance. Function **Colour** → TBHQ disappears, E171 is listed. Add the rosemary swap to the plan → 1 row whose declaration mentions rosemary extract (E392).

## Documentation

Complete user guide and technical documentation — the clean-label reformulation problem, how to use the finder, the database by function group, how to read a swap card, five worked examples in full (TBHQ; nitrite and the celery nuance; modified starch → pulse flours; aspartame → stevia/monk fruit; MSG → yeast extract), when NOT to swap (the three keep verdicts), label-declaration principles, honest scope, the testing summary, and the tested core verbatim: `docs/clean-label-replacement-finder-docs.pdf`.

Created by Dr. Asif Ahmad · Asif SaaS Studio · v1.0
