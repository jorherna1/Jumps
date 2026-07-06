# A Jump-Diffusion Framework to Construct an Unbiased Environmental Index

**Jorge Nestor Hernandez and Enrique Villamor**
Florida International University

---

## Overview

This paper proposes a market-based environmental index that avoids the self-reporting bias of corporate ESG disclosures and the subjectivity of third-party ratings. The approach identifies abnormal stock-price movements (jumps) triggered by climate-related news events: each trading day is classified as a jump day when the standardized return satisfies |Z| > 1, where Z is computed relative to a rolling 64-day baseline. Jump arrivals for each firm are modeled as a Poisson process with intensity lambda (average jumps per day) and average jump size k (mean signed return on jump days). A firm-level indicator theta = lambda * k summarizes the direction and magnitude of climate-news-driven price dislocations. Scores are min-max normalized to a 0-100 index, where higher values indicate more positive market responses to climate news. Because the index is derived entirely from observed price dynamics and publicly available news, it requires no voluntary disclosure and is free from rater disagreement.

---

## Repository contents

### Notebooks

| File | Description |
|------|-------------|
| `NYT Climate News.ipynb` | Retrieves climate-related articles via the NYT Archive API (2014–2024), applies keyword filtering to isolate climate and environmental news, and produces `nyt_climate_news_updated.csv` |
| `Jump Diffusion Modeling.ipynb` | Loads the firm price panel and the news dataset; builds the Climate Impact Matrix; applies the \|Z\| > 1 jump rule; forms the Jump Impact Matrix; estimates lambda and k for each firm; computes theta and the min-max normalized 0–100 index; reproduces all paper figures (score histogram, top/bottom 10 firms, jump vs non-jump return distributions, news volume over time, XOM case study) |

### Data files

| File | Description |
|------|-------------|
| `nyt_climate_news_updated.csv` | Filtered climate news dataset with publication dates, produced by `NYT Climate News.ipynb` |
| `Stock_Data.xlsx` | Raw adjusted open and close prices for the 88-firm panel (top 100 US firms by market cap; 12 firms with incomplete price histories excluded) |
| `Stock_Data(Clean).xlsx` | Cleaned version of the same price panel used directly by `Jump Diffusion Modeling.ipynb` |

---

## Pipeline

1. **`NYT Climate News.ipynb`** — requires a [NYT Archive API](https://developer.nytimes.com/docs/archive-product/1/overview) key stored in the environment variable `NYT_API_KEY`. Writes `nyt_climate_news_updated.csv`.
2. **`Jump Diffusion Modeling.ipynb`** — reads `Stock_Data(Clean).xlsx` and `nyt_climate_news_updated.csv`. Because the CSV is already committed, this notebook can be run standalone without Step 1.

---

## Reproduction reference

The table below gives parameter estimates for ExxonMobil (XOM) as a spot-check against the paper's reported values.

| Parameter | Value |
|-----------|-------|
| lambda (jump intensity, jumps/day) | 0.007345 |
| k (mean jump size) | -0.001643 |
| theta = lambda * k | -1.2e-5 |
| Normalized index score | 44.49 |

---

## Citation

```bibtex
@unpublished{hernandez_villamor_jumps,
  author = {Hernandez, Jorge Nestor and Villamor, Enrique},
  title  = {A Jump-Diffusion Framework to Construct an Unbiased Environmental Index},
  note   = {Working paper, Florida International University},
  year   = {2026},
}
```

---

## Acknowledgements

This research was supported by the US Department of Defense under grant **W911NF-25-1-0138**.
