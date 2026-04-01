[README.md](https://github.com/user-attachments/files/26419734/README.md)
# Physics-Informed Stacking Ensemble for Simultaneous Prediction of Surface Roughness and Sound Pressure Level in VBD Marble Milling

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19368120.svg)](https://doi.org/10.5281/zenodo.19368120)

**Authors:** Erkan Özkan, Oğuzhan Öz, Gencay Sarıışık  
**Affiliation:** Armoren Research Lab, Afyon Kocatepe University  
**Journal:** Expert Systems with Applications (ESWA)  
**GitHub:** [https://github.com/erkanozka/pap1_marble_VBD_milling_ML](https://github.com/erkanozka/pap1_marble_VBD_milling_ML)

---

## Overview

This repository contains the experimental datasets, Google Colab notebooks, and all reproducible output files for the manuscript:

> *"Physics-Informed Machine Learning for Simultaneous Prediction of Surface Roughness (Ra) and Sound Pressure Level (Lp) in VBD Marble Milling"*

Two marble varieties are studied:
- **Afyon White (AW)** — primary training and validation material
- **Afyon Grey (AG)** — cross-material generalization validation

---

## Repository Structure

```
├── README.md
├── data/
│   ├── pap_AW_VBD_milling_2640obs.xlsx          # AW raw dataset (2,640 obs)
│   └── pap_AG_VBD_milling_2640obs.xlsx          # AG raw dataset (2,640 obs)
├── notebooks/
│   ├── pap_AW_VBD_milling_ML.ipynb              # AW full pipeline notebook
│   └── pap_AG_VBD_milling_ML.ipynb              # AG full pipeline notebook
├── pap1_AW_VBD_milling_ML_output/
│   ├── FD1_Predicted_vs_Actual.csv              # Figure 5 data
│   ├── FD2_Residuals.csv                        # Figure 6 data
│   ├── FD3_SHAP_Summary.csv                     # SHAP beeswarm values
│   ├── FD4_FeatureImportance.csv                # Figure 3b data
│   ├── FD5_PDP.csv                              # Figure 7 data
│   ├── FD6_LearningCurve.csv                    # Figure 4c data
│   ├── FD7_SHAP_Interaction.csv                 # SHAP interaction values
│   ├── Table1_Descriptive.csv
│   ├── Table2_PhysicsFeatures.csv
│   ├── Table3_VIF.csv
│   ├── Table3b_Correlation.csv
│   ├── Table4a_BorutaPerc.csv
│   ├── Table4_FeatureSelection.csv
│   ├── Table5_CV_Ra.csv
│   ├── Table5_CV_Lp.csv
│   ├── Table6_BaseModel_Ra.csv
│   ├── Table6_BaseModel_Lp.csv
│   ├── Table7_BO_Ra.csv
│   ├── Table7_BO_Lp.csv
│   ├── Table8_Bootstrap_CI.csv
│   ├── Table9_Wilcoxon.csv
│   ├── Table10_Permutation.csv
│   ├── Table11_MetaLearner.csv
│   └── Table12_EarlyStopping.csv
└── pap1_AG_VBD_milling_ML_output/
    ├── FD1_Predicted_vs_Actual.csv
    ├── FD2_Residuals.csv
    ├── FD3_SHAP_Summary.csv
    ├── FD4_FeatureImportance.csv
    ├── FD5_PDP.csv
    ├── FD6_LearningCurve.csv
    ├── FD7_SHAP_Interaction.csv
    ├── Table1_Descriptive.csv
    ├── Table2_PhysicsFeatures.csv
    ├── Table3_VIF.csv
    ├── Table3b_Correlation.csv
    ├── Table4a_BorutaPerc.csv
    ├── Table4_FeatureSelection.csv
    ├── Table5_CV_Ra.csv
    ├── Table5_CV_Lp.csv
    ├── Table6_BaseModel_Ra.csv
    ├── Table6_BaseModel_Lp.csv
    ├── Table7_BO_Ra.csv
    ├── Table7_BO_Lp.csv
    ├── Table8_Bootstrap_CI.csv
    ├── Table9_Wilcoxon.csv
    ├── Table10_Permutation.csv
    ├── Table11_MetaLearner.csv
    └── Table12_EarlyStopping.csv
```

---

## Dataset Description

Each dataset contains **2,640 observations** from a full-factorial CNC milling experiment:
- **4 spindle speeds** (n): 6,000 / 8,000 / 10,000 / 12,000 min⁻¹
- **4 feed rates** (f): 1,000 / 3,000 / 5,000 / 7,000 mm/min
- **16 blocks** × 165 observations per block
- **Tooling:** Vacuum Brazed Diamond (VBD) disc

### Variables (13 columns per dataset)

| Column | Description | Unit |
|--------|-------------|------|
| Block | Experimental block ID (n × f combination) | — |
| n | Spindle speed | min⁻¹ |
| f | Feed rate | mm/min |
| Fz | Axial force | N |
| Fx | Force in X direction | N |
| Fy | Force in Y direction | N |
| P | Electrical power consumption | W |
| SE | Specific energy | J/cm³ |
| Fr | Resultant force | N |
| Ft | Tangential force | N |
| Ra | Surface roughness (target) | μm |
| Lp | Sound pressure level (target) | dB |

Seven physics-derived features (Fe1–Fe7) are computed within the notebook from the measured process signals.

---

## Key Results

| Marble | Target | R² | RMSE | MAPE (%) |
|--------|--------|----|------|----------|
| **AW** | **Ra** | **0.9700** | **0.1556 μm** | **1.85** |
| **AW** | **Lp** | **0.9691** | **0.4510 dB** | **0.41** |
| AG | Ra | 0.7599 | 0.3291 μm | 4.13 |
| AG | Lp | 0.8953 | 0.5976 dB | 0.57 |

Boruta-SHAP selected **distinct feature sets** for each marble, confirming that each stone variety carries its own machining signature.

---

## Reproduction

1. Open the notebook (AW or AG) in [Google Colab](https://colab.research.google.com/)
2. Mount Google Drive and adjust `BASE_DIR` path
3. Run all cells — the notebook produces all Table and FD CSV files automatically
4. Seed is fixed (`SEED = 42`) for full reproducibility

---

## Output File Descriptions

### Figure Data (FD) Files

| File | Content | Manuscript Reference |
|------|---------|---------------------|
| FD1_Predicted_vs_Actual.csv | Test-set actual vs predicted values | Figure 5 |
| FD2_Residuals.csv | Residual values for diagnostics | Figure 6 |
| FD3_SHAP_Summary.csv | Per-observation SHAP values | Figure 3b source |
| FD4_FeatureImportance.csv | Mean \|SHAP\| importance per feature | Figure 3b |
| FD5_PDP.csv | Partial dependence profile grid values | Figure 7 |
| FD6_LearningCurve.csv | Learning curve R² across training fractions | Figure 4c |
| FD7_SHAP_Interaction.csv | SHAP interaction values (pairwise) | §4.5 |

### Table Files

| File | Content | Manuscript Reference |
|------|---------|---------------------|
| Table1_Descriptive.csv | Descriptive statistics | Table 1 |
| Table2_PhysicsFeatures.csv | Fe1–Fe7 definitions and VIF | Table 2 |
| Table3_VIF.csv | Variance inflation factors | Table 3 |
| Table4_FeatureSelection.csv | Boruta-SHAP selected features | Table 3 |
| Table5_CV_{Ra,Lp}.csv | CV strategy comparison | Table 4 |
| Table6_BaseModel_{Ra,Lp}.csv | Base model test performance | Table 4 |
| Table7_BO_{Ra,Lp}.csv | Bayesian-optimized hyperparameters | Table 5 |
| Table8_Bootstrap_CI.csv | Bootstrap 95% confidence intervals | Table 6a |
| Table9_Wilcoxon.csv | Wilcoxon signed-rank test results | Table 8 |
| Table10_Permutation.csv | Permutation test (N = 200) results | §4.4 |
| Table11_MetaLearner.csv | Meta-learner grid search | Table 6b |
| Table12_EarlyStopping.csv | Early stopping convergence | §4.3 |

---

## License

This repository is released under the [MIT License](LICENSE).

## Citation

If you use this dataset, please cite:

```
Özkan, E., Öz, O., & Sarıışık, G. (2025). Physics-informed machine learning for 
simultaneous prediction of surface roughness and sound pressure level in VBD marble 
milling [Dataset]. Zenodo. https://doi.org/10.5281/zenodo.19368120
```

## Acknowledgements

This research was supported by Afyon Kocatepe University Scientific Research Projects Coordination Unit (BAP) under project number 23.FEN.BİL.06.
