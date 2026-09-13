# expected_stats

This project builds an xBA-style model from Statcast data. The goal is to estimate the probability that a batted ball becomes a hit, then aggregate those probabilities for a batter or season.

## Current milestone

`Data.ipynb` fetches an April-May 2024 Statcast sample, caches the raw response as a Parquet file, keeps batted-ball events, creates an `is_hit` target, checks feature completeness, and fits a logistic-regression baseline. The initial features are launch speed, launch angle, spray coordinates, batter/pitcher handedness, and pitch type. The notebook also aggregates contact-level probabilities into batter-level expected batting averages.

The current development check trains on April 1-May 30, 2024 and tests on May 31, 2024. It is useful for verifying the pipeline, but a single holdout date is still too small to represent final model performance.

## Roadmap

1. Expand the date range and cache the raw Statcast extract. (Complete for the development window)
2. Establish a simple baseline using the overall hit rate. (Complete)
3. Fit a logistic regression with one-hot encoded categorical features. (Complete)
4. Compare it with a nonlinear model such as gradient boosting.
5. Split by date: train on earlier games and test on later games to avoid temporal leakage.
6. Evaluate log loss, Brier score, calibration, and grouped accuracy by launch-speed/angle bins.
7. Aggregate predicted hit probabilities by batter to create an expected batting average. (Complete)

## Modeling notes

- Define the target before fitting: singles, doubles, triples, and home runs count as hits; outs and errors do not.
- Do not use `events` as a model feature because it directly contains the target outcome.
- Report both model performance and calibration. A useful expected-stat model should produce probabilities that behave like probabilities, not only maximize classification accuracy.