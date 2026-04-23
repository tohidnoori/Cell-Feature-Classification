# Cell Feature Classification & Feature Engineering 🔬

This project focuses heavily on **preprocessing, feature engineering, and feature selection** to prepare complex tabular data for classification. Using the `segmentationData` dataset, we engineered new domain-specific features and rigorously filtered the dataset to predict the cell `Class`. We then evaluated the quality of our feature engineering by benchmarking three traditional Machine Learning models and one Neural Network.

### Primary Focus: Preprocessing & Feature Engineering
The core of this notebook is dedicated to transforming raw extracted features into a highly predictive, low-noise dataset. Key steps include:

**1. Data Cleaning & Encoding**
*   **Column Formatting:** Stripped "Ch" from column names for cleaner data handling.
*   **Data Leakage Prevention:** Dropped identifier columns (`Case` and `Cell`).
*   **Target Encoding:** Converted the `Class` target to binary ($1$ if "PS", $0$ otherwise).
*   **Outlier Detection:** Analyzed distributions using Interquartile Range (IQR) and Z-score ($> 3$ standard deviations) methods.

**2. Feature Engineering**
We created several composite features to better capture the underlying biology and morphology:
*   **Relative Biomarker Expression:** `Ratio_Marker3_to_Marker4` ($AvgInten3 / AvgInten4$)
*   **Biomarker Concentration:** `Biomarker3_Density` ($TotalInten3 / Area1$)
*   **Biomarker Heterogeneity:** `Biomarker3_Heterogeneity` ($IntenCoocEntropy3 \times VarInten3$)
*   **Fiber/Spot Concentration:** `Fiber_Density_Ch3` ($SpotFiberCount3 / Area1$)
*   **Spatial Context:** `Distance_From_Center` (Calculated using $X/Y$ centroids relative to the overall tissue/image center).

**3. Feature Selection & Dimensionality Reduction**
To prevent the curse of dimensionality and reduce noise, we applied rigorous filter methods:
*   **Target Correlation Filtering:** Removed features with low correlation to the target variable ($|corr| < 0.1$).
*   **Multicollinearity Removal:** Identified and dropped highly inter-correlated features (correlation $> 0.85$) to reduce redundancy.

### Dataset
*   **Source:** `segmentationData`
*   **Target:** `Class` (Binary: PS vs. Non-PS)
*   **Features:** Raw morphological/intensity features + 5 custom engineered features (reduced via correlation filtering).

### Models & Results
We trained four different models to test the effectiveness of our engineered features. Below are the results on the test set:

#### 1. Random Forest (Best Performing Model ⭐)
*   **Accuracy:** $0.9307$
*   **Precision:** $0.9394$
*   **Sensitivity:** $0.9538$
*   *Note: Tree-based models handled the engineered tabular features exceptionally well, resulting in the highest overall performance and lowest false negative rate.*

#### 2. Support Vector Machine (SVM)
*   **Accuracy:** $0.8589$
*   **Precision:** $0.8830$
*   **Sensitivity:** $0.9000$

#### 3. K-Nearest Neighbors (KNN, $k=40$)
*   **Accuracy:** $0.8292$
*   **Precision:** $0.8775$
*   **Sensitivity:** $0.8538$

#### 4. Neural Network
*   **Accuracy:** $0.7946$
*   **Precision:** $0.8865$
*   **Sensitivity:** $0.7808$
*   *Note: The Neural Network had the lowest sensitivity ($0.7808$), indicating it struggled more with false negatives compared to the machine learning baselines on this specific tabular setup.*

### Visualizations
*   **Correlation Heatmaps:** Visualized feature-to-target correlations before and after removing low-impact features.
*   **Collinearity Heatmaps:** Visualized inter-feature relationships to demonstrate the reduction of multicollinearity.
*   **Confusion Matrices:** Plotted for all four models (SVM, Random Forest, KNN, Neural Net) to visualize True Positives, True Negatives, False Positives, and False Negatives.# Cell Feature Classification & Feature Engineering 🔬

This project focuses heavily on **preprocessing and feature engineering** to prepare complex tabular data for classification. Using the `segmentationData` dataset, we process 58 extracted morphological, intensity, and texture features to predict the cell `Class`. We then evaluate the quality of our feature engineering by benchmarking three traditional Machine Learning models and one Neural Network.

### Primary Focus: Preprocessing & Feature Engineering
The core of this notebook is dedicated to transforming raw extracted features into a highly predictive dataset. Key steps include:
*   **Data Cleaning:** Dropping identifier columns (`Cell` and `Case`) to prevent data leakage.
*   **Missing Value Handling:** Identifying and imputing missing data.
*   **Feature Scaling:** Standardizing all 58 numerical features (e.g., `Area1`, `AvgInten1`) using `StandardScaler` to ensure uniform distribution (mean of $0$, variance of $1$), which is critical for distance-based models like KNN and Neural Networks.
*   **Target Encoding:** Preparing the `Class` variable for binary/multiclass classification.

### Dataset
*   **Source:** `segmentationData`
*   **Target:** `Class`
*   **Features:** 58 numerical features representing cell morphology, intensity, and texture/fibers.
*   **Split:** Standard Train/Test split for model evaluation.

### Models & Results

We trained four different models to test the effectiveness of our engineered features. Below are the results on the test set:

#### 1. Random Forest (Best Performing Model ⭐)
*   **Accuracy:** $0.9307$
*   **Precision:** $0.9394$
*   **Sensitivity:** $0.9538$
*   *Note: Tree-based models handled the engineered tabular features exceptionally well, resulting in the highest overall performance and lowest false negative rate.*

#### 2. Support Vector Machine (SVM)
*   **Accuracy:** $0.8589$
*   **Precision:** $0.8830$
*   **Sensitivity:** $0.9000$

#### 3. K-Nearest Neighbors (KNN, $k=40$)
*   **Accuracy:** $0.8292$
*   **Precision:** $0.8775$
*   **Sensitivity:** $0.8538$

#### 4. Neural Network
*   **Accuracy:** $0.7946$
*   **Precision:** $0.8865$
*   **Sensitivity:** $0.7808$
*   *Note: The Neural Network had the lowest sensitivity ($0.7808$), indicating it struggled more with false negatives compared to the machine learning baselines on this specific tabular setup.*

### Visualizations
*   **Confusion Matrices:** Plotted for all four models (SVM, Random Forest, KNN, Neural Net) to visualize True Positives, True Negatives, False Positives, and False Negatives, allowing for a direct comparison of where each model excels or fails.
