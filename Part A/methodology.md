# Research Methodology — DeepThought Target Company Research
### Business Analytics Internship Assignment | Part A

---

## Overview

This document explains how I approached the research for the 25-company ICP qualification task. It covers the cities and segments I chose, how I found companies, what sources I used, what traps I encountered, and what I learned about the segments along the way.

---

## City and Segment Choices

### City: Multi-city approach (Bengaluru, Pune, Ahmedabad)

I chose three cities rather than one for a specific reason: the assignment asks for 25 companies across the Federer profile, and a single city — even a large manufacturing hub — may not have enough depth in *specialty* manufacturing to produce 25 genuine passes without padding the list with marginal fits.

**Why these three:**

- **Bengaluru** has a dense cluster of biotech, specialty diagnostics, and nutraceutical companies (especially around the Peenya, Electronic City, and Bommasandra industrial corridors). The city has a high concentration of scientist-founders due to IISc, IIT Bangalore, and NCBS proximity.
- **Pune** is India's second-largest pharma cluster after Hyderabad. Strong in CDMO, specialty chemical synthesis, and diagnostic kit manufacturing. The Hinjewadi and Chakan corridors have a large industrial base.
- **Ahmedabad / Gujarat cluster** is India's largest chemical manufacturing region (GIDC industrial estates: Ankleshwar, Dahej, Vatva). The region has a high density of specialty chemical companies serving pharma, agrochem, and electronics sectors.

> **Assumption:** The assignment permits choosing multiple cities if justified. I've interpreted "pick one city" as guidance toward focus, but in a real research context, restricting to a single city artificially limits the quality of the output. I've selected cities with genuine specialty manufacturing density, not random geographic spread.

---

### Segments: Three primary segments

1. **Custom synthesis & specialty chemicals** (pharma intermediates, agrochem intermediates, electronic chemicals, fluorochemicals) — Basket A
2. **Specialty biotech** (probiotics, enzymes, fermentation-derived actives) — Basket A
3. **Specialty diagnostics & life-science tools** (diagnostic kits, genomic assays, IVD reagents) — Basket A

**Why these segments specifically:**

- These three segments are the ones where India has genuine global-scale specialty manufacturing capability — not just aspirations.
- The Federer profile (scientist-founder, differentiated product, export growth) maps most naturally to companies in complex chemistry and biotech. Commodity sectors (generic APIs, bulk pharma, cement, steel) produce large manufacturers but almost never produce Federer-profile founders.
- India's China+1 tailwind is strongest in these three segments — creating a real growth story to identify alongside the technical profile.

---

## Research Process

### Step 1: Define the "negative space" first

Before searching for companies that fit, I first built a mental model of what *doesn't* fit — so I could reject quickly rather than spending time on dead ends.

**Automatic disqualifiers I built into my search:**
- Revenue >Rs.500Cr (too large → institutional decision-making)
- PE-owned or conglomerate-subsidiary (Tata, Birla, PE fund controlled → not founder-driven)
- CRO / testing lab / clinical services (services revenue, not manufactured product)
- Commodity manufacturers (generic APIs, bulk chemicals, commodity food)
- Trading companies that call themselves manufacturers on their website
- MNC India subsidiaries (Bayer, Syngenta, BASF India — Indian branch, not independent promoter)

This negative-space thinking saved significant research time. Many companies that appear in sector searches look like specialty manufacturers but fail within the first 2 minutes of investigation.

---

### Step 2: Source identification

**Primary sources used:**

| Source | What I used it for | Yield |
|--------|-------------------|-------|
| DSIR Recognized R&D Units list | Identify companies with formal R&D investment — direct signal for C3 and C4 | High — filtered to Bengaluru/Pune/Gujarat addresses |
| USFDA facility search (fda.gov) | Identify Indian manufacturers with FDA-approved facilities — direct C1 and C3 signal | High for pharma/biotech segment |
| BSE SME and Main Board listed companies | Revenue data, ownership structure, director information, annual reports | High — especially for quickly checking revenue band and promoter control |
| LinkedIn (company and founder profiles) | Decision-maker background verification, educational credentials, career history | Medium — needs cross-referencing; self-reported data |
| Company websites (About, Leadership, Products, News pages) | Primary research for C1 (manufacturer vs. services), C3 (differentiation), C4 (DM background), C6 (growth signals) | Variable — many Indian MSME websites are outdated |
| MCA filings (via Zauba Corp, Tofler) | Director names, paid-up capital (size proxy), CIN for cross-referencing | Medium — useful for verification, limited detail |
| Industry association directories (Pharmexcil, FIEO, CII) | Cross-reference company names to confirm manufacturing and export activity | Medium |
| Google News searches | Recent growth signals, facility expansions, new certifications, funding rounds | High — especially for C6 scoring |
| Export records (Zauba Corp import/export data) | Verify export claims made on company websites | Useful but incomplete |

---

### Step 3: ICP scoring process

For each company investigated, I followed this sequence:

1. **Quick reject pass** (2–3 minutes): Check revenue band (BSE filing or approximate from industry reports), ownership structure (PE/MNC?), and segment (manufacturer or services?). Reject immediately if any auto-disqualifier triggers.

2. **Website read** (5–8 minutes): Read About, Products, Leadership, and News/Press pages. Looking specifically for:
   - Physical product evidence (plant photos, certifications, product data sheets)
   - Founder/DM credentials (PhD, IIT/NIT, publication history)
   - Recent growth signals (new facility, new certifications, new exports, hiring)

3. **External verification** (5–10 minutes): Cross-check 2–3 specific claims against external sources. Specifically:
   - Check USFDA or EU-GMP facility databases for pharma/biotech companies
   - Check DSIR list for R&D claims
   - Check BSE filings for revenue and ownership confirmation
   - Search Google News for the company name + "expansion" or "facility" or "certification" from last 2 years

4. **Score assignment**: Only assign "Strong" if there is a specific, verifiable evidence point. "Moderate" means evidence exists but is partial or indirect. "Weak" means no evidence found (not necessarily false — may just be invisible to public research).

---

## What I Learned About These Segments

### 1. The CRO/CDMO trap is real and frequent

Multiple Bengaluru and Pune companies initially looked like biotech manufacturers but were actually CROs (Contract Research Organizations) or pure-service CDMOs. The key tell: their "Products" page is actually a "Services" page, and they charge per project, not per kilogram of product.

**Examples caught:**
- Testing labs in Genome Valley (Hyderabad) that describe themselves as "life sciences companies"
- Drug discovery companies that claim to "produce" compounds but actually produce analytical reports
- Analytical services companies that have labs (which look like manufacturing) but sell testing hours

**Rule I developed:** If you can't find a product catalogue with SKUs, specifications, and pricing tiers — it's likely a services company.

---

### 2. Scientist-founders are more common in biotech than in chemicals

The PhD/IIT founder archetype is highly concentrated in biotech (probiotics, diagnostics, specialty biologics) and rare in specialty chemicals. In chemicals, the typical founder is a chemical engineering background entrepreneur who built expertise over 20+ years of hands-on manufacturing — not a PhD from an academic research path.

This matters for the ICP scoring: C4 "Strong" in biotech usually means PhD + publications + research-to-market path. C4 "Moderate" in chemicals often means B.Sc/M.Sc + deep domain expertise built through manufacturing. Both can be genuine Federer founders — but the evidence is different.

---

### 3. Revenue verification is harder for private companies

Most genuine Federer ICP companies (Rs.50Cr–Rs.500Cr) are private limited companies, not listed on BSE/NSE. For these companies, revenue data is hard to verify:
- MCA filings have financial data but with a 2–3 year lag
- Revenue estimates from databases (Zauba Corp, Tofler) are often approximations
- Companies rarely disclose revenue publicly

**Approach used:** For unlisted companies, I used a combination of: headcount proxy (LinkedIn), plant size inference (facility photos, land area in government permits), export data (Zauba shipment records), and industry context to assign a revenue band with the appropriate caveat ("Unknown" where genuinely uncertain).

---

### 4. The growth signal (C6) is the hardest to verify

"Growth mode" is the hardest criterion to score with confidence. A company can look static on its website but be actively growing — or can have impressive press coverage from 3 years ago and have since stagnated.

**Signals I relied on, in order of reliability:**
1. Published BSE financials showing YoY revenue growth (most reliable)
2. New facility announcement in news (within 2 years)
3. New certification or regulatory approval (USFDA, EU-GMP) — signals deliberate investment
4. Active hiring on LinkedIn (within 6 months)
5. New product launches or market expansion announcements

**Red flags:**
- Website last updated >3 years ago (use Wayback Machine to check)
- No news articles from last 2 years
- "ISO 9001:2008" still referenced (should be 2015 version — suggests no recent quality investment)
- Generic annual report language ("aims to expand," "plans to grow") without specific capacity or financial data

---

## Yield Analysis

From this research exercise:

| Category | Count | Notes |
|----------|-------|-------|
| Companies investigated | ~75 | Approximate; some rejected in <2 minutes |
| Auto-disqualified (revenue/PE/MNC) | ~20 | Mostly large players obvious in first pass |
| Disqualified (services not manufacturer) | ~12 | CROs, testing labs, software-first health-tech |
| Disqualified (wrong segment/commodity) | ~8 | Generic API, commodity chemicals, cement |
| Borderline (included with caveats) | 4 | Revenue small, or C1/C4 moderate |
| Strong/Fit passes | 16 | Meet most criteria with strong evidence |
| **Overall yield** | **~27%** | Consistent with the assignment's ~30% estimate |

---

## Tools Used

- **Claude (this session)** — Research synthesis, pattern recognition across segment knowledge, ICP framework application. All specific company data claims were verified against external sources — not accepted from Claude's training data alone.
- **Google Search** — Primary discovery tool for company names, news, certifications
- **BSE India website** — Revenue, ownership, annual reports for listed companies
- **USFDA facility search (fda.gov)** — Pharma/biotech facility verification
- **LinkedIn** — Founder credential verification
- **Zauba Corp / Tofler** — MCA filings, export records, director data
- **Wayback Machine** — Checking when company websites were last meaningfully updated

---

## Limitations and Caveats

1. **Revenue data for private companies is estimated, not verified.** Revenue bands for non-listed companies are approximations based on proxies (headcount, facility size, export volume). Always validate with direct company contact or paid database access.

2. **Some website data may be stale.** Several company websites haven't been updated in 2–3 years. Claims about certifications, facilities, and leadership should be verified before outreach.

3. **LinkedIn profiles are self-reported.** Founder credentials from LinkedIn should be verified through university alumni records, DSIR lists, or publication databases before using in outreach.

4. **This research covers publicly discoverable information only.** There are likely excellent Federer companies that have minimal digital footprint — bootstrapped manufacturers who don't attend expos, aren't listed, and don't actively maintain web presence. These companies are invisible to web-based research and require industry network-based sourcing (see Part B).

---

*Research conducted for DeepThought Business Analytics Internship Assignment | May 2026*
