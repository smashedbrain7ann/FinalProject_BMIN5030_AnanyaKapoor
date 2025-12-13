# Final Project: Causal Effects of Insomnia on Major Depressive Disorder  
**BMIN5030 – Data Science for Biomedical Informatics**

**Author:** Ananya Kapoor  

---

## Project Overview

This repository contains my final project for **BMIN5030: Data Science for Biomedical Informatics**.  
The project uses **two-sample Mendelian randomization (MR)** to test whether **genetic liability to insomnia causally increases the risk of major depressive disorder (MDD)**.

Observational studies consistently report strong associations between sleep disturbances and depression, but these relationships are vulnerable to **confounding** and **reverse causation**. Mendelian randomization leverages genetic variants as instrumental variables to strengthen causal inference under well-defined assumptions.

The analysis pairs genome-wide significant insomnia variants from **UK Biobank** with an independent **Psychiatric Genomics Consortium (PGC)** depression GWAS and applies multiple MR estimators and sensitivity analyses to assess robustness.

---

## Research Question

> Does genetic liability to insomnia causally increase the risk of major depressive disorder?

---

## Data Sources

All genetic summary statistics are accessed via **OpenGWAS**.

### Exposure GWAS
- **Trait:** Sleeplessness / insomnia  
- **Cohort:** UK Biobank  
- **OpenGWAS ID:** `ukb-b-3957`  
- **Sample size:** ~460,000 individuals  

### Outcome GWAS
- **Trait:** Major Depressive Disorder (MDD)  
- **Consortium:** Psychiatric Genomics Consortium (PGC)  
- **OpenGWAS ID:** `ieu-a-1188`  
- **Sample size:** ~170,000 individuals  

The exposure and outcome GWAS are independent, satisfying the requirements of a two-sample MR design.

---

## Methods Summary

### Instrument Construction and Data Cleaning
- Genome-wide significant SNPs selected (p < 5×10⁻⁸)
- LD clumping applied (r² < 0.001, 10 Mb window)
- Allele harmonization performed across exposure and outcome
- Palindromic SNPs with intermediate allele frequencies removed
- Instrument strength evaluated using F-statistics (F > 10 threshold)

### Mendelian Randomization Analyses
- **Primary estimator:** Inverse-variance weighted (IVW) MR
- **Sensitivity estimators:**  
  - MR-Egger  
  - Weighted median  
  - Simple median  

### Robustness and Bias Diagnostics
- Cochran’s Q test (heterogeneity)
- MR-Egger intercept test (directional pleiotropy)
- MR-PRESSO (outlier detection, corrected estimate, distortion test)
- Leave-one-out analysis
- Single-SNP MR estimates and funnel plot

---

## Repository Structure

```text
.
├── insomnia_mdd_mr_final_project_KAPOOR.qmd
├── insomnia_mdd_mr_final_project_KAPOOR.html
├── README.md
├── results/
│   ├── mr_results_insomnia_to_MDD.tsv
│   ├── mr_results_insomnia_to_MDD_OR.tsv
│   ├── mr_heterogeneity_insomnia_to_MDD.tsv
│   ├── mr_pleiotropy_insomnia_to_MDD.tsv
│   ├── mr_leaveoneout_insomnia_to_MDD.tsv
│   ├── mr_singlesnp_insomnia_to_MDD.tsv
│   └── mr_presso_insomnia_to_MDD.rds
└── figures/
    ├── scatter_insomnia_to_MDD.png
    ├── forest_loo_insomnia_to_MDD.png
    └── funnel_insomnia_to_MDD.png
