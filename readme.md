Customer Churn Prediction
Introduction

This project implements an end-to-end machine learning solution to predict customer churn using Azure cloud services. The workflow covers the complete lifecycle: training, deployment, automated data ingestion, scoring, storage, and visualization.

Machine learning models were trained in Azure Machine Learning Studio, where three algorithms were evaluated:

Two-Class Logistic Regression

Two-Class Decision Forest

Two-Class Boosted Decision Trees

The Two-Class Boosted Decision Trees model was selected as it delivered the highest accuracy. This model was deployed as a real-time endpoint in Azure ML Studio, enabling live scoring of customer data.

An Azure Data Factory (ADF) pipeline was developed to orchestrate the process. It ingests new customer data, sends it to the deployed endpoint for scoring, and stores the results in Azure SQL Database. The scored results are then connected to Power BI, providing interactive dashboards to monitor and analyze churn predictions.

Approach

Train and evaluate models in Azure Machine Learning Studio.

Deploy the best-performing model as a real-time endpoint.

Build an Azure Data Factory pipeline to:

Ingest customer data

Score the data via the ML endpoint

Store results in Azure SQL Database

Visualize predictions in Power BI dashboards.

Evaluation

Three models were tested, and evaluation metrics compared.

Boosted Decision Trees showed the best accuracy and was selected for production.

Model evaluation reports are available in the results/ directory.

Repository Structure
├── data/                # Data files or references
├── notebooks/           # Training notebooks or AML experiment exports
├── results/             # Model evaluation results
├── pipeline/            # Azure Data Factory pipeline JSON/snapshots
├── deployment/          # Endpoint configuration or scoring scripts
├── powerbi/             # Power BI reports or screenshots
└── README.md            # Project documentation

Technology Stack

Azure Machine Learning Studio – Model training and deployment

Azure Data Factory – Data ingestion and orchestration

Azure SQL Database – Storage of scored data

Power BI – Visualization and reporting

Python – Underlying ML algorithms in Azure ML

Workflow Summary

Data ingestion through Azure Data Factory

Scoring via the deployed ML endpoint

Storage of results in Azure SQL Database

Visualization in Power BI

Next Steps

Automate retraining as new data arrives.

Implement monitoring for data drift and model performance.

Add CI/CD pipelines for continuous integration and deployment.
