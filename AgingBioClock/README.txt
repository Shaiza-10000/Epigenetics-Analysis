# Multiple Biomarkers of Aging

## Overview

This notebook evaluates multiple **epigenetic aging clocks** across two EPIC array datasets. It uses the [Biolearn](https://github.com/bio-learn/biolearn) library an open-source Python framework by the Biomarkers of Aging Consortium to load methylation data directly from GEO and run standardized aging clock predictions.

**Paper reference:** Ying et al. (2023). *Biolearn, an open-source library for biomarkers of aging.* bioRxiv. https://doi.org/10.1101/2023.12.02.569722

---

## Requirements

```bash
pip install biolearn matplotlib pandas numpy
```

---

## Datasets

| Dataset | Description | Platform | Samples |
|---|---|---|---|
| **GSE120307** | Broad age-range blood methylation dataset (used in official Biolearn docs) | Illumina 450k | varied |
| **GSE41169** | Dutch population blood methylation study with age & sex metadata | Illumina 450k | 95 |

Both datasets are loaded automatically via `DataLibrary` no manual downloading required.

---

## Aging Clocks Used

8 clocks spanning three generations of epigenetic clock development:

| Clock | Year | Description |
|---|---|---|
| **Horvathv1** | 2013 | Original pan-tissue clock, 353 CpGs across 51 tissue types |
| **Hannum** | 2013 | Blood-specific clock using 71 CpGs |
| **PhenoAge** | 2018 | Second-generation clock predicting phenotypic age via clinical biomarkers |
| **DunedinPACE** | 2022 | Predicts *pace* of aging (rate), not age in years |
| **Lin** | 2016 | Blood-specific clock using 99 CpGs |
| **Zhang_10** | 2019 | Mortality-associated clock using only 10 CpGs |
| **YingCausAge** | 2022 | Causality-enriched clock targeting CpGs with causal links to aging |
| **YingDamAge** | 2022 | Causality-enriched clock targeting biological damage accumulation |

> **Note:** DunedinPACE is excluded from age prediction plots since it outputs a dimensionless pace-of-aging rate, not years.

---

## Analyses & Outputs

### 1. Correlation Matrix
Shows how strongly each pair of clocks agree when ranking samples by predicted age. Produced for both datasets separately.

### 2. Age Prediction Plots
Scatter plots of predicted age vs. chronological age for each clock (excluding DunedinPACE). Tighter scatter around the diagonal = higher accuracy.

### 3. Age Deviation Heatmap
Per-sample, per-clock deviation (predicted − actual age). Warm colors = biologically older than real age; cool colors = biologically younger.

### 4. Mean Absolute Error (MAE) Comparison
Bar chart quantifying average prediction error (in years) per clock across both datasets.

### 5. Predicted Age Distribution
Box plots showing each clock's predicted age distribution, compared against the dataset's mean chronological age.

---

## Key Concepts

- **Epigenetic aging clock** - a model that predicts biological/chronological age from DNA methylation patterns at specific CpG sites.
- **Regression to the mean** - a known limitation of linear clocks where predictions compress at age extremes (predicting too high for young, too low for old).
- **MAE (Mean Absolute Error)** - average number of years a clock's prediction deviates from true age; lower is better.