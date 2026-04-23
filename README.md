# Cell Feature Classification & Feature Engineering 🔬

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
