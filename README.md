# Band Gap Prediction for Nitride-Based Solid-State Electrolytes Using Machine Learning

## Background
The development of high-performance solid-state electrolytes is critical for advancing next-generation battery technologies, particularly for applications in electric vehicles. Nitride-based materials, such as Li₃N and Mg₃N₂, represent an underexplored class of potential electrolytes due to their promising ionic conductivity and wide electronic band gaps, which are essential for ensuring electrochemical stability and safety [1]. This project leverages machine learning, specifically a Gradient Boosting Regressor (XGBoost), to predict the band gaps of nitride-based compounds sourced from the Materials Project database [2]. Focusing on pure nitride systems, this study aims to identify stable, high-performance electrolyte candidates, contributing to the design of safer and more efficient energy storage systems.

## Data and Features
Using the mp-api, the data selection criteria require the presence of nitrogen (```elements=["N"]```), exclude oxygen and sulfur (```exclude_elements=["S", "O"]```) to avoid oxynitrides and thionitrides, and limit compounds to 2–6 elements (```num_elements=(2, 6)```) with energy above hull ≤0.15 eV for stability. The selected features, adopted from paper Qin et a. (2024), include ```material_id```, ```formula_pretty```, ```band_gap```, ```volume```, ```cbm```, ```density```, ```density_atomic```, ```efermi```, ```energy_above_hull```, ```num_magnetic_sites```, and ```num_unique_magnetic_sites```, providing a comprehensive set of structural and electronic properties for accurate band gap prediction [3].

## Implementation
Data preprocessing reduced the initial dataset from 3,055 to 1,671 compounds through systematic removal of missing values and outlier elimination using IQR methodology. Eight input features were selected for model training as previously mentioned. Min-Max normalization addressed feature scale disparities.
XGBoost was implemented for its demonstrated effectiveness in materials property prediction and interpretability through feature importance analysis. The model was trained using standard hyperparameters with 80/20 train-test split.

## Results
The XGBoost model achieved the following performance metrics:

**Training Set:**
- R² = 0.954
- MAE = 0.247 eV
- MSE = 0.118 eV²

**Test Set:**
- R² = 0.865
- MAE = 0.435 eV
- MSE = 0.392 eV²

The test R² of 0.865 represents acceptable performance compared to literature benchmarks, though it falls short of state-of-the-art results [3] [4]. Wang et al. achieved R² = 0.920 using ensemble methods on larger datasets [4], highlighting the limitations of the current approach's dataset size and model selection.

The training-test performance gap reveals concerning generalization issues. The R² degradation of 0.089 indicates moderate overfitting, while the disproportionate increase in MSE (232%) compared to MAE (76%) suggests the presence of significant outliers in test predictions. This pattern indicates that while most predictions maintain reasonable accuracy, the model produces some substantially inaccurate predictions for certain nitride compositions, as MSE penalizes large errors more heavily than MAE.
Overall, performance degradation most likely stems from the relatively small dataset size (1,671 samples).
Larger gaps often reflect insufficient data diversity or feature engineering limitations rather than algorithmic deficiencies. The model may be memorizing specific nitride compositions rather than learning generalizable structure-property relationships.

## Feature Analysis
SHAP analysis identified feature importance hierarchy:
- Fermi energy (efermi): Dominant predictor (mean |SHAP| ≈ 0.8)
- Conduction band minimum (cbm): Secondary importance with negative correlation
- Density: Moderate positive correlation
- Volume, atomic density, energy above hull: Minor contributions
- Magnetic descriptors: Negligible influence

The dominance of electronic descriptors over structural features aligns with fundamental band gap physics. However, the strong reliance on Fermi energy differs from Qin et al.'s findings for silicon oxides, where CBM showed greater prominence [3]. This discrepancy may reflect material-specific electronic structure differences between nitrides and silicon oxides.

## Critical Assessment
Several limitations warrant consideration:
- Dataset size: The 1,671-sample dataset is relatively small compared to recent materials ML studies, potentially limiting generalizability.
- Feature selection: The eight-feature approach, while computationally efficient, may oversimplify the complex relationships governing band gaps in nitride systems.
- Validation scope: Testing is limited to the same chemical space as training data, without external validation on experimentally synthesized nitrides.
- Performance gap: The training-test R² difference (0.089) suggests some overfitting, despite XGBoost's built-in regularization.

## Bibliography
[1] Li, W., Li, M., Ren, H., Kim, J.T., Li, R., Sham, T.-K. and Sun, X. (2025). Nitride solid-state electrolytes for all-solid-state lithium metal batteries. Energy & Environmental Science. [online] doi:https://doi.org/10.1039/d4ee04927f.
‌

[2] Jain, A., Ong, S.P., Hautier, G., Chen, W., Richards, W.D., Dacek, S., Cholia, S., Gunter, D., Skinner, D., Ceder, G. and Persson, K.A. (2013). Commentary: The Materials Project: A materials genome approach to accelerating materials innovation. APL Materials, [online] 1(1), p.011002. doi:https://doi.org/10.1063/1.4812323.
‌

[3] Qin, H., Zhang, Y., Guo, Z., Wang, S., Zhao, D. and Xue, Y. (2024). Prediction of Bandgap in Lithium-Ion Battery Materials Based on Explainable Boosting Machine Learning Techniques. Materials, 17(24), pp.6217–6217. doi:https://doi.org/10.3390/ma17246217.
‌

[4] Wang, Y., Lv, J., Zhu, L. and Ma, Y. (2021). Accurate prediction of band gap of materials using stacking machine learning model. Computational Materials Science, 201, p.110899.

