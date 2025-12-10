# STA 610 Case Study: Diazepam Street Pricing Analysis

**Author:** Zixiao Tan

## Overview

This project analyzes street pricing data for Diazepam (a benzodiazepine) using hierarchical modeling techniques. The analysis explores factors associated with price per milligram (ppm) and investigates geographic heterogeneity in pricing across different U.S. states.

## Research Questions

1. Which variables are associated with pricing per milligram of Diazepam?
2. Is there heterogeneity in pricing of Diazepam by location?

## Data

The analysis uses the **StreetRx** dataset, which contains crowdsourced street drug pricing information. Key variables include:

- **ppm**: Price per milligram (outcome variable)
- **mgstr**: Dosage strength (2mg, 4mg, 5mg, 10mg)
- **bulk_purchase**: Indicator for purchases of 10+ units
- **source**: Source of information (Heard of, Internet, Personal)
- **state**: U.S. state where purchased
- **year**: Year of purchase

## Methodology

### Statistical Approach
- **Model Type**: Hierarchical linear mixed model with random intercepts by state
- **Response Transformation**: Log transformation of ppm to meet normality assumptions
- **Fixed Effects**: Dosage strength (mgstr), bulk purchase indicator, source of information
- **Random Effects**: State-level intercepts to capture geographic variation
- **Model Selection**: Exhaustive search with BIC criterion across 1,024 candidate models

### Analysis Framework
- **Frequentist Approach**: Maximum likelihood estimation using `lme4`
- **Bayesian Approach**: MCMC sampling using `brms` with non-informative priors
- **Model Diagnostics**: Residual analysis, influential group detection, assumption checks

## Key Findings

- **Dosage Effects**: Pricing per mg varies significantly across dosage strengths
- **Bulk Discounts**: Bulk purchases are approximately 12.4% cheaper per mg
- **Source Differences**: Internet sources show 33% lower prices compared to word-of-mouth, while personal reports are 10% lower
- **Geographic Variation**: Significant heterogeneity in baseline pricing across states
- **Model Convergence**: Frequentist and Bayesian estimates are nearly identical

## Project Structure

```
.
├── case_study.Rmd              # Main analysis R Markdown file
├── case_study_report.Rmd       # Report version
├── streetrx.RData              # Dataset
├── presentation/               # Presentation materials
└── README.md                   # This file
```

## Requirements

### R Packages
```r
tidyverse, lme4, rstan, brms, knitr, kableExtra,
patchwork, lubridate, gridExtra, influence.ME
```

## Usage

To reproduce the analysis:

1. Load the required R packages
2. Open `case_study.Rmd` in RStudio
3. Knit the document to generate the PDF report

```r
# In R console
rmarkdown::render("case_study.Rmd")
```

## Presentation Video

Watch the project presentation on YouTube:

**[STA 610 Case Study Presentation](https://www.youtube.com/watch?v=f6dPuEkmfMs)**

## Limitations

- High within-state variance remains unexplained
- Normality assumption shows deviations in residual tails
- Some influential groups (e.g., Texas) detected but retained due to large sample sizes
- Missing data in `primary_reason` variable excluded from analysis

## License

This project was completed as part of Duke University's STA 610 course.
