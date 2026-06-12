# IPL Powerplay Score Prediction Using Weighted Ridge Regression

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-Machine_Learning-orange)
![Project](https://img.shields.io/badge/Type-Course_Project-green)

## Overview

In T20 cricket, the first six overs of an innings, known as the **Powerplay**, often play a crucial role in determining the momentum of the batting team. This project develops a machine learning model to predict a team's final Powerplay score (runs scored after six overs) using information available after the first three overs.

The project combines cricket-specific feature engineering with a weighted ridge regression framework to estimate the expected score at the end of the Powerplay.

---

## Problem Statement

Given the state of an innings after the first three overs, predict the total runs scored at the end of six overs.

The prediction uses:

- Runs scored after three overs
- Wickets lost
- Dot balls
- Boundaries scored
- Momentum in scoring rate
- Innings context
- Venue information

---

## Dataset

The project uses IPL ball-by-ball match data.

Each delivery contains information such as:

- Match ID
- Innings number
- Over and ball number
- Runs scored
- Extras
- Wickets
- Venue

The raw match files are processed to generate innings-level observations suitable for supervised learning.

---

## Feature Engineering

For each innings, information from the first three overs is used to construct the feature set.

### 1. Runs After Three Overs (R3)

Total runs scored during the first three overs.

### 2. Wickets Lost (W3)

Number of wickets lost within the first three overs.

### 3. Dot Balls

Count of deliveries that produced zero runs.

### 4. Boundaries

Total number of fours and sixes scored.

### 5. Momentum

Measures whether the batting side is accelerating or slowing down.

Formula:

`Momentum = Runs in 3rd Over - Average Runs per Over`

Positive values indicate an increasing scoring rate, while negative values indicate declining momentum.

### 6. Chasing Indicator

Binary variable:

- `0` = First Innings
- `1` = Second Innings

### 7. Venue Effects

Venue-specific dummy variables are created to account for differences in scoring conditions across stadiums.

---

## Target Variable

The target variable is:

`Y6 = Total Runs After Six Overs`

which represents the final Powerplay score.

---

## Baseline Estimation

A cricket-inspired baseline estimate is first computed:

`Baseline Score = 2 × R3`

Since the first half of the Powerplay has already been completed, doubling the three-over score provides a reasonable initial estimate.

Instead of predicting the final score directly, the model predicts the correction term:

`Correction = Actual Powerplay Score − Baseline Score`

This approach simplifies the learning task and improves model stability.

---

## Model Formulation

The final prediction is computed as:

`Predicted Powerplay Score = 2 × R3 + Model Correction`

where:

- `R3` is the score after three overs.
- `2 × R3` serves as a cricket-inspired baseline estimate.
- `Model Correction` is learned using weighted ridge regression.

---

## Model

The project uses **Weighted Ridge Regression**.

### Why Ridge Regression?

- Reduces overfitting
- Handles correlated features
- Produces stable coefficient estimates
- Performs well with venue dummy variables

### Time-Based Weighting

Recent IPL seasons are assigned higher weights than older seasons.

This reflects the evolution of modern T20 cricket, where scoring rates have increased over time. The weighting scheme uses an exponential decay function to gradually reduce the influence of older matches.

---

## Training and Testing Strategy

The dataset is split chronologically.

### Training Set

- IPL seasons before 2023

### Testing Set

- IPL seasons from 2023 onwards

This prevents information leakage and better simulates real-world prediction scenarios.

---

## Evaluation Metric

Model performance is evaluated using **Root Mean Squared Error (RMSE)**.

RMSE measures the average magnitude of prediction errors and penalizes large mistakes more heavily. Lower RMSE values indicate better predictive performance.

---

## Project Workflow

1. Extract IPL ball-by-ball data
2. Process innings-level information
3. Generate first-three-over features
4. Compute baseline Powerplay estimate
5. Train weighted ridge regression model
6. Predict six-over scores
7. Evaluate performance using RMSE

---

## Key Insights

- Runs scored after three overs are the strongest predictor of the final Powerplay score.
- Momentum provides useful information about short-term batting trends.
- Venue conditions contribute significantly to scoring variation.
- Recent IPL seasons should be weighted more heavily due to changing batting strategies.

---

## Technologies Used

- Python
- NumPy
- Pandas
- Matplotlib
- Scikit-learn

---

## Learning Outcomes

Through this project, the following concepts were explored:

- Sports Analytics
- Feature Engineering
- Regression Modeling
- Regularization Techniques
- Time-Weighted Learning
- Model Evaluation and Validation
- Cricket Data Analysis

---

## Future Improvements

Potential extensions include:

- Incorporating team strength metrics
- Including batter and bowler quality indicators
- Adding pitch and weather information
- Exploring non-linear models such as XGBoost and LightGBM
- Developing real-time Powerplay prediction systems

---
