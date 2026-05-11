# Proposal: 1000 ICP-Qualified Companies in 30 Days
### DeepThought Business Analytics Internship — Part B, Question 2

---

## The Core Problem

Building a list of 1000 companies sounds like a volume problem. It isn't. It's a yield problem.

If you scrape 10,000 Indian manufacturers from MCA or an industrial directory, you'll get 10,000 names. But DeepThought's ICP is a narrow intersection — specialty product, promoter-driven, Rs.50–500Cr, technical decision-maker, growth mode. From empirical testing in Part A, roughly 3 in 10 companies investigated will pass. That means to find 1000 genuine passes, you need to investigate ~3,500 companies. And to have 3,500 worth investigating, your raw universe needs to be ~5,000–6,000.

The constraint isn't finding names. It's making sure every hour of investigation time is spent on companies that have at least a reasonable prior probability of being Federer profile — so your ~30% yield rate applies to a pre-filtered pool, not a bulk dump.

This proposal is built around that logic.

---

## The Funnel

```
Raw universe: ~5,000–6,000 company records
  ↓ Hard pre-filters (auto-disqualify: MNC subsidiaries, PE-owned, revenue >500Cr, CROs/services)
Screened pool: ~3,000–3,500
  ↓ Website scraping + AI-assisted 6-criterion scoring
First-pass qualifies: ~1,200–1,400
  ↓ Human QA on borderline and low-confidence scores
Final verified list: 1,000 ICP-qualified companies
```

Each stage is described in detail below.

---

## Week 1: Build the Universe (Days 1–7)

The first week has one goal: collect 5,000–6,000 company records (name, city, segment, website URL) that have a non-trivial prior probability of being Federer profile companies. No scoring yet.

### Source 1: DSIR Recognized In-House R&D Units (Expected: 800–1,000 records)

**What:** The Department of Scientific & Industrial Research publishes a list of companies with recognized in-house R&D units. This list has ~3,500 entries nationally. Filtered to manufacturing companies in target cities and segments, it produces ~800–1,000 relevant records.

**Why it works:** DSIR recognition directly signals C3 (differentiation — they've invested in formal R&D) and C4 (technical decision-maker — someone had to set up and maintain a recognized R&D unit). It pre-qualifies two of the six criteria before you even open the company's website.

**How to extract:** DSIR list is downloadable from dsir.gov.in as a PDF/Excel. Parse it, filter by state (Karnataka, Maharashtra, Gujarat, Telangana, Tamil Nadu) and industry category (pharmaceuticals, chemicals, biotechnology, electronics, engineering).

**Limitation:** Skews toward established companies that knew about DSIR and applied. Misses newer startups and bootstrapped manufacturers who haven't engaged with the DSIR application process.

---

### Source 2: USFDA / EU-GMP / WHO-GMP Facility Databases (Expected: 400–600 records)

**What:** USFDA publishes a searchable database of approved drug manufacturing facilities globally (accessible at fda.gov/drugs). EU-GMP database is maintained by EMA. WHO-GMP prequalification list covers facilities for global health procurement.

**Why it works:** International regulatory approval simultaneously proves C1 (you can't get USFDA approval without a manufacturing facility), C3 (only differentiated specialty manufacturers pursue international regulatory compliance), and C5 (export market access). Three criteria proven in one data source.

**How to extract:** USFDA facility list can be scraped with a Python script (requests + BeautifulSoup) filtering to India. EU-GMP list is downloadable from the EMA website. Filter results to remove Tier-1 large pharma companies (Sun, Cipla, Dr. Reddy's — these will exceed Rs.500Cr). Focus on the mid-tier.

**Limitation:** Heavy pharma/biotech bias. Doesn't cover defence, agri-inputs, diagnostics, or specialty engineering well. Good for chemicals and pharma verticals.

---

### Source 3: BSE SME / NSE Emerge Listed Companies (Expected: 500–700 records)

**What:** BSE SME platform and NSE Emerge list small-cap manufacturing companies. These companies are typically Rs.10Cr–Rs.300Cr revenue — directly in the ICP revenue band.

**Why it works:** Listed companies have public annual reports (revenue verified, ownership structure clear, director bios available). This makes the scoring process dramatically faster — revenue band, promoter control, and DM credentials can be checked in 3 minutes instead of 15.

**How to extract:** BSE provides sector-wise company lists downloadable from bseindia.com. Filter to: Pharmaceuticals, Chemicals, Biotechnology, Medical Devices, Defence, Agri-Inputs. Download company master with CIN, website, sector.

**Limitation:** Only captures listed companies. The majority of genuine Federer MSMEs are unlisted private limited companies. This source covers the listed minority — important for verification quality but not for volume.

---

### Source 4: Industry Expo Exhibitor Lists (Expected: 700–900 records)

**What:** Major industry-specific trade expos publish exhibitor directories. Target expos:
- **BioAsia** (Hyderabad) — biotech, pharma, diagnostics
- **CPHI India** — pharma ingredients, APIs, CDMOs
- **Chem Expo India** / **India Chem** — specialty chemicals
- **ACREX / IMTEX** — engineering, precision manufacturing
- **Agri Intex** (Coimbatore) — agri-inputs, seeds, crop protection
- **MedIndia / Medtronics India** — medical devices, diagnostics
- **India Lab Expo** — lab instruments, diagnostics, life science tools

**Why it works:** Expo participation signals growth intent (spending Rs.2–10L on a booth). Exhibitor directories are already segmented by industry and include company names, websites, and sometimes contact information. Self-selection means companies that exhibit are typically active, growth-mode operators.

**How to extract:** Most expo websites publish PDF exhibitor directories. Recent expos (2023–2025) are most valuable. Use Python (PyMuPDF for PDF parsing) or manual extraction.

**Limitation:** Biased toward companies with marketing budgets. Misses bootstrapped manufacturers who grow through word-of-mouth and don't exhibit.

---

### Source 5: State Industrial Development Corporation Directories (Expected: 600–800 records)

**What:** TSIIC (Telangana), MIDC (Maharashtra), GIDC (Gujarat), KIADB (Karnataka), and SIDCO (Tamil Nadu) maintain lists of companies in their industrial estates. These are physical manufacturing locations — real plants, not virtual offices.

**Why it works:** Industrial estate membership directly proves C1 (manufacturer with a physical plant) and C2 (India-based). These directories are less well-known than national databases, so competitors researching the same ICP are less likely to have mined them.

**How to extract:** Some directories are publicly available on state government websites. Others require a request or a nominal fee. GIDC and MIDC directories are relatively accessible. Filter by industrial area type (pharmaceutical belt, chemical zone, biotech park).

**Limitation:** Data may be stale. Companies in industrial estates may have closed or changed segments. Requires manual verification of active status.

---

### Source 6: LinkedIn Sales Navigator — Inverted Search (Expected: 400–600 records)

**What:** Instead of finding companies and checking if the founder is technical, find technical founders first and check if their company is a manufacturer.

Search parameters: Industry (pharmaceutical manufacturing, chemical manufacturing, biotechnology, medical devices), Company headcount (50–500 people, proxy for Rs.30–500Cr revenue), Geography (Bengaluru, Pune, Hyderabad, Ahmedabad, Chennai, Coimbatore, Vadodara, Indore), Seniority (Owner, CXO, Founder), Keywords in title or bio (PhD, IIT, BITS, IISc, NIT, "R&D Head" turned founder).

**Why it works:** This approach is C4-first. Every company found this way has already passed the technical DM criterion — you're just verifying manufacturing and differentiation. It also surfaces unlisted private companies that don't appear in financial databases.

**Limitation:** LinkedIn data is self-reported and often incorrect for Indian MSMEs. Company headcount is particularly unreliable. Needs verification. Also misses founders who don't maintain LinkedIn profiles (surprisingly common in the 50+ age bracket in tier-2 cities).

---

### Source 7: MCA Database via Antigravity/Tofler (Expected: 800–1,000 records, after filtering)

**What:** Ministry of Corporate Affairs has data on all 2M+ registered Indian companies. Filter by: NIC code (target manufacturing sub-sectors), state (target states), paid-up capital (Rs.1Cr–Rs.50Cr proxy for MSME size), active company status.

Target NIC codes:
- 21001–21009: Pharmaceutical manufacturing
- 20119–20291: Specialty chemical manufacturing
- 26601–26609: Medical devices and instruments
- 27201–27209: Electronics and communication equipment
- 01111–01129: Agri seed and crop input manufacturing

**Why it works:** Comprehensive coverage of private companies invisible to other sources. Includes company name, directors, CIN, and registered address.

**Limitation:** Very noisy. NIC codes are self-reported and frequently incorrect. Many "manufacturing" companies by NIC code are actually traders or service providers. Requires aggressive post-filtering. No website data — website discovery adds significant time.

---

### Week 1 Output Target

After deduplication across all 7 sources: **~5,000–6,000 company records** with at minimum name, city, and rough segment tag. Approximately 55% will have a website URL. Remaining 45% need website discovery.

**Deduplication approach:** Fuzzy string matching on company names (Levenshtein distance) combined with CIN matching for listed companies. Manual review of top 50 suspected duplicates.

**Website discovery for companies without URLs:**
- Google search automation: `"{company name}" {city} site:.com OR site:.in`
- If no website found after 3 search attempts: flag as "no website" — these companies are deprioritized (impossible to score without a website unless we have alternative sources)

**Week 1 Daily Schedule:**

| Day | Task |
|-----|------|
| 1–2 | Download and parse DSIR list, BSE/NSE SME lists, USFDA facility list — structured data, fastest to process |
| 3–4 | Scrape expo exhibitor directories from 6–8 target expos. Build scraper with Python + Playwright or BeautifulSoup |
| 4–5 | Extract MIDC, GIDC, TSIIC, KIADB directories. Query MCA via Antigravity for target NIC codes |
| 5–6 | LinkedIn Sales Navigator extraction for technical founders in target cities and segments |
| 6–7 | Deduplicate master list. Website discovery for companies without URLs. Build final universe CSV |

---

## Weeks 2–3: Automated ICP Scoring (Days 8–19)

### The Scraper

For each company with a website, scrape these pages and concatenate to a single text blob (~8K tokens max):
- Homepage
- /about, /about-us, /company
- /leadership, /team, /management
- /products, /services (to distinguish manufacturer from services company)
- /news, /media, /press, /blog
- /careers, /jobs (hiring signals → C6)
- /certifications, /quality, /compliance

**Technical stack:** Python + Playwright (handles JavaScript-rendered sites) with 15-second timeout per page. Respect `robots.txt`. Random delay between requests (3–8 seconds) to avoid being blocked.

**Pre-filter before scraping:**
Before running the LLM scoring pipeline, auto-reject any company where:
- No website found (after Google search attempt)
- Website is a parked page (total page text < 300 characters)
- Company name contains "Trading", "Distributors", "Imports", "Exports" (word-level match, not substring)
- Revenue is known and >Rs.500Cr (from BSE data)
- Company name contains known MNC parent names (Bayer, BASF, Syngenta, Cipla, Sun Pharma, Dr. Reddy's)

This pre-filter should eliminate ~500–800 records before AI scoring, saving cost and time.

---

### The AI Scoring Pipeline

**Prompt architecture:**
The scoring prompt is sent to Claude (Haiku for first pass, Sonnet for borderline review) with:
1. The concatenated scraped website text
2. DeepThought's 6-criterion ICP definition (verbatim from the assignment brief)
3. Explicit instructions to score each criterion as Weak / Moderate / Strong with a one-line evidence quote from the scraped text
4. An instruction to flag any criterion where it "cannot find evidence" as "Unknown" rather than defaulting to a score
5. An instruction to identify if the company appears to be a CRO/services company and disqualify at C1
6. A request for a JSON response with a structured schema

**Expected response schema:**
```json
{
  "c1_manufacturer": {"score": "Strong", "evidence": "...", "confidence": "high"},
  "c2_india": {"score": "Strong", "evidence": "...", "confidence": "high"},
  "c3_differentiation": {"score": "Moderate", "evidence": "...", "confidence": "medium"},
  "c4_tech_dm": {"score": "Unknown", "evidence": null, "confidence": "low"},
  "c5_tailwind": {"score": "Strong", "evidence": "...", "confidence": "high"},
  "c6_growth": {"score": "Weak", "evidence": "...", "confidence": "low"},
  "overall_verdict": "borderline",
  "disqualify_flag": null,
  "notes": "..."
}
```

**Cost estimate:**
- Haiku first pass: ~$0.005/company × 3,500 = ~$17.50 (~Rs.1,500)
- Sonnet re-score on ~20% borderline: ~$0.04/company × 700 = ~$28 (~Rs.2,400)
- Scraping compute: negligible
- **Total AI cost: under Rs.4,000 for the full pipeline**

**Speed estimate:**
- Scraping: ~45 seconds/company (with delays) = ~43 hours for 3,500. Run 5 parallel scrapers = ~9 hours total
- Haiku scoring: ~3 seconds/company API latency = ~3 hours for 3,500 (with batching)
- Sonnet re-scoring: ~5 seconds/company = ~1 hour for 700
- **Total compute: ~13 hours spread over 2–3 days**

**Weeks 2–3 Daily Schedule:**

| Day | Task |
|-----|------|
| 8–9 | Build and test scraper on 50 companies. Debug edge cases (JS-heavy sites, rate limiting, redirect chains) |
| 10 | Build scoring pipeline: prompt design, JSON parser, result storage. Test on 15 calibration companies (use Part A companies as ground truth). Tune prompt until ≥12/15 match expected scores |
| 11–14 | Run scraper on full universe (3,500 companies, 5 parallel workers) |
| 14–17 | Run Haiku scoring on all scraped companies |
| 17–18 | Run Sonnet re-scoring on borderline cases (total score 40–50, or any criterion flagged "low confidence") |
| 19 | Compile first-pass results. Expected output: ~1,200–1,400 passes, ~300–400 borderline/low-confidence flagged for human QA |

---

## Weeks 3–4: Human QA (Days 19–30)

### Why Human QA Is Non-Negotiable

AI scoring has predictable failure modes that cannot be fixed with better prompts alone:

1. **C3 inflation:** LLM reads "ISO 9001 certified" and scores differentiation as Moderate. But ISO 9001 is a baseline quality management standard — almost every manufacturer has it. It is not a differentiator. A human reviewer recognizes this immediately; an LLM needs explicit instruction for every certification type.

2. **C4 false positives:** LLM infers "technical founder" from any engineering degree mention on the website. But a B.Tech from a tier-3 college running a commodity chemicals trading company is not the same as a PhD from IISc running a specialty biotech. The LLM sees "engineering background" and scores Moderate; a human reviewer would score Weak.

3. **C6 false positives:** LLM reads press coverage from 2019 and scores growth as Moderate. But no visible activity in 5 years is a red flag for C6, not a neutral signal.

4. **C1 false negatives:** Some genuine manufacturers use "solutions provider" or "services" language on their website (especially when trying to position for B2B consulting relationships) but actually produce physical products. LLM takes the website language too literally and disqualifies good companies.

### QA Process

**Step 1 — Auto-QA flags (programmatic, before human review):**
Flag for human review if any of these conditions are met:
- All 6 criteria are scored "high confidence" but total is exactly 40–42 (likely inflated borderline)
- C3 evidence mentions ONLY "ISO 9001" or "ISO 14001" with no other differentiation signals
- C6 evidence references news articles or press releases older than January 2023
- C4 evidence mentions educational credential but no named person (LLM may have hallucinated a credential)
- Any criterion has confidence = "low" or "unknown"

Expected flagged count: ~300–400 companies

**Step 2 — Human review of flagged companies:**
For each flagged company: open website, verify 2–3 key claims, adjust scores if needed. Decision: Accept / Reject / Keep as borderline.

Estimated time: 4–5 minutes per company × 350 companies = ~25 hours. Spread across 5 working days = 5 hours/day.

**Step 3 — Spot check strong passes:**
Randomly sample 50 companies from the "strong pass" (70+ score) group. Verify core claims. This tests whether the pipeline is systematically inflating scores for a category we haven't anticipated.

**Step 4 — Final list assembly:**
- Take all strong_pass companies (expected ~600–700)
- Take human QA-verified pass companies (expected ~400–500)
- Drop remaining borderline/unverified
- Target: **1,000 verified companies**

**Weeks 3–4 Daily Schedule:**

| Day | Task |
|-----|------|
| 19–20 | Run auto-QA flags. Separate flagged vs. clean. |
| 20–24 | Human QA on ~350 flagged companies (5 hours/day × 4 days) |
| 24–25 | Spot-check 50 strong_pass companies |
| 25–27 | Final assembly: merge clean strong_pass + QA-verified pass. Deduplicate. Verify count ≥ 1,000 |
| 27–29 | Add personalization hooks for top 200 (priority outreach tier) |
| 29–30 | Format final deliverable. Write source breakdown. Buffer for overruns |

---

## Weekly Summary

| Week | Focus | Daily Output |
|------|-------|-------------|
| 1 | Sourcing | Build 5,000–6,000 company universe with names, cities, segment tags, websites |
| 2 | Scraping + first-pass scoring | All companies scraped and scored by AI. ~1,200–1,400 first-pass qualifications |
| 3 | Re-scoring + QA start | Borderline re-scored. Human QA begins on 300–400 flagged companies |
| 4 | QA completion + assembly | 1,000 verified companies in final CSV. Top 200 with personalization hooks |

---

## Yield Expectations at Each Stage

| Stage | Count | Notes |
|-------|-------|-------|
| Raw universe | 5,000–6,000 | Before deduplication |
| After deduplication | 4,500–5,200 | ~10–15% overlap across sources |
| After hard pre-filter | 3,000–3,500 | Remove MNC/PE/CRO/no-website |
| After AI first-pass scoring | 1,200–1,400 pass | ~35–40% pass rate after pre-filtering |
| After human QA | 1,000 verified | Drop inflated borderlines and false positives |
| **Net yield from raw universe** | **~20–22%** | Conservative; may improve with prompt refinement |

---

## Risk Mitigation

| Risk | Probability | Mitigation |
|------|-------------|-----------|
| Yield lower than 30% | Medium | Expand universe with 2–3 additional expo lists. Add state industrial estates (SIDCO Tamil Nadu, RIICO Rajasthan). Run a second LinkedIn search pass targeting different company sizes |
| Scraper blocked by websites | Medium | Rotate user agents. Add variable delays (5–12 sec). Use residential proxy for high-priority sectors. Fall back to manual for important companies that block scraping |
| AI scoring accuracy <80% on calibration set | Low-Medium | Retune prompt on calibration set. Split into two-step scoring: Haiku for C1/C2/C5 (factual signals), Sonnet for C3/C4/C6 (judgment calls). Add more negative examples in the prompt |
| QA bottleneck >25 hours | Medium | Tighten auto-QA rules to reduce flag volume. Focus QA on C3 and C4 (highest false positive rate). Accept moderate-confidence scores for C1/C2/C5 without human review |
| Deduplication errors (same company listed under multiple names) | Low | Fuzzy name matching + CIN number matching for listed companies. Manual review of top 30 suspected duplicates |
| Week 1 data sources slower than expected | Low-Medium | DSIR and BSE sources process in Day 1–2. Expo scraping is the variable — start it in parallel with other sources, not sequentially |

---

## Budget

| Tool | Purpose | Estimated Cost |
|------|---------|---------------|
| Claude Haiku API | First-pass ICP scoring (3,500 companies) | ~Rs.1,500 |
| Claude Sonnet API | Borderline re-scoring (700 companies) | ~Rs.2,400 |
| Antigravity | MCA data extraction | License provided |
| LinkedIn Sales Navigator | Technical DM discovery | License provided |
| Playwright + Python | Website scraping (open source) | Free |
| Residential proxy service | Anti-blocking for scraping | ~Rs.2,000/month |
| Tofler / Zauba Corp | MCA lookups, export verification | ~Rs.3,000 one-time |
| **Total** | | **~Rs.9,000** |

---

## Final Deliverable Structure

1. **Master CSV** — 1,000 companies, each with: name, website, city, segment, products, revenue band, decision-maker name + credentials, C1–C6 scores with evidence quotes, overall verdict, confidence flags, source
2. **Priority-200 list** — Top 200 companies scored ≥80 with personalization hooks ready for outbound
3. **Source breakdown** — Which sources contributed how many final companies (to inform future sourcing investment decisions)
4. **Methodology document** — Scraper architecture, scoring prompt text, QA process, yield rates at each stage
5. **Code repository** — All scraping scripts, scoring pipeline, QA automation, data processing notebooks — reproducible end-to-end

---

## A Note on Quality vs. Speed

The 30-day timeline is tight but achievable. The risk is cutting QA to hit the count target. I would rather deliver 950 verified companies on Day 30 than deliver 1,050 companies with 150 inflated borderlines included to hit a round number.

DeepThought's sales team will use this list to write personalized outreach. A false positive — where someone sends a well-crafted email to a CRO that was misclassified as a manufacturer — damages credibility more than a slightly shorter list. Quality control is the constraint that cannot be sacrificed.

---

*Proposal for DeepThought Business Analytics Internship | May 2026*
