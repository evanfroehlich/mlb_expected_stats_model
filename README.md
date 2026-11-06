# expected_stats

This project builds an xBA model from Statcast data. The goal is to estimate the probability that a batted ball becomes a hit, then aggregate those probabilities for a batter or season.

## Current milestone

`Data.ipynb` fetches a 2023-2026 Statcast sample, caches the raw response as a Parquet file, keeps batted-ball events, creates an `is_hit` target, checks feature completeness, and fits a logistic-regression baseline. The initial features are launch speed, launch angle, spray coordinates, batter/pitcher handedness, and pitch type. 

The current development check trains on 2023-2025 and tests on 2026. 

## Roadmap

1. Expand the date range and cache the raw Statcast extract. (Complete for the development window)
2. Establish a simple baseline using the overall hit rate. (Complete)
3. Fit a logistic regression with one-hot encoded categorical features. (Complete)
4. Compare it with a nonlinear model such as random forests and gradient boosting (In-progress).
5. Aggregate predicted hit probabilities by batter to create an expected batting average.
6. Extend to xwOBA using multi-label classification models.
