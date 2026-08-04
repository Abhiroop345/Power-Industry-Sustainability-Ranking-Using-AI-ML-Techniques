# Power Industry Sustainability Ranking Using AI/ML Techniques

A transparent, reproducible AI/ML framework for ranking Indian power sector companies on
Environmental, Social, and Governance (ESG) performance — built as part of the IDEAS–TIH
Summer Internship Programme (IDEAS – Institute of Data Engineering, Analytics and Science
Foundation, ISI Kolkata).

## Overview

Commercial ESG ratings (CRISIL, MSCI, etc.) are widely used but proprietary, costly to access,
and opaque in their exact methodology. This project builds an open, auditable alternative:
a full pipeline that cleans public ESG disclosures, engineers features, applies unsupervised and
supervised machine learning, and produces a ranked Sustainability Index — with every
methodological choice, correction, and limitation documented rather than hidden.

**Companies covered:** Adani Power · Tata Power · Power Grid Corporation of India · JSW Energy ·
NTPC Limited · NHPC Limited
**Period:** FY 2022-23 to FY 2024-25 (18 company-year observations)

## Objectives

1. Identify sustainability indicators relevant to the power industry (13 indicators across E/S/G).
2. Collect and structure ESG data for six major Indian power companies over three years.
3. Apply AI/ML techniques — K-Means clustering and Random Forest regression — to evaluate and
   rank companies on sustainability performance.
4. Compare the AI-generated ranking against conventional weighting methods and an external ESG
   benchmark.
5. Identify sustainability leaders and laggards and provide actionable recommendations.

## Methodology

The pipeline follows four phases, fully implemented in the Colab notebook:

1. **Data Preparation** — cleaning, missing-value imputation, feature engineering (derived Waste
   Intensity, governance-text scoring), and segment-aware Min-Max normalization.
2. **Feature Selection** — Pearson correlation analysis and PCA to check indicator redundancy and
   validate the E/S/G groupings.
3. **AI/ML Model Development** — K-Means clustering (sustainability tiers) and Random Forest
   regression (data-driven pillar weights via feature importance), both validated appropriately
   for a small-sample dataset (silhouette score / 5-fold cross-validation).
4. **Sustainability Ranking Framework** — a composite Sustainability Index
   `SI = wE·E + wS·S + wG·G` under equal, expert, and AI-derived weighting schemes, benchmarked
   against an external ESG reference score via Spearman rank correlation.

Two methodological corrections are documented explicitly in the notebook and report:
undisclosed governance text was initially (incorrectly) scored as zero rather than treated as
missing data, and combustion-driven environmental indicators are normalized within business-model
peer segments (Thermal/Mixed Generation vs. Transmission/Hydro) rather than pooled across all six
companies, to avoid mechanically favoring non-combustion business models.

## Key Results

| Rank | Company | Sustainability Index (AI-derived weights) | Category |
|------|---------|---------------------------------------------|----------|
| 1 | JSW Energy | 0.846 | Leader |
| 2 | Power Grid Corporation of India | 0.716 | Leader |
| 3 | NHPC Limited | 0.699 | Leader |
| 4 | Adani Power | 0.539 | Average |
| 5 | Tata Power | 0.496 | Laggard |
| 6 | NTPC Limited | 0.375 | Needs Improvement |

External validation against an illustrative ESG benchmark score found a weak, statistically
non-significant Spearman correlation (ρ = 0.319, p = 0.538) across all three internal weighting
schemes — an honest finding discussed in detail in the report, not glossed over. A weight-
calibration procedure (grid search) improves this fit (ρ = 0.754) by shifting weight toward
Governance, though this is flagged as a small-sample result requiring further validation.

## How to Run

**Option A — Google Colab (recommended, no setup required)**
1. Open [Google Colab](https://colab.research.google.com).
2. `File → Upload notebook` and select `notebooks/Power_Sector_Sustainability_Ranking_AI_ML.ipynb`.
3. Run all cells (`Runtime → Run all`). When prompted, upload `data/ESG_Dataset.xlsx`.

**Option B — Local Jupyter**
```bash
git clone https://github.com/<your-username>/power-sector-esg-ranking.git
cd power-sector-esg-ranking
pip install -r requirements.txt
jupyter notebook notebooks/Power_Sector_Sustainability_Ranking_AI_ML.ipynb
```

## Requirements

See [`requirements.txt`](requirements.txt). Core dependencies: `pandas`, `numpy`, `scikit-learn`,
`scipy`, `matplotlib`, `openpyxl`.

## Limitations

- Small sample size (6 companies, 18 observations) limits the statistical robustness of
  correlation, feature-importance, and cross-validation estimates.
- External validation uses an illustrative benchmark score; verified CRISIL/MSCI ESG ratings
  would strengthen Section 5 of the report considerably.
- Findings are specific to the Indian power sector and may not generalize elsewhere.

Full discussion in `docs/IDEAS_ISI_Summer_Internship_Report.docx`, Section 6 (Conclusion) and
Section 11 equivalent (Limitations).

## Deliverables

- **Notebook:** end-to-end, reproducible analysis pipeline (`notebooks/`)
- **Report:** full project report in IDEAS–ISI submission format (`docs/`)
- **Presentation:** 12-slide project summary deck (`docs/`)

## License

Code in this repository is released under the [MIT License](LICENSE). The underlying ESG data is
compiled from public company disclosures (annual reports, sustainability reports) and is provided
here for academic and educational purposes only; no ownership over the source companies' data is
claimed.

## Acknowledgments

Developed as part of the IDEAS–TIH Summer Internship Programme, under the guidance of
Dr. Piyali Sengupta, IDEAS – Institute of Data Engineering, Analytics and Science Foundation,
ISI Kolkata.
