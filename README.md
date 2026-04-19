# Advanced Modeling: Economic Impact of Armed Conflicts
 
**Author:** Sude Boz 
**Date:** March 2026
 
## Overview
 
This project applies supervised learning techniques to analyze the economic consequences of armed conflicts. Using the *War Economic Impact* dataset from Kaggle, the analysis tackles two modeling tasks — one classification and one regression — to understand how socioeconomic indicators relate to black market activity and GDP contraction during and after armed conflicts.
 
## Dataset
 
The *War Economic Impact* dataset (sourced from Kaggle) contains **100,000 observations** of conflicts across different regions, types, and time periods, with **28 variables** covering socioeconomic indicators (unemployment, poverty, inflation, black market activity, informal economy) as well as conflict metadata (type, duration, region, status).
 
For computational efficiency, a random sample of **5,000 observations** was drawn using a fixed seed (2026) for reproducibility. No missing values or duplicates were found, so no imputation or deduplication was required.
 
## Research Tasks
 
### Classification
Predict the **Black Market Activity Level** of each conflict, simplified into a binary target (`BM_High`) that groups High/Dominant activity against Low/Moderate activity.
 
### Regression
Predict the **GDP Change** (percentage change in GDP during the conflict), a continuous variable ranging from approximately -85% to -5%.
 
## Methodology
 
The project is split into interpretation-focused and prediction-focused modeling sections.
 
**Classification models:**
- Logistic Regression with stepwise selection
- Linear Discriminant Analysis (LDA)
- Quadratic Discriminant Analysis (QDA)
- Naive Bayes
- k-Nearest Neighbors (with cross-validation tuning)
- Decision Tree
- Bagging
- Random Forest
**Regression models:**
- Baseline linear regression
- Stepwise selection
- Ridge Regression
- Lasso Regression
- Principal Component Regression (PCR)
- Partial Least Squares (PLS)
Exploratory data analysis preceded modeling, including distribution checks, correlation analysis, and multicollinearity handling (e.g., `During_War_Unemployment` and `Unemployment_Spike` had perfect correlation, so redundant variables were removed).
 
## Key Findings
 
**Classification was challenging.** Linear and probabilistic models performed near random (Balanced Accuracy ≈ 0.50). Tree-based methods (Decision Tree and Random Forest) did marginally better at Balanced Accuracy = 0.540, the only models to statistically outperform random guessing (p < 0.05). Random Forest variable importance highlighted `Start_Year`, `Conflict_Duration`, `Households_Fallen_Into_Poverty_Estimate`, and `Black_Market_Gap` as the strongest predictors, suggesting temporal and poverty-related factors drive black market development — but the signal in the predictors is weak overall.
 
**Regression produced substantially stronger results.** The baseline linear model reached a Test R² of 0.53 with no signs of overfitting. The most important finding is that **conflict type is by far the dominant predictor of GDP decline**: Asymmetric Wars produced the deepest contractions (median ≈ -70%), while other conflict types were associated with 40–47 percentage points less severe economic damage. Stepwise selection trimmed the model down to just 5 variables while preserving nearly identical performance (R² = 0.528), confirming that most predictors in the full model were redundant. Ridge and Lasso offered no improvement since there was no overfitting to correct, and PLS achieved comparable performance to PCR with far fewer components.
 
## Repository Contents
 
- `final_advanced_modeling.qmd` — Quarto source file with all code and analysis
- `final_advanced_modeling.html` — Rendered HTML report
- `README.md` — This file
## How to Reproduce
 
1. Clone the repository.
2. Open the `.qmd` file in RStudio or any Quarto-compatible editor.
3. Install the required R packages: `tidyverse`, `MASS`, `e1071`, `class`, `rpart`, `randomForest`, `glmnet`, `pls`, `caret`, `corrplot`.
4. Render with `quarto render final_advanced_modeling.qmd` or click "Render" in RStudio.
The random seed (2026) is fixed throughout the analysis to ensure reproducibility.final_advanced_modeling.html — Rendered HTML report
README.md — This file

How to Reproduce

Clone the repository.
Open the .qmd file in RStudio or any Quarto-compatible editor.
Install the required R packages: tidyverse, MASS, e1071, class, rpart, randomForest, glmnet, pls, caret, corrplot.
Render with quarto render final_advanced_modeling.qmd or click "Render" in RStudio.

The random seed (2026) is fixed throughout the analysis to ensure reproducibility.
