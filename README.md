# Predicting Melbourne Housing Prices with Bayesian Hierarchical Models  

This repository contains the code, analysis, and report developed as part of the Statistics and Probability course project at Bocconi University, Master of Science in Business Analytics and Data Science. The project applies Bayesian hierarchical modeling with MCMC methods to analyze and predict housing prices in Melbourne.

**Project Title:** Bayesian Hierarchical Modeling for Melbourne Housing Prices


## Project Overview  

Housing affordability and variability in Melbourne are influenced by property characteristics, location, and temporal dynamics. This project investigates the determinants of housing prices in Melbourne (2016–2017 dataset), accounting for structural, spatial, and seasonal effects.  

**Key steps:**  
- Exploratory Data Analysis (EDA) to uncover structural, temporal, and spatial trends.  
- Data cleaning, outlier removal, and feature engineering (log transformation, dummy variables, seasonality terms).  
- Hierarchical Bayesian modeling using MCMC methods, including fixed and random effects.  
- Model evaluation with predictive performance metrics (RMSE, MAE).  


## Key Findings  

- **Structural attributes:** Each additional room is associated with ~16% higher predicted price (log scale); car spaces also increase price, while **distance from the CBD** reduces price.  
- **Property type effects:** Townhouses and units are priced lower than houses on the log scale.  
- **Spatial variability:** Strong random effects by **council areas** and **regions**.  
- **Temporal trends:** Seasonal patterns in both prices and transaction volumes (captured via month effects).  
- **Performance:** RMSE = **0.234** on the log scale; MAE ≈ **$177,196** on the price scale, indicating robust predictive power.  


## Repository Structure  

- **EDA_housing.html**  
  Interactive exploratory data analysis (distributions, trends, spatial views).  

- **MCMC model.Rmd**  
  RMarkdown implementing the Bayesian hierarchical model with MCMC (Metropolis for fixed effects; Gibbs for random effects/variances).  

- **Final_Report.pdf**  
  Final report covering methodology, results, and conclusions.

- **housing.csv**  
  Dataset provided as part of the assignment


## Methods Summary  

### Data Preparation  
- Imputation of missing **CouncilArea** from postcode mapping; numeric NAs filled with medians.  
- Outlier removal on **Price** (IQR rule); log-transform of price.  
- Feature engineering: dummies for **Type** and **Method**, month-based **seasonality** (sin/cos), interactions (e.g., Rooms × Type, Car × Distance).  
- Train/test split (80/20).  

### Modeling  
- **Likelihood (log price):**  
  LogPrice_i ~ Normal(μ_i, σ²)  

- **Linear predictor:**  
  μ_ij = β₀ + Σ βₖ X_ijk + u_CouncilArea + u_Region + u_Month

- **Fixed effects:** Rooms, Car, Distance (CBD), Seasonality, YearBuilt, Method, interactions.  
- **Random effects:** Council area, region, month.  
- **Priors:** Weakly-informative Normals for \(\beta\); Inverse-Gamma for variances.  

### MCMC Implementation  
- **Metropolis** updates for fixed effects \(\beta\).  
- **Gibbs** updates for random effects and variance components.  
- Typical run: 50,000 iterations, 10,000 burn-in, thinning every 20.  


## Reproducibility  

- **Software:** R (≥ 4.2)  
- **Key packages:** `tidyverse`, `data.table`, `lme4`, `coda`, `ggplot2`

## Authors
- Caretti Giorgio Filippo
- Lorenzana Luca Garcia
- Milani Luca
- Muraro Margherita

## Contacts
For any inquiries, please contact:
- luca.milani2@studbocconi.it
