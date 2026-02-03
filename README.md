# Bank Transaction Fraud Detection Analysis



## Project Background

This project focuses on fraud detection and anomaly identification within banking transactions. The primary objective is to develop a model that minimizes financial loss by detecting suspicious patterns with high precision, ensuring a balance between fraud capture and a low false-positive rate.

The dataset contains 2,512 transactional records, providing deep insights into customer demographics, usage patterns, and financial activity, which are essential for building robust financial security applications.

The project focuses on the following technical areas:
* Behavioral Segmentation: Using unsupervised learning to group customers based on transaction frequency, amount, and demographics.
* Anomaly & Fraud Identification: Detecting outliers and suspicious activity patterns that deviate from normal banking behavior.
* Dimensionality Reduction: Implementing PCA to simplify complex datasets while retaining critical information for better cluster visualization.
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

## Machine Learning Workflow

### Clustering (Unsupervised Learning)

The goal of this phase was to group transactions based on behavioral similarities without prior labeling.

1. **Data Processing & Cleaning:** Handling missing values, duplicates, and initial data auditing.
2. **Preprocessing:** Feature scaling (Standardization) and encoding to prepare the data for distance-based algorithms.
3. **Cluster Optimization:** Used the **Elbow Method** to determine the optimal number of clusters.
4. **Model Development:** Applied **K-Means Clustering** to segment the data.
5. **Evaluation & Inversion:** Used **Silhouette Scores** for validation, then performed **Feature Inversion** to translate the scaled data back into original values for business interpretation.

### Classification (Supervised Learning)

After identifying the clusters and built a model to predict categories for new data.

1. **Dataset Integration:** Used the labels generated from the clustering phase as the target variable.
2. **Data Splitting:** Divided the data into training and testing sets.
3. **Classification Model:** Developed a **Decision Tree** classifier to learn the rules that define each transaction risk level.
4. **Model Evaluation:** Measured performance using a Confusion Matrix and Accuracy/Precision metrics.

## Executive Summary

### Overview of Findings

The hybrid analysis segmented banking transactions into distinct risk profiles and built a highly reliable classification system. Through K-Means analysis, the data was categorized into groups with clear behavioral differences. PCA visualization confirmed that fraudulent signatures are distinct from normal activities, allowing for effective separation even in high-dimensional datasets. The tuned Decision Tree model achieved 1.00 Precision for High-Risk transactions (Class 1). This means the system has a 0% False Positive rate, ensuring that no legitimate customers are wrongly flagged as fraud. With a 1.00 Recall for Safe transactions (Class 0), the model guarantees that all standard banking activities proceed without interruption, maintaining a seamless user experience.

<p align="center">
 <img width="696" height="507" alt="silhouette k means" src="https://github.com/user-attachments/assets/e55547c9-3106-40b0-a972-d7a80828ac78" />

</p>

####

* Optimal Cluster Identification (Elbow Method)I used the Elbow Method to determine the ideal number of clusters by observing the Within-Cluster Sum of Squares (WCSS).
* Insight: The "elbow" or the point where the rate of decrease significantly levels off was found at $K = 2$, score = 0,572.
* Decision: This indicates that the transaction data is most naturally segmented into [X] distinct groups.

####

<p align="center">
 <img width="841" height="704" alt="visualization pca cluster" src="https://github.com/user-attachments/assets/bf1bafd0-5988-4ca1-912e-b71b4c832518" />

</p>

####

* Dimensionality Reduction with PCA Since the dataset contains multiple features, I applied PCA to reduce the dimensions while retaining maximum variance.
* Visualization: This allows us to visualize the clusters in a 2D/3D space, showing how the model separates different transaction behaviors.
* Insight: In the PCA plot, we can see clear separation between the groups, which justifies the effectiveness of our clustering approach.

####

Tuned Model Performance
              precision    recall  f1-score   support

           0       0.65      1.00      0.79       196
           1       1.00      0.46      0.63       193

    accuracy                           0.73       389
   macro avg       0.83      0.73      0.71       389
weighted avg       0.82      0.73      0.71       389

####

* Zero False Positives: The model achieved a 100% Precision rate for High-Risk transactions, meaning it never wrongly flagged a legitimate transaction as fraud.
* Safe Haven: The 1.00 Recall for Safe transactions ensures that all legitimate banking activities are correctly identified and processed without friction.
* Trade-off: The lower recall for Class 1 (0.46) indicates a conservative approach, where the model only flags fraud when it is absolutely certain.

### Cluster Interpretation (Post-Inversion Analysis)

#### Cluster 0: (Nasabah usia lanjut dan berorientasi pada tujuan jangka panjang):
* Cluster ini didominasi oleh nasabah usia dewasa atau kategori Middle Age dengan rata-rata usia 45 tahun. Kondisi finansial mereka sangat stabil dengan saldo rekening yang tinggi serta sudah memiliki pekerjaan tetap, seperti dokter.
* Nasabah dalam cluster ini, cenderung memiliki durasi transaksi yang relatif lebih lama dibandingkan rata-rata populasi. Perilaku transaksinya menunjukkan bahwa mereka penuh pertimbangan dan sangat berhati-hati. Hal ini juga ditunjukkan pada kecenderungan mereka menggunakan tipe transaksi debit melalui channel Branch (Kantor Cabang) yang mana memerlukan interaksi langsung.

#### Cluster 1: (Nasabah usia muda dan perilaku transaksi yang dinamis):
* Cluster ini didominasi oleh nasabah yang memiliki rata-rata usia 44 tahun dengan kategori Young Adult. Namun, berdasarkan pekerjaannya data menunjukkan bahwa rata-rata nasabah adalah seorang pelajar. Hal ini mengindikasian kemungkinan adanya data yang belum diperbaharui oleh sistem atau segmen ini mewakili kelompok profesional yang tengah menempuh pendidikan pascasarjana (S2/S3).
* Perilaku transaksi kelompok nasabah dalam cluster ini sangat dinamis. Hal ini ditunjukkan dari tingginya transaksi yang pernah dilakukan. Di sisi lain, tingkat login durasi transaksi mereka cukup singkat atau dengan kata lain kelompok nasabah dalam cluster ini, sudah cukup terbiasa melakukan transaksi. Hal ini juga menunjukkan perilaku kategori umur di Young Adult yang sudah tech savvy.
* Saldo rekening menunjukkan cukup tinggi, namun hal ini juga sejalan dengan tingginya jumlah transaksi mereka yang mana hal ini mengindikasikan bahwa perilaku kelompok nasabah ini cukup impulsif dan lebih fokus pada pemenuhan kebutuhan gaya hidup jangka pendek.

#####


## Recommendations:

Based on the insights and findings above, we would recommend that the stakeholder team consider the following: 
* Berdasarkan analisis maka rekomendasi yang dapat diberikan pada kelompok nasabah cluster nol ini adalah tabungan jangka panjang, asuransi hari tua, deposito berjangka, hingga layanan nasabah prioritas.
* Berdasarkan analisis maka rekomendasi yang dapat diberikan pada kelompok nasabah di cluster satu ini adalah produk cicilan dan kredit (paylater) atau produk-produk perbankan lainnya dengan resiko rendah.


## Assumptions and Caveats:

Throughout the analysis, several assumptions were made to address data challenges and ensure accuracy. These assumptions and caveats are noted below:
* Missing values in Item Weight were handled using mean and mode imputation respectively, assuming these values represent the general distribution of the data.
* As this is a synthetic dataset for a case study, the analysis assumes that the recorded transactions are representative of actual retail patterns during the established timeframe.


