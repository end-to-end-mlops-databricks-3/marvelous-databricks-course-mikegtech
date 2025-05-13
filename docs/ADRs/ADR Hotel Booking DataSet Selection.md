# ADR: Selection of the Hotel Booking Kaggle Dataset

## Overview

We need a publicly available, well-documented dataset to showcase end-to-end MLOps workflows—data ingestion, preprocessing, feature engineering, model training, validation, deployment, and monitoring—within a Databricks production environment. After evaluating several options, the Kaggle **Hotel Booking Demand** dataset (mojtaba142/hotel-booking-demand) has been selected.

## Issue

Identify a dataset that:

* Contains diverse numerical and categorical features with temporal context.
* Is of sufficient size for realistic experimentation but manageable within a Databricks workspace.
* Has a clear, permissive license and easy reproducibility via API.

## Decision

Use the Kaggle **Hotel Booking Demand** dataset by mojtaba142. Highlights:

* Approximately 119K hotel bookings (2015–2017).
* 32 features covering guest demographics, booking details, hotel type, and stay information.
* Two distinct hotel types (City vs. Resort) for segmentation.
* CC BY-SA 4.0 license supports academic and demonstration use.

## Status

**Approved**: Ready for ingestion into Databricks for MLOps pipeline development and demonstration.

## Assumptions

1. Historical 2015–2017 booking data adequately illustrate MLOps processes.
2. Data will be stored as Delta Lake tables in Databricks.
3. Databricks compute and storage resources are available to run Spark jobs at scale.
4. Users have valid Kaggle API credentials for reproducible dataset retrieval.

## Constraints

* Dataset limited to two hotel categories; not broadly representative of all hospitality contexts.
* Potential class imbalance (e.g., cancellations vs. stays) may need mitigation strategies.
* Missing or inconsistent values in fields like `country` and `children` require cleaning.

## Implications

* **Ingestion & Storage**: Automate data retrieval via Kaggle API; load CSV into Delta Lake using Databricks notebooks or jobs.
* **Data Versioning**: Leverage Databricks Unity Catalog or DVC-on-DBFS for version control of raw and transformed data.
* **Feature Engineering**: Implement within Databricks notebooks or MLflow Projects, deriving time-based, categorical, and aggregated features.
* **Model Development & Tracking**: Train and log models using MLflow on Databricks; support both classification (cancellation prediction) and regression (e.g., lead time forecasting).
* **Deployment & Serving**: Package models as Databricks Model Serving endpoints or as REST APIs via MLflow deployment.
* **Monitoring & Governance**: Use Databricks-native monitoring for data drift, model performance, and auditability via Unity Catalog.

## Notes

* **Reproducible Pull**:

  ```bash
  kaggle datasets download -d mojtaba142/hotel-booking-demand
  ```
* Consider synthetic data augmentation or resampling techniques to address class imbalance.
* Document dataset schema and processing steps in the project repository README.
