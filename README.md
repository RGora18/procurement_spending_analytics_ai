# Government Procurement Spending Analytics with AI

**Program:** AICTE | IBM SkillsBuild Data Analytics with AI Academic Internship 2026 (BharatCares)
**Author:** Rutuja

## Project Description

This project analyzes **real government tender data** from Singapore's GeBIZ e-procurement portal
to uncover spending trends, category and agency-wise allocation, and vendor concentration, then
builds a machine learning model that predicts **tender failure risk** &mdash; the risk that a tender
receives zero supplier bids &mdash; using only information known before the tender is awarded.

The project follows the exact analyst workflow taught across the program's masterclasses:

**Raw Data &rarr; Clean Data &rarr; EDA &rarr; Insights &rarr; Prediction &rarr; Dashboard &rarr; Decision**

## Tools & Platforms Used (per Masterclass Requirements)

| Tool | Role in this project |
|---|---|
| **Google Colab** | The notebook environment this project is built for. Upload `procurement_data_raw.csv` via the Files panel, then Runtime → Run all. |
| **Google Gemini** | Used as the AI coding assistant during development, following the **Ask AI → Review → Verify → Apply** workflow from Masterclass 1 — specific, detailed prompts (documented inline in the notebook, e.g. Sections 1.5–1.6) rather than vague requests, with every AI-suggested change reviewed and verified against the actual data before being applied. |
| **IBM Bob** | IBM's AI-powered development partner (introduced in the program's IBM Bob onboarding session), used to assist with project structuring. |
| **pandas, numpy, matplotlib, seaborn, scikit-learn** | Core Python data analytics and machine learning stack. |

## Dataset

**Real dataset:** *Government Procurement via GeBIZ* — 32,756 actual tender award records from
Singapore's government e-procurement portal (2015–2021), across 122 agencies. Published on Kaggle.

**Raw columns:** `tender_no., tender_description, agency, award_date, tender_detail_status, supplier_name, awarded_amt`

The raw data had no missing values and no true duplicate rows, but did need real cleaning work:
- `award_date` was stored as DD/MM/YYYY text and was converted to a proper date type.
- No category column existed — one was engineered from `tender_description` using keyword rules (see notebook Section 1.6).
- Repeated `tender_no.` values were investigated and confirmed to be a legitimate one-tender-to-many-rows structure (multi-item/multi-supplier awards), not duplicate-record errors.

## Project Structure

```
├── Rutuja_ProcurementAnalytics.ipynb   # Main notebook — full 7-stage workflow on real data
├── procurement_data_raw.csv            # Real GeBIZ dataset (32,756 rows)
├── requirements.txt                    # Python dependencies
├── Rutuja_ProjectReport.docx           # Full project report/documentation
└── README.md                           # This file
```

## Setup & Run Instructions

### Option A — Google Colab (as taught in the masterclasses)
1. Go to [colab.research.google.com](https://colab.research.google.com/) and sign in.
2. Upload `Rutuja_ProcurementAnalytics.ipynb` (File → Upload notebook).
3. Click the Files icon on the left, click Upload, and add `procurement_data_raw.csv`.
4. Runtime → Run all.

### Option B — Local Jupyter
```bash
pip install -r requirements.txt
jupyter notebook Rutuja_ProcurementAnalytics.ipynb
```
Then Cell → Run All.

## The 7-Stage Workflow in This Notebook

1. **Raw Data → Clean Data** — verify data quality on real data (dates, duplicates, outliers); engineer a Category column; define 5 business questions.
2. **EDA** — trends, rankings, comparisons, vendor/agency segments, correlations — all computed on real numbers.
3. **Insights** — Observation → Insight → Hypothesis → Recommendation, printed directly from live computation, not assumed.
4. **Prediction** — leakage-safe Random Forest model predicting real tender-failure risk; confirmed and excluded a genuine leakage source (`awarded_amt` is always 0 for failed tenders); accuracy/precision/recall explained in plain business language; confusion matrix; risk table.
5. **Dashboard** — 4-panel summary view of the key metrics.
6. **Decision** — practical, non-causal business recommendations based only on model output.
7. **Wrap-up** — summary of what was built and next steps.

## Results Summary (Real Data)

- Total awarded value trended between roughly S$16–24 billion/year from 2015–2020 (2021 is a partial year in this dataset, through March).
- **Construction & Infrastructure** was the largest category by awarded value (~47% of category spending); **Land Transport Authority** was the top agency by awarded value.
- The top 10 identified suppliers held about 19% of total awarded value (excluding "Unknown"/no-award rows).
- 4.3% of tender records received zero supplier bids ("Awarded to No Suppliers").
- The tender-failure prediction model reached ~81% accuracy, but — as the notebook explicitly flags — accuracy is misleading on this imbalanced target (always predicting "will succeed" would already score ~96%). Precision and recall were low (~7% and ~26% respectively), showing that with only agency, category, and description-length as features, this real, rare event is genuinely hard to predict — an honest finding, not a failure to report.

## License / Use

Created for academic submission as part of the IBM SkillsBuild Data Analytics with AI Internship
(AICTE, in association with BharatCares). Not intended for commercial use. Underlying data sourced
from Singapore's public GeBIZ tender records via Kaggle.
