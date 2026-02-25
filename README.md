# spark-rfm-customer-segmentation
End-to-end customer segmentation using Apache Spark on a 500K+ transaction dataset. RFM feature engineering, clustering (BisectingKMeans), and predictive modeling for high-value customer identification.
Project Overview

This project presents an end-to-end customer segmentation and predictive modeling pipeline built with Apache Spark on a large-scale e-commerce transaction dataset (500,000+ rows).

The objective is to transform raw transactional data into actionable customer insights using RFM methodology, clustering techniques, and supervised learning models.

The workflow covers data preparation, feature engineering, unsupervised segmentation, supervised prediction, and translation into business strategy.

Business Questions

How can customer behavior be summarized quantitatively?

Can customers be segmented automatically using unsupervised learning?

Can we predict high-value customers using limited behavioral signals?

How can analytical results be translated into marketing actions?

Dataset

Online Retail transactional dataset
More than 500,000 transactions
Unit of analysis: CustomerID (aggregated level)

Technical Stack

Apache Spark (PySpark)

Spark MLlib

RFM Feature Engineering

VectorAssembler

StandardScaler (Z-score normalization)

KMeans

BisectingKMeans

Gaussian Mixture Model (GMM)

Logistic Regression

Random Forest

Linear Regression

Silhouette Score

Data Preparation

CSV ingestion using Spark

Cleaning invalid transactions

Handling missing CustomerID values

Formatting dates and monetary values

Creation of TotalPrice = Quantity × UnitPrice

Aggregation performed at the CustomerID level to construct behavioral indicators.

RFM Feature Engineering

Each customer is represented by:

Recency: Days since last purchase

Frequency: Number of distinct orders

Monetary: Total spending

Features are assembled into a dense vector and standardized using Z-score normalization.

Final dataset structure:

CustomerID | Recency | Frequency | Monetary | rfm_scaled

Unsupervised Segmentation
Models evaluated

KMeans

BisectingKMeans

Gaussian Mixture Model (GMM)

Model selection criterion

Silhouette score tested for k = 2 to 10.

Best model

BisectingKMeans
k = 3
Silhouette score ≈ 0.745

Gaussian Mixture Model produced significantly lower scores (best ≈ 0.54).

Cluster Interpretation

Three behavioral segments were identified:

High Value Customers

Dormant Customers

Growth Potential Customers

Cluster distribution:

Majority cluster: ~3,200 customers

Intermediate cluster: ~1,100 customers

High-value minority cluster: ~50 customers

Supervised Classification
Objective

Binary classification to identify high spenders.

Target definition:
High Spender = Monetary > 500

Features used:
Recency and Frequency only.

Results

Logistic Regression
Accuracy: 0.8132
F1-score: 0.8133

Random Forest
Accuracy: 0.8215
F1-score: 0.8203

Insight: Recency and Frequency alone strongly predict high-spending behavior.

Regression Modeling
Objective

Predict Monetary value using Recency and Frequency.

Baseline Linear Regression:

RMSE: 11346.80
R²: 0.1628

After log transformation:

RMSE: 1.0220
R²: 0.3079

Feature transformation significantly improved model performance.

Production Pipeline Concept

A production-ready architecture would include:

Periodic RFM recalculation

Automated cluster assignment

High-spender probability scoring

CRM campaign activation

This demonstrates how analytical models can be integrated into operational marketing systems.

Key Takeaways

End-to-end Spark ML pipeline successfully implemented.

Feature engineering proved more impactful than increasing model complexity.

Three-cluster segmentation provides the most actionable business insight.

Recency and Frequency are strong predictors of customer value.

Log transformation improved regression performance.
