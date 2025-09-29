# Mod4_FinalProject

## Overview

This project analyzes hourly bike-share data to extract actionable insights for business and product decisions. Using Python and Jupyter Notebooks, we explore trends, perform hypothesis testing, and conduct an A/B analysis to inform recommendations for staffing, promotions, and bike availability.



## Key Insights & EDA

### Top 3 Trends

1. **Higher Usage During Working Hours and Weekdays**  
   Peak demand occurs during commuting hours (7–9 AM and 4–6 PM) on weekdays, suggesting staffing and bike availability should prioritize these periods.

2. **Seasonal Variation**  
   Bike usage is highest in summer and lowest in winter, highlighting opportunities for seasonal promotions or dynamic pricing to balance demand.

3. **Weather Impact**  
   Extreme temperatures and rain reduce usage significantly, which can inform forecasting and contingency planning for low-demand days.

### Data Quality & Interpretation

- Minimal missing values; no significant imputation needed.  
- Continuous variables (temperature, humidity, windspeed) normalized for consistency.  
- Statistical summaries confirm reasonable distributions; outliers examined for business relevance.



## Hypothesis Testing

### Q1: Difference in Mean Usage on Working vs Non-Working Days

- **Test**: Two-sample t-test (independent)  
- **Rationale**: Comparing means between two independent groups.  
- **Results**:  
  - Working day mean = 193.21 rides/hour  
  - Non-working day mean = 181.41 rides/hour  
  - t-statistic = 4.095  
  - p-value = 0.00004  
  - 95% CI: [6.15, 17.45]  
- **Practical Significance**: Higher usage on working days informs staffing and bike allocation.  
- **Assumptions**: Independent samples, approximately normal distributions; verified via descriptive stats and visual checks.

### Q2: Effect of Season on Usage

- **Test**: One-way ANOVA  
- **Rationale**: Comparing means across more than two groups (seasons).  
- **Results**:  
  - F-statistic = 409.18  
  - p-value ≈ 7.40 × 10⁻²⁵⁷  
- **Interpretation**: Seasonal differences in usage are extremely significant; summer demand is highest, winter lowest.  
- **Assumptions**: Homogeneity of variance and independence; variance similarity confirmed via visual checks.



## A/B Test: Evening Usage Intervention

**Eligibility:** Working days, 5–7 PM (hours 17–19), favorable weather (weathersit 1 or 2), humidity ≤ 0.70  

**Test:** Two-sample t-test (unequal variance) comparing pre-launch vs post-launch counts  

**Balance Table (weekday × hour):**

| Weekday | Hour | Pre | Post |
|---------|------|-----|------|
| 1       | 17   | 3   | 3    |
| 1       | 18   | 2   | 2    |
| 1       | 19   | 2   | 2    |
| 2       | 17   | 3   | 3    |
| 2       | 18   | 2   | 2    |
| 2       | 19   | 3   | 3    |
| 3       | 17   | 3   | 3    |
| 3       | 18   | 3   | 3    |
| 3       | 19   | 3   | 3    |
| 4       | 17   | 4   | 4    |
| 4       | 18   | 4   | 4    |
| 4       | 19   | 3   | 3    |
| 5       | 17   | 4   | 4    |
| 5       | 18   | 4   | 4    |
| 5       | 19   | 3   | 3    |

**Weather Mix (counts):**

| Weathersit | Pre | Post |
|------------|-----|------|
| 1          | 37  | 41   |
| 2          | 9   | 5    |

**Guardrail Metrics (group means):**

| Metric      | Pre       | Post      |
|------------|-----------|-----------|
| registered | 120.3     | 128.4    |
| casual     | 104.46    | 87.76    |
| temp       | 0.779     | 0.670    |
| hum        | 0.485     | 0.524    |
| windspeed  | 0.209     | 0.229    |

**Sample Sizes and Primary Metric:**

- Pre: 45 slots  
- Post: 45 slots  
- Mean counts: Pre = A_cnt.mean()  
- Post = B_cnt.mean()  
- Mean difference (Post − Pre) = 43.78 rides/hour  
- t-statistic = -1.567  
- p-value = 0.1206  
- 95% CI: [-11.72, 99.29]  
- Reject H0? No (not statistically significant)  
- Practically significant (≥ 5 rides/hour)? Yes  

**Interpretation:**  

While the observed increase in evening bike usage (≈44 rides/hour) exceeds the practical threshold, the result is **not statistically significant** at α = 0.05. The wide confidence interval, which includes negative values, indicates uncertainty in the effect. Guardrail metrics and balance checks confirm pre/post groups are comparable. Recommendation: consider additional testing or a larger sample before deploying this intervention.


## Guiding Questions Addressed

1. **α Rationale**: α = 0.05 balances false alarms (ineffective strategies) vs. missed opportunities (underutilized promotions).  
2. **Statistical vs Practical Significance**: Only results exceeding the practical threshold (e.g., +5 rides/hour) are recommended for action.  
3. **Threats to Conclusions**: Non-random events (holidays, special events) could bias results. Independence and variance assumptions were verified; randomized pilots could improve robustness.  
4. **Equity Considerations**: Analysis could disadvantage low-demand neighborhoods if bikes are reallocated solely based on peak usage. Mitigation: ensure minimum service levels and equitable distribution policies.


## Repository Structure

- **data/**: Raw and processed datasets  
- **figures/**: Visualizations for EDA and presentation  
- **notebooks/**: Jupyter Notebooks with analysis code  
- **slides/**: Stakeholder-ready presentation  
- **README.md**: Project overview, insights, and detailed results  


