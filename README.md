# IPL Powerplay Score Prediction Using Weighted Ridge Regression

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-Machine_Learning-orange)
![Project](https://img.shields.io/badge/Type-Course_Project-green)

## Overview

This project predicts a team's final Powerplay score (runs after 6 overs) using information available after the first 3 overs of an IPL innings. A Weighted Ridge Regression model is trained on historical IPL ball-by-ball data, incorporating match context and venue effects.

## Features

- Runs after 3 overs (R3)
- Wickets lost (W3)
- Dot balls
- Boundaries
- Momentum
- Chasing indicator
- Venue information

## Target

The target variable is the total runs scored after 6 overs:

$$
Y_6 = \text{Powerplay Score}
$$

Instead of predicting \($Y_6\$) directly, the model predicts a correction to the baseline estimate:

$$
\text{Baseline} = 2 \times R_3
$$

$$
\text{Correction} = Y_6 - (2 \times R_3)
$$

## Model

- Weighted Ridge Regression
- Exponential time-based weighting
- Venue one-hot encoding
- Chronological train-test split

## Dataset

IPL ball-by-ball match data from multiple seasons.

### Training Set

- Seasons before 2023

### Test Set

- Seasons from 2023 onwards

## Results

| Metric | Value |
|----------|----------|
| Test Matches | 293 |
| Test Innings Evaluated | 582 |
| RMSE | **10.34 Runs** |

## Workflow

1. Extract IPL ball-by-ball data
2. Generate first-3-over features
3. Compute baseline estimate
4. Train Weighted Ridge Regression model
5. Predict Powerplay scores
6. Evaluate using RMSE

## Frameworks Used

- Python
- NumPy
- Pandas
- SciPy
- Matplotlib

## Future Improvements

- Include batter and bowler quality metrics.
- Incorporate team strength information.
- Add pitch and weather conditions.
- Explore non-linear models such as XGBoost and LightGBM.
- Develop a real-time Powerplay score prediction system.
