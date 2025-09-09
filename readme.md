<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Customer Churn Prediction</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            max-width: 900px;
            margin: auto;
            padding: 20px;
            color: #333;
        }
        h1, h2, h3 {
            color: #2c3e50;
        }
        pre {
            background: #f4f4f4;
            padding: 10px;
            border-left: 3px solid #2c3e50;
            overflow-x: auto;
        }
        ul {
            margin: 10px 0 10px 20px;
        }
        code {
            background: #f4f4f4;
            padding: 2px 4px;
            border-radius: 3px;
        }
        table {
            border-collapse: collapse;
            width: 100%;
            margin: 10px 0;
        }
        table, th, td {
            border: 1px solid #ccc;
        }
        th, td {
            padding: 8px 12px;
            text-align: left;
        }
    </style>
</head>
<body>

<h1>Customer Churn Prediction</h1>

<h2>Introduction</h2>
<p>This project implements an end-to-end machine learning solution to predict customer churn using Azure cloud services. The workflow covers the complete lifecycle: training, deployment, automated data ingestion, scoring, storage, and visualization.</p>

<p>Machine learning models were trained in <strong>Azure Machine Learning Studio</strong>, where three algorithms were evaluated:</p>
<ul>
    <li>Two-Class Logistic Regression</li>
    <li>Two-Class Decision Forest</li>
    <li>Two-Class Boosted Decision Trees</li>
</ul>

<p>The <strong>Two-Class Boosted Decision Trees</strong> model was selected as it delivered the highest accuracy. This model was deployed as a real-time endpoint in Azure ML Studio, enabling live scoring of customer data.</p>

<p>An <strong>Azure Data Factory (ADF) pipeline</strong> was developed to orchestrate the process. It ingests new customer data, sends it to the deployed endpoint for scoring, and stores the results in <strong>Azure SQL Database</strong>. The scored results are then connected to <strong>Power BI</strong>, providing interactive dashboards to monitor and analyze churn predictions.</p>

<h2>Approach</h2>
<ul>
    <li>Train and evaluate models in Azure Machine Learning Studio.</li>
    <li>Deploy the best-performing model as a real-time endpoint.</li>
    <li>Build an Azure Data Factory pipeline to:
        <ul>
            <li>Ingest customer data</li>
            <li>Score the data via the ML endpoint</li>
            <li>Store results in Azure SQL Database</li>
            <li>Visualize predictions in Power BI dashboards</li>
        </ul>
    </li>
</ul>

<h2>Evaluation</h2>
<ul>
    <li>Three models were tested, and evaluation metrics compared.</li>
    <li>Boosted Decision Trees showed the best accuracy and was selected for production.</li>
    <li>Model evaluation reports are available in the <code>results/</code> directory.</li>
</ul>

<h2>Repository Structure</h2>
<pre>
├── data/                # Data files or references
├── notebooks/           # Training notebooks or AML experiment exports
├── results/             # Model evaluation results
├── pipeline/            # Azure Data Factory pipeline JSON/snapshots
├── deployment/          # Endpoint configuration or scoring scripts
├── powerbi/             # Power BI reports or screenshots
└── README.md            # Project documentation
</pre>

<h2>Technology Stack</h2>
<ul>
    <li>Azure Machine Learning Studio – Model training and deployment</li>
    <li>Azure Data Factory – Data ingestion and orchestration</li>
    <li>Azure SQL Database – Storage of scored data</li>
    <li>Power BI – Visualization and reporting</li>
    <li>Python – Underlying ML algorithms in Azure ML</li>
</ul>

<h2>Workflow Summary</h2>
<ul>
    <li>Data ingestion through Azure Data Factory</li>
    <li>Scoring via the deployed ML endpoint</li>
    <li>Storage of results in Azure SQL Database</li>
    <li>Visualization in Power BI</li>
</ul>

<h2>Next Steps</h2>
<ul>
    <li>Automate retraining as new data arrives.</li>
    <li>Implement monitoring for data drift and model performance.</li>
    <li>Add CI/CD pipelines for continuous integration and deployment.</li>
</ul>

</body>
</html>
