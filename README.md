---

### Credit Card Fraud Detection

## Project Overview

This project applies anomaly detection techniques to identify fraudulent credit card transactions using the multivariate Gaussian model on the Credit Card Fraud Detection dataset (https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud). The goal is to detect rare fraud cases (0.17% of transactions) while evaluating performance with key metrics and visualizations.

## Data Preprocessing

- **Feature Transformation**:
  - Applied `log1p` transformation to the `Amount` column to reduce skewness.
  - Flattened features (`V1` to `V28` and `Amount`) into a vector, excluding `Time` and `Class`.
  - Normalized features using `StandardScaler`, fitted on non-fraud training data and applied to validation/test sets.
- **Target Handling**:
  - Target variable (`Class`) retained as binary labels (0 = non-fraud, 1 = fraud) for evaluation.

## Modeling

- **Anomaly Detection**:
  - Implemented a multivariate Gaussian model fitted on non-fraud training data, computing probability densities:
    ![Multivariate Gaussian Equation](https://latex.codecogs.com/png.latex?\dpi{150}\inline%20p(\mathbf{x})%20=%20\frac{1}{(2\pi)^{n/2}%20\sqrt{|\Sigma|}}%20\exp\left(-\frac{1}{2}%20(\mathbf{x}%20-%20\mu)^T%20\Sigma^{-1}%20(\mathbf{x}%20-%20\mu)\right))
  - Added regularization (1e-4) to the covariance matrix to prevent singularity.
  - Optimized threshold using F1-score (beta=1) on the validation set.
- **Evaluation**:
  - Assessed performance on a test set (57,109 samples) using confusion matrix, F1-score, precision, and recall.

## Results

The model’s performance on the test set is summarized below:

- **F1-Score (Fraud Class)**: 0.0236
- **Confusion Matrix**:
  - TN: 37,835 | FP: 19,028
  - FN: 9      | TP: 237
- **Precision (Fraud)**: 0.0123
- **Recall (Fraud)**: 0.9634
- **Observations**: High recall (96.34%) indicates near-perfect fraud detection, but low precision (1.23%) due to 19,028 false positives limits practical use.

## Conclusion

This project demonstrates anomaly detection for credit card fraud using a multivariate Gaussian model, achieving high recall (96.34%) on the Credit Card Fraud Detection dataset. However, the low F1-score (0.0236) and high false positive rate highlight challenges in balancing precision and recall. The model serves as a starting point for fraud detection, with potential for improvement through threshold tuning or alternative approaches. Visualizations (e.g., confusion matrix) provide insight into performance, making this a valuable baseline for future exploration.

---