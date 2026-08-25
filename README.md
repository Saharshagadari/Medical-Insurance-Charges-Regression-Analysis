# Medical Insurance Charges — Regression Analysis

Looking at what drives individual health insurance costs, using an interpretable OLS regression: formal hypothesis testing, an interaction term motivated by a pattern found in the data, and classical regression assumption checks.

## Key Findings

- **Smoking status is the dominant cost driver.** Median charges are **$34,545 for smokers vs. $7,419 for non-smokers** — confirmed with a Mann-Whitney U test (p ≈ 9.7e-118).
- **The effect of BMI depends on smoking status.** Adding an interaction term for this raised the model's R² from 0.705 to **0.842** and cut RMSE by 27% ($6,320 → $4,617).
- **Region has no statistically significant effect** on charges (Kruskal-Wallis p ≈ 0.20).
- **6 of 10 model coefficients are statistically significant at p < 0.05** (age, smoker, bmi, children, and both engineered interaction features) — confirmed with `statsmodels.OLS`. Region and sex are not significant, consistent with the Kruskal-Wallis result above.

## Tech Stack

**Python** end-to-end: pandas and NumPy for cleaning and data manipulation, scikit-learn and statsmodels for modeling and inference, SciPy for hypothesis testing, matplotlib/seaborn for visualization.

## Methodology

- **Cleaning** is handled in pandas: dropping nulls, standardizing category labels, stripping the `$` prefix from `charges`, and correcting sign errors — with a re-validation step after every type coercion .
- **Non-parametric hypothesis tests** (Mann-Whitney U, Kruskal-Wallis) are used instead of a t-test/ANOVA because a Shapiro-Wilk test confirms `charges` is not normally distributed — using the parametric versions here would violate their own assumptions.
- **Model choice** is based on RMSE/MAE in the target's original units (dollars), not just R², since R² alone can mask exactly where a model's errors are concentrated — see the residual analysis in Section 6 of the notebook.

