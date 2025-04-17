# Truer Ratings: Normalizing Google Reviews Data

## Overview

This project analyzes Google review data to identify and correct for systematic voluntary response bias. We observed that average user ratings were skewed lower than the expected neutral value. This repository contains the Python code (in a Jupyter Notebook) used to explore this bias, develop a linear normalization model, and visualize the results.

**Developed for the Carolina Data Challenge (September 2024). Awarded 2nd Place (out of 800+ teams) in the Social Science category.**

## Problem Statement

Online reviews, particularly on platforms like Google, often suffer from voluntary response bias – users with strong opinions (frequently negative) are more likely to contribute. Our initial analysis of the `google_review_ratings.csv` dataset confirmed this, revealing an average user rating significantly below the theoretical neutral midpoint (approx. 2.12 vs. 2.5 on a 1-5 scale, assuming 1 is the minimum allowed rating).

## Objective

To develop and apply a statistical method to normalize Google review ratings, correcting for the observed systematic negative bias. The goal is to adjust ratings to better reflect a 'truer' average sentiment while preserving relative differences between rated items.

## Methodology

1.  **Data Loading & Cleaning:**
    *   Imported the `google_review_ratings.csv` dataset using pandas.
    *   Handled missing values (`NaN`) by filling with 0.0 (assuming non-rated items contribute neutrally to averages where applicable).
    *   Addressed data type errors, specifically correcting a column (`local_services_avg`) where some entries were strings containing tabs (e.g., `"2\t2"`) instead of floats.
    *   Removed irrelevant identifier columns (`User`).

2.  **Exploratory Data Analysis (EDA):**
    *   Calculated the average rating submitted by each user across all categories they rated.
    *   Visualized the distribution of these user averages using a histogram, confirming a right skew (mean ≈ 2.12).

3.  **Bias Calculation & Normalization Approach:**
    *   Calculated the difference (`d_i`) between each user's average rating (`x̄_i`) and the expected mean (2.5).
    *   Calculated category means before (`raw`) and after applying an initial user-level adjustment (`normalized`).
    *   Determined the average difference (`k`) between these raw and normalized category means. This constant `k` (≈ 0.387 after removing an outlier category `garden_avg` with low sample size) represents the average systematic bias observed.

4.  **Linear Adjustment Model:**
    *   Developed a linear model to adjust any given rating `x` to a normalized rating `μ`:
        $$ \mu = \frac{k}{2.5} (x - 5) + x $$
    *   This model anchors the adjustment at (5, 5) (no change for 5-star ratings), increases lower ratings more significantly than higher ratings, and shifts the overall average rating upwards by approximately `k`.

5.  **Visualization:**
    *   Used matplotlib to plot histograms showing the distribution of category means before and after normalization.
    *   Plotted the linear adjustment function against the original rating scale to visualize the model's effect.

## Key Findings

*   A consistent negative bias (`k ≈ 0.387`) was identified across most Google review categories in the dataset.
*   The developed linear normalization model effectively adjusts ratings to counteract this bias.
*   Normalization resulted in a distribution of category averages that better resembles a bell curve centered around an adjusted mean (approx. 2.5 + k/2).

## Technologies Used

*   Python 3
*   Pandas
*   NumPy
*   Matplotlib
*   Jupyter Notebook

## How to Run

1.  Clone this repository.
2.  Ensure you have Python and the required libraries (pandas, numpy, matplotlib) installed.
3.  Place the `google_review_ratings.csv` dataset in the root directory of the repository.
4.  Open and run the `truer_ratings.ipynb` Jupyter Notebook.

## Authors

*   Ivy Nangalia ([@ivynangalia](https://github.com/ivynangalia))
*   Evan Flynn ([@eflynn4](https://github.com/eflynn4))