#Bank Transaction Fraud Detection Analysis




## Project Overview

This project focuses on fraud detection and anomaly identification within banking transactions. The primary objective is to develop a model that minimizes financial loss by detecting suspicious patterns with high precision, ensuring a balance between fraud capture and a low false-positive rate.

The dataset contains 2,512 transactional records, providing deep insights into customer demographics, usage patterns, and financial activity, which are essential for building robust financial security applications.

## Machine Learning Workflow

### Phase 1: Clustering (Unsupervised Learning)

The goal of this phase was to group transactions based on behavioral similarities without prior labeling.

1. **Data Processing & Cleaning:** Handling missing values, duplicates, and initial data auditing.
2. **Preprocessing:** Feature scaling (Standardization) and encoding to prepare the data for distance-based algorithms.
3. **Cluster Optimization:** Used the **Elbow Method** to determine the optimal number of clusters ().
4. **Model Development:** Applied **K-Means Clustering** to segment the data.
5. **Evaluation & Inversion:** Used **Silhouette Scores** for validation, then performed **Feature Inversion** to translate the scaled data back into original values for business interpretation.

### Phase 2: Classification (Supervised Learning)

After identifying the clusters (Safe, Warning, High-Risk), I built a model to predict these categories for new data.

1. **Dataset Integration:** Used the labels generated from the clustering phase as the target variable.
2. **Data Splitting:** Divided the data into training and testing sets.
3. **Classification Model:** Developed a **Decision Tree** classifier to learn the rules that define each transaction risk level.
4. **Model Evaluation:** Measured performance using a Confusion Matrix and Accuracy/Precision metrics.

