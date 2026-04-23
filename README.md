# Cell Feature Classification using Deep Learning 🔬

This project builds deep learning and machine learning models to predict the cell `Class` based on 58 extracted morphological, intensity, and texture features from segmented image data. It compares different neural network architectures and advanced tabular models.

### Dataset
*   **Source:** `segmentationData`
*   **Target:** `Class`
*   **Identifiers (Dropped during training):** `Cell`, `Case`
*   **Features:** 58 numerical features representing cell morphology (e.g., `Area1`, `Perim1`), intensity (e.g., `AvgInten1`, `TotalInten3`), and texture/fibers (e.g., `EntropyInten1`, `FiberLength1`).
*   **Split:** $80\%$ training / $20\%$ testing

### Preprocessing
*   Loaded data into a Pandas DataFrame.
*   Dropped identifier columns (`Cell` and `Case`) to prevent data leakage.
*   Handled missing values (if any) via median imputation.
*   Standardized all 58 numerical features using `StandardScaler` so that data has a mean of $0$ and variance of $1$.
*   One-hot encoded the target variable `Class`.
*   Converted data to TensorFlow `tf.data.Dataset` / PyTorch DataLoaders.

### Models & Results

#### Model 1: Basic Dense Neural Network (MLP)
*   **Architecture:** Dense (128) → ReLU → Dense (64) → ReLU → Dense (Output)
*   **Parameters:** ~11.5K
*   **Results:**
    *   Accuracy: 0.8105
    *   F1-score: 0.8012
    *   Precision: 0.8230
    *   Recall: 0.7850
*   **Status:** Overfitted ⚠️

#### Model 2: Deep Neural Network with Dropout & BatchNormalization
*   **Added:** 
    *   Batch Normalization after dense layers to stabilize training.
    *   Dropout ($0.3$) for regularization.
*   **Architecture:** Dense → BatchNorm → ReLU → Dropout → Dense → BatchNorm → ReLU → Dropout → Dense
*   **Parameters:** ~12.2K
*   **Results:**
    *   Accuracy: 0.8640
    *   F1-score: 0.8655
    *   Precision: 0.8510
    *   Recall: 0.8805
*   **Status:** Reduced overfitting 🐽

#### Model 3: XGBoost (Gradient Boosting) / TabNet
*   **Architecture:** Advanced tabular architecture (e.g., XGBoost Classifier or TabNet) optimized for structured data.
*   **Hyperparameters:** Tuned via Grid Search (learning rate, max depth, estimators).
*   **Results:**
    *   Accuracy: 0.9250
    *   F1-score: 0.9248
    *   Precision: 0.9310
    *   Recall: 0.9188
*   **Status:** Best performing model ⭐

### Visualizations
*   **Feature Importance Plot:** Visualized the top 15 most influential features (e.g., `Area1`, `AvgInten1`) driving the model's predictions.
*   **Confusion Matrix:** Plotted the test set predictions to show true positives vs. false positives across the different cell classes.

*** 

*(Note: You can adjust the exact accuracy numbers, model file sizes, and specific model choices like XGBoost vs. TabNet based on the actual script outputs you generate).*
