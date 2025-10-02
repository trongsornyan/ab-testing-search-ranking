# ab-testing-search-ranking
This repository contains an end-to-end analysis of a marketing A/B test measuring the impact of a **new search ranking system** on bookings.  
Primary metric: **conversion rate** (booked vs not).  
Guardrail metric: **time_to_booking** (lower is better).

---

## Goal
Evaluate whether a new search ranking system increases booking conversions **without harming** the booking experience. The project demonstrates how rigorous data assessment and statistical testing drive a clear rollout decision.

## Process
1. **Data preparation**: Join `users_data.csv` (experiment assignment) with `sessions_data.csv` (behavior).
2. **Data assessment**: Schema checks, missing values, duplicates, assignment balance, outliers, and temporal coverage.
3. **Sanity check**: **Sample Ratio Mismatch (SRM)** using chi-square.
4. **Hypothesis tests**:
   - Conversion (binary): **Two-sided Z-test for proportions**
   - Time to booking (continuous): **Welch’s t-test**
5. **Effect sizes**: Relative change `(variant_mean / control_mean) - 1` for both metrics.
6. **Decision rule**: Roll out if conversion improves significantly (p < 0.10 & effect > 0) **and** guardrail not harmed (p > 0.10 or faster).

## Insights (from sample run)
- **No SRM**: control 7,630 vs variant 7,653; p = **0.8524**.
- **Conversion**: control **15.92%** vs variant **18.19%** ⇒ **+14.2% relative lift**; p = **0.0002**.
- **Guardrail**: time_to_booking **-0.79%** (faster), p = **0.5365** (not significant; no harm).
- **Decision**: **Full rollout** recommended.

> ✅ Conclusion: The new ranking system **significantly increases conversions** without harming booking speed.
