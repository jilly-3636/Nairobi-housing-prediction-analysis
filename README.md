# Nairobi-housing-prediction-analysis


A worked statistics analysis of 1,486 rental listings across 110 neighbourhoods in Nairobi, Kiambu, Kajiado and Machakos counties. It moves from describing the data (averages, spread, distributions) to testing hypotheses with both parametric (t-tests, ANOVA, Pearson) and non-parametric (Wilcoxon, Mann–Whitney, Kruskal–Wallis, Spearman, chi-square) methods.

## Data
`data/nairobi_rentals_reemio.csv`, collected from Reemio Listings (listings.reemioltd.com) on 19 September 2026; listing dates run from December 2025 to September 2026.

**Real columns:** listing date, location (neighbourhood, sub-county, county), market segment, property type, bedrooms, bathrooms, balconies, floor level, building ID, rent, deposit. `distance_to_cbd_km` is derived from neighbourhood coordinates.

**Simulated for teaching:** `size_sqm`, `building_age_years`, `furnished`, `parking`, `gym`, `borehole`, `peak_commute_min`, `rent_kes_2025`, `days_on_market`, `building_occupancy_pct`, `tenant_satisfaction_10`, `listed_by`. Findings based on these columns say nothing about the real Nairobi market.


## Key findings
1. **Typical rent is far below the average.** Median asking rent is KES 25,000 but the mean is KES 33,753, because a small number of very expensive homes (119 listings above KES 65,500) pull the average up. About 69% of listings are cheaper than the mean.
2. **Location matters, but not for every county.** For 2-bedroom units, only Kiambu and Nairobi differ significantly (Nairobi about KES 11,000 higher); Kruskal–Wallis agrees that counties differ. Further from the CBD, rent tends to fall (Pearson r = −0.38, Spearman ρ = −0.47).
3. **Listings with parking rent for much more** (simulated feature linked to real rent): 2-bedroom units with parking average about KES 41,400 vs 25,200 without, roughly 50% more on a log scale.
4. **Rents rose about 4% year on year** (about KES 1,357 per unit, paired t-test, p < 0.001). An *independent* t-test on the same columns would wrongly show no difference, which is why paired data need paired tests.
5. **Listings are posted on weekdays.** Tuesday has 334 listings and Sunday only 17 (chi-square goodness of fit, p < 0.001).

![Rent by bedrooms](images/B4_rent_by_bedrooms_boxplot.png)
![Distance to CBD vs rent](images/D13_scatter.png)

## Caveats
Units in the same building are not independent observations, so p-values here are likely somewhat too small; see the extension section of the notebook.

## Tools
Python, pandas, NumPy, SciPy, statsmodels, matplotlib, seaborn, Jupyter.
