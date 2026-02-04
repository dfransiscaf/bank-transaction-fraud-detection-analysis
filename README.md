# Bank Transaction Fraud Detection Analysis



## Project Background

This project focuses on fraud detection and anomaly identification within banking transactions. The primary objective is to develop a model that minimizes financial loss by detecting suspicious patterns with high precision, ensuring a balance between fraud capture and a low false-positive rate.

The dataset contains 2,512 transactional records, providing deep insights into customer demographics, usage patterns, and financial activity, which are essential for building robust financial security applications.

The project focuses on the following technical areas:
* Behavioral Segmentation: Identified correlations between features to group customers based on their transaction habits.
* Anomaly & Fraud Identification: Detecting outliers and suspicious activity patterns that deviate from normal banking behavior.
* Dimensionality Reduction: Implementing PCA to simplify complex datasets and provide clear visual representation of the clusters.
* Predictive Risk Modeling: Developing a classification system that can automatically assign a risk level to new incoming transactions.

## Data Structure & Initial Checks

The dataset consists of two primary tables that provide a holistic view of a bank business, including:
* AccountID: Unique identifier for each account, with multiple transactions per account.
* TransactionAmount: Monetary value of each transaction, ranging from small everyday expenses to larger purchases.
* TransactionDate: Timestamp of each transaction, capturing date and time.
* TransactionType: Categorical field indicating 'Credit' or 'Debit' transactions.
* Location: Geographic location of the transaction, represented by U.S. city names.
* DeviceID: Alphanumeric identifier for devices used to perform the transaction.
* IP Address: IPv4 address associated with the transaction, with occasional changes for some accounts.
* MerchantID: Unique identifier for merchants, showing preferred and outlier merchants for each account.
* AccountBalance: Balance in the account post-transaction, with logical correlations based on transaction type and amount.
* PreviousTransactionDate: Timestamp of the last transaction for the account, aiding in calculating transaction frequency.
* Channel: Channel through which the transaction was performed (e.g., Online, ATM, Branch).
* CustomerAge: Age of the account holder, with logical groupings based on occupation.
* CustomerOccupation: Occupation of the account holder (e.g., Doctor, Engineer, Student, Retired), reflecting income patterns.
* TransactionDuration: Duration of the transaction in seconds, varying by transaction type.
* LoginAttempts: Number of login attempts before the transaction, with higher values indicating potential anomalies.

Conducted a thorough audit of the raw dataset and performed the following cleaning steps to ensure data integrity:

* Handling Missing Values: Removed records with missing values to maintain a high-quality and consistent dataset for analysis.
* Removing Duplicates: Identified and eliminated redundant entries to ensure each transaction is uniquely and accurately represented.
* Data Standardization: Uniformed categorical values by converting text to lowercase and mapping internal codes into clear, user-friendly descriptions.
* Data Distribution Tuning: Addressed extreme variances and improved model stability by grouping continuous numerical data into strategic categories (Binning)

## Machine Learning Workflow

### Clustering (Unsupervised Learning)

The goal of this phase was to group transactions based on behavioral similarities without prior labeling.
* Data Processing & Cleaning: Performed initial data auditing, including handling missing values and duplicates.
* Preprocessing: Applied feature scaling (Standardization) and encoding to prepare the data for distance-based algorithms.
* Cluster Optimization: Utilized the Elbow Method to determine the optimal number of clusters ().
* Model Development: Applied K-Means Clustering to segment transactions into distinct behavioral groups.
* Evaluation & Inversion: Validated clusters using Silhouette Scores, followed by Feature Inversion to translate scaled data back into original values for meaningful business interpretation.

### Classification (Supervised Learning)

After identifying the clusters and built a model to predict categories for new data.
* Dataset Integration: Used the labels generated from the clustering phase as the target variable for training.
* Data Splitting: Divided the dataset into training and testing sets to ensure model generalization.
* Classification Model: Developed a Decision Tree classifier to identify the underlying rules that define each risk level.
* Model Evaluation: Measured performance using a Classification Report and Confusion Matrix to ensure high detection accuracy.

## Executive Summary

### Overview of Findings

The hybrid analysis segmented banking transactions into distinct risk profiles and built a highly reliable classification system. Through K-Means analysis, the data was categorized into groups with clear behavioral differences. PCA visualization confirmed that fraudulent signatures are distinct from normal activities, allowing for effective separation even in high-dimensional datasets. The tuned Decision Tree model achieved 1.00 Precision for High-Risk transactions (Class 1). This means the system has a 0% False Positive rate, ensuring that no legitimate customers are wrongly flagged as fraud. With a 1.00 Recall for Safe transactions (Class 0), the model guarantees that all standard banking activities proceed without interruption, maintaining a seamless user experience.

#### 
### Cluster Identification (Elbow Method)

<p align="center">
 <img width="696" height="507" alt="silhouette k means" src="https://github.com/user-attachments/assets/e55547c9-3106-40b0-a972-d7a80828ac78" />

</p>

####

* Used the Elbow Method to determine the ideal number of clusters by observing the Within-Cluster Sum of Squares (WCSS).
* The "elbow" point—where the rate of decrease significantly levels off was found at $K = 2$ with a Silhouette Score of 0.572. This indicates that the transaction data is most naturally segmented into two distinct behavioral groups.

####
### 2D Cluster Visualization (PCA) 

<p align="center">
 <img width="841" height="704" alt="visualization pca cluster" src="https://github.com/user-attachments/assets/bf1bafd0-5988-4ca1-912e-b71b4c832518" />

</p>

####

* Since the dataset contains multiple features, PCA was applied to reduce dimensions while retaining maximum variance.
* This allows for cluster visualization in 2D space, showing how the model separates different transaction behaviors. The PCA plot displays a clear separation between groups, justifying the effectiveness of the clustering approach.

####
### Tuned Model Performance 

              precision    recall  f1-score   support

           0       0.65      1.00      0.79       196
           1       1.00      0.46      0.63       193

    accuracy                           0.73       389
   macro avg       0.83      0.73      0.71       389
weighted avg       0.82      0.73      0.71       389

####

* High-Risk Precision (1.00): The model achieved a 100% Precision rate for High-Risk transactions, meaning it never wrongly flagged a legitimate transaction as fraud (Zero False Positives).
* Safe Transaction Recall (1.00): This ensures all legitimate banking activities are correctly identified and processed without friction.
* Fraud Recall (0.46): The lower recall for Class 1 indicates a conservative approach. The model is tuned to prioritize certainty; it only flags a transaction as fraud when the pattern is undeniable, minimizing unnecessary customer intervention.

####
### Cluster Interpretation (Post-Inversion Analysis)

Cluster 0: High-Value Traditionalists (Mature & Goal-Oriented)
* This cluster is dominated by middle-aged customers with an average age of 45 years. They exhibit high financial stability, characterized by substantial account balances and established professional backgrounds (e.g., Medical Doctors).
* Customers in this segment tend to have a longer transaction duration compared to the general population, suggesting a cautious and highly considered decision-making process.
* They show a strong preference for Debit transactions performed through Physical Branch Channels. This indicates a reliance on direct interaction and a traditional approach to banking security and services.

Cluster 1: Tech-Savvy Spenders (Young & Dynamic)
* With an average age of 44 years, this group is categorized under the "Young Adult" professional bracket. Interestingly, a significant portion is listed as Students, which may indicate outdated system records or a segment of postgraduate professionals (Masters/PhD candidates).
* This segment is highly dynamic, characterized by a high frequency of transactions. Conversely, they have very short login durations, suggesting they are tech-savvy and highly efficient in navigating digital banking platforms.
* While they maintain relatively high balances, their high transaction volume suggests a more impulsive spending pattern. Their behavior is primarily focused on short-term lifestyle needs rather than long-term financial accumulation.

#####


## Recommendations:

Based on the insights and findings above, we would recommend that the stakeholder team consider the following: 
* Cluster 0 (High-Value Traditionalists): Given their financial stability and long-term orientation, the stakeholder team should focus on wealth preservation and premium services. Recommended products include Long-term Savings Plans, Retirement Insurance (Pension Funds), Time Deposits (CDs), and invitations to Priority/Private Banking services.
* Cluster 1 (Tech-Savvy Spenders): Due to their dynamic transaction patterns and impulsive spending habits, this segment is ideal for credit-based and digital-first products. Recommended offerings include Installment Plans, Buy Now Pay Later (BNPL) services, and low-risk credit products tailored to lifestyle needs, delivered through digital channels.


## Assumptions and Caveats:

Throughout the analysis, several assumptions were made to address data challenges and ensure accuracy. These assumptions and caveats are noted below:
* In Cluster 1, the data shows an average age of 44 with a 'Student' status. This is interpreted as Profile Lag, where long-term customers likely have not updated their occupational profiles in the bank's database since their initial account opening.
* This discrepancy does not affect the model's clustering logic (as it is based on multi-dimensional mathematical distances). However, it suggests that future model iterations would benefit from data enrichment or a profile validation campaign to ensure occupational data reflects the current status of the customers.

