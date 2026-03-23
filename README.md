# Housing Affordability & Life Satisfaction in Canada

**Modeling the impact of rising rental costs on Canadian well-being using machine learning and SHAP interpretability**

> DATA5000 Project — Carleton University  
> Noah Kasdorf, Chloé Lachance-Soulard, Emily Larkin

---

## Overview

Canada's housing affordability crisis extends beyond financial strain — it affects mental health and overall life satisfaction. This project investigates whether housing affordability, measured as expected rent stress (rent-to-income ratio), predicts life satisfaction for Canadians, and identifies which populations are most vulnerable to rising rental costs.

We merge individual-level health survey data with regional rental market data, train predictive models, and use a 2020→2025 counterfactual scenario to estimate how worsening affordability has impacted well-being across demographic groups.

## Research Questions

1. Has housing affordability decreased since 2020, and how has this affected life satisfaction?
2. How important is housing affordability in predicting life satisfaction?
3. Which Canadians face the most prominent rental stress (by income, age, and region)?

## Data Sources

| Dataset | Year | Records | Source |
|---|---|---|---|
| Canadian Community Health Survey (CCHS) | 2020 | 101,822 respondents | [Kaggle](https://www.kaggle.com/datasets/aradhanahirapara/healthcare-survey) |
| CMHC Rental Market Survey | 2020 | 10 provinces, 37 regional rates | [CMHC](https://www.cmhc-schl.gc.ca/) |
| CMHC Rental Market Survey | 2025 | 10 provinces, 37 regional rates | [CMHC](https://www.cmhc-schl.gc.ca/) |

## Methodology

1. **Merge datasets** — Match CCHS health regions to CMHC rental regions at the CMA or provincial level
2. **Engineer features** — Compute `Affordability_Stress = (Regional Rent × 12) / Annual Income`, adjusted for household size
3. **Drop features** — Remove data leaks (self-reported mental/general health), mediators (stress level, sense of belonging), and redundant columns
4. **Train models** — Compare Linear Regression vs. XGBoost with 5-fold cross-validation
5. **Counterfactual analysis** — Swap in 2025 rents with wage-adjusted incomes to estimate the predicted shift in life satisfaction

## Key Findings

| Metric | Value |
|---|---|
| XGBoost CV R² | 0.202 ± 0.004 |
| Mean Absolute Error | 1.14 pts (0–10 scale) |
| SHAP rank of Affordability Stress | #5 of 42 features (5.8% of attribution) |
| Mean predicted life satisfaction drop (2020→2025) | −0.037 pts (p < .001, Cohen's d = −0.65) |

- **Income:** Low-income Canadians (<$40k) experience ~1.6× the average drop
- **Age:** Remarkably uniform impact across all adult cohorts (−0.035 to −0.037)
- **Urban vs. Rural:** Smaller centres hit harder (−0.042) than major CMAs (−0.018) due to proportionally larger rent increases from lower baselines
- **30% threshold validated:** SHAP dependence plot confirms the CMHC 30% rent-to-income guideline as a well-being inflection point


## Requirements

```
python >= 3.9
pandas
numpy
scikit-learn
xgboost
shap
matplotlib
seaborn
scipy
```

Install dependencies:

```bash
pip install pandas numpy scikit-learn xgboost shap matplotlib seaborn scipy
```

## Running the Analysis

1. Clone the repository
2. Place the data files in the `Data/` directory
3. Open and run `Housing_Affordability_Analysis.ipynb` from top to bottom

The notebook is self-contained — it loads data, engineers features, trains models, runs the counterfactual, and produces all figures.
# Housing Affordability & Life Satisfaction in Canada

**Modeling the impact of rising rental costs on Canadian well-being using machine learning and SHAP interpretability**

> DATA5000 Project — Carleton University  
> Noah Kasdorf, Chloé Lachance-Soulard, Emily Larkin

---

## Overview

Canada's housing affordability crisis extends beyond financial strain — it affects mental health and overall life satisfaction. This project investigates whether housing affordability, measured as expected rent stress (rent-to-income ratio), predicts life satisfaction for Canadians, and identifies which populations are most vulnerable to rising rental costs.

We merge individual-level health survey data with regional rental market data, train predictive models, and use a 2020→2025 counterfactual scenario to estimate how worsening affordability has impacted well-being across demographic groups.

## Research Questions

1. Has housing affordability decreased since 2020, and how has this affected life satisfaction?
2. How important is housing affordability in predicting life satisfaction?
3. Which Canadians face the most prominent rental stress (by income, age, and region)?

## Data Sources

| Dataset | Year | Records | Source |
|---|---|---|---|
| Canadian Community Health Survey (CCHS) | 2020 | 101,822 respondents | [Kaggle](https://www.kaggle.com/datasets/aradhanahirapara/healthcare-survey) |
| CMHC Rental Market Survey | 2020 | 10 provinces, 37 regional rates | [CMHC](https://www.cmhc-schl.gc.ca/) |
| CMHC Rental Market Survey | 2025 | 10 provinces, 37 regional rates | [CMHC](https://www.cmhc-schl.gc.ca/) |

## Methodology

1. **Merge datasets** — Match CCHS health regions to CMHC rental regions at the CMA or provincial level
2. **Engineer features** — Compute `Affordability_Stress = (Regional Rent × 12) / Annual Income`, adjusted for household size
3. **Drop features** — Remove data leaks (self-reported mental/general health), mediators (stress level, sense of belonging), and redundant columns
4. **Train models** — Compare Linear Regression vs. XGBoost with 5-fold cross-validation
5. **Counterfactual analysis** — Swap in 2025 rents with wage-adjusted incomes to estimate the predicted shift in life satisfaction

## Key Findings

| Metric | Value |
|---|---|
| XGBoost CV R² | 0.202 ± 0.004 |
| Mean Absolute Error | 1.14 pts (0–10 scale) |
| SHAP rank of Affordability Stress | #5 of 42 features (5.8% of attribution) |
| Mean predicted life satisfaction drop (2020→2025) | −0.037 pts (p < .001, Cohen's d = −0.65) |

- **Income:** Low-income Canadians (<$40k) experience ~1.6× the average drop
- **Age:** Remarkably uniform impact across all adult cohorts (−0.035 to −0.037)
- **Urban vs. Rural:** Smaller centres hit harder (−0.042) than major CMAs (−0.018) due to proportionally larger rent increases from lower baselines
- **30% threshold validated:** SHAP dependence plot confirms the CMHC 30% rent-to-income guideline as a well-being inflection point


## Requirements

```
python >= 3.9
pandas
numpy
scikit-learn
xgboost
shap
matplotlib
seaborn
scipy
```

Install dependencies:

```bash
pip install pandas numpy scikit-learn xgboost shap matplotlib seaborn scipy
```

## Running the Analysis

1. Clone the repository
2. Place the data files in the `Data/` directory
3. Open and run `Housing_Affordability_Analysis.ipynb` from top to bottom

The notebook is self-contained — it loads data, engineers features, trains models, runs the counterfactual, and produces all figures.
