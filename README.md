# Band Gap Prediction for Nitride-Based Solid-State Electrolytes Using Machine Learning

### Background
The development of high-performance solid-state electrolytes is critical for advancing next-generation battery technologies, particularly for applications in electric vehicles. Nitride-based materials, such as Li₃N and Mg₃N₂, represent an underexplored class of potential electrolytes due to their promising ionic conductivity and wide electronic band gaps, which are essential for ensuring electrochemical stability and safety [1]. This project leverages machine learning, specifically a Gradient Boosting Regressor (XGBoost), to predict the band gaps of nitride-based compounds sourced from the Materials Project database [2]. Focusing on pure nitride systems, this study aims to identify stable, high-performance electrolyte candidates, contributing to the design of safer and more efficient energy storage systems.

### Data and Features
Using the mp-api, the data selection criteria require the presence of nitrogen (```elements=["N"]```), exclude oxygen and sulfur (```exclude_elements=["S", "O"]```) to avoid oxynitrides and thionitrides, and limit compounds to 2–6 elements (```num_elements=(2, 6)```) with energy above hull ≤0.15 eV for stability. The selected features, adopted from paper Qin et a. (2024), include ```material_id```, ```formula_pretty```, ```band_gap```, ```volume```, ```cbm```, ```density```, ```density_atomic```, ```efermi```, ```energy_above_hull```, ```num_magnetic_sites```, and ```num_unique_magnetic_sites```, providing a comprehensive set of structural and electronic properties for accurate band gap prediction [3].

### Implementation

### Bibliography
[1] Li, W., Li, M., Ren, H., Kim, J.T., Li, R., Sham, T.-K. and Sun, X. (2025). Nitride solid-state electrolytes for all-solid-state lithium metal batteries. Energy & Environmental Science. [online] doi:https://doi.org/10.1039/d4ee04927f.
‌

[2] Jain, A., Ong, S.P., Hautier, G., Chen, W., Richards, W.D., Dacek, S., Cholia, S., Gunter, D., Skinner, D., Ceder, G. and Persson, K.A. (2013). Commentary: The Materials Project: A materials genome approach to accelerating materials innovation. APL Materials, [online] 1(1), p.011002. doi:https://doi.org/10.1063/1.4812323.
‌

[3] Qin, H., Zhang, Y., Guo, Z., Wang, S., Zhao, D. and Xue, Y. (2024). Prediction of Bandgap in Lithium-Ion Battery Materials Based on Explainable Boosting Machine Learning Techniques. Materials, 17(24), pp.6217–6217. doi:https://doi.org/10.3390/ma17246217.
‌
