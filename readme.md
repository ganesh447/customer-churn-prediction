<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Customer Churn Prediction</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            line-height: 1.7;
            color: #333;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 2rem;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }
        
        .header {
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            color: white;
            padding: 3rem 2rem;
            text-align: center;
            position: relative;
            overflow: hidden;
        }
        
        .header::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: repeating-linear-gradient(
                0deg,
                transparent,
                transparent 2px,
                rgba(255, 255, 255, 0.03) 2px,
                rgba(255, 255, 255, 0.03) 4px
            );
            animation: slide 20s linear infinite;
        }
        
        @keyframes slide {
            0% { transform: translateX(-50%) translateY(-50%) rotate(0deg); }
            100% { transform: translateX(-50%) translateY(-50%) rotate(360deg); }
        }
        
        .header h1 {
            font-size: 3rem;
            font-weight: 700;
            margin-bottom: 1rem;
            position: relative;
            z-index: 2;
        }
        
        .header .subtitle {
            font-size: 1.2rem;
            opacity: 0.9;
            position: relative;
            z-index: 2;
        }
        
        .content {
            padding: 3rem;
        }
        
        .section {
            margin-bottom: 3rem;
        }
        
        .section h2 {
            color: #1e3c72;
            font-size: 2rem;
            font-weight: 600;
            margin-bottom: 1.5rem;
            padding-bottom: 0.5rem;
            border-bottom: 3px solid #667eea;
            display: inline-block;
        }
        
        .section h3 {
            color: #2a5298;
            font-size: 1.4rem;
            font-weight: 600;
            margin: 2rem 0 1rem;
        }
        
        .intro-grid {
            display: grid;
            grid-template-columns: 2fr 1fr;
            gap: 2rem;
            margin-top: 2rem;
        }
        
        .intro-text {
            font-size: 1.1rem;
            line-height: 1.8;
        }
        
        .highlight-box {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 2rem;
            border-radius: 15px;
            text-align: center;
        }
        
        .highlight-box h4 {
            font-size: 1.2rem;
            margin-bottom: 1rem;
        }
        
        .models-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 1.5rem;
            margin: 2rem 0;
        }
        
        .model-card {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            padding: 2rem;
            border-radius: 15px;
            text-align: center;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        
        .model-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 30px rgba(240, 147, 251, 0.3);
        }
        
        .model-card.winner {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            border: 3px solid #fff;
            transform: scale(1.05);
        }
        
        .model-card h4 {
            font-size: 1.1rem;
            margin-bottom: 0.5rem;
        }
        
        .approach-steps {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 1.5rem;
            margin: 2rem 0;
        }
        
        .step {
            background: white;
            border: 2px solid #e1e8ed;
            border-radius: 15px;
            padding: 2rem;
            position: relative;
            transition: all 0.3s ease;
        }
        
        .step:hover {
            border-color: #667eea;
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(102, 126, 234, 0.1);
        }
        
        .step-number {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            position: absolute;
            top: -15px;
            left: 20px;
        }
        
        .tech-stack {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1rem;
            margin: 2rem 0;
        }
        
        .tech-item {
            background: linear-gradient(135deg, #ffecd2 0%, #fcb69f 100%);
            padding: 1.5rem;
            border-radius: 10px;
            text-align: center;
            transition: transform 0.3s ease;
        }
        
        .tech-item:hover {
            transform: scale(1.05);
        }
        
        .tech-item strong {
            color: #d63384;
            display: block;
            margin-bottom: 0.5rem;
        }
        
        .file-structure {
            background: #f8f9fa;
            border: 1px solid #e1e8ed;
            border-radius: 10px;
            padding: 2rem;
            font-family: 'Monaco', 'Consolas', monospace;
            margin: 2rem 0;
        }
        
        .file-structure pre {
            margin: 0;
            white-space: pre;
            overflow-x: auto;
        }
        
        .workflow-flow {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin: 2rem 0;
            flex-wrap: wrap;
            gap: 1rem;
        }
        
        .workflow-item {
            background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%);
            padding: 1rem 1.5rem;
            border-radius: 25px;
            text-align: center;
            flex: 1;
            min-width: 150px;
        }
        
        .arrow {
            font-size: 1.5rem;
            color: #667eea;
        }
        
        .next-steps {
            background: linear-gradient(135deg, #d299c2 0%, #fef9d7 100%);
            border-radius: 15px;
            padding: 2rem;
            margin: 2rem 0;
        }
        
        .next-steps ul {
            list-style: none;
            padding-left: 0;
        }
        
        .next-steps li {
            padding: 0.5rem 0;
            padding-left: 2rem;
            position: relative;
        }
        
        .next-steps li::before {
            content: "🎯";
            position: absolute;
            left: 0;
        }
        
        .badge {
            display: inline-block;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 0.3rem 0.8rem;
            border-radius: 15px;
            font-size: 0.8rem;
            font-weight: 500;
            margin: 0.2rem;
        }
        
        @media (max-width: 768px) {
            body {
                padding: 1rem;
            }
            
            .header h1 {
                font-size: 2rem;
            }
            
            .intro-grid {
                grid-template-columns: 1fr;
            }
            
            .content {
                padding: 2rem;
            }
            
            .workflow-flow {
                flex-direction: column;
            }
            
            .arrow {
                transform: rotate(90deg);
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🎯 Customer Churn Prediction</h1>
            <p class="subtitle">End-to-End Machine Learning Solution with Azure Cloud Services</p>
        </div>
        
        <div class="content">
            <div class="section">
                <h2>📋 Introduction</h2>
                <div class="intro-grid">
                    <div class="intro-text">
                        <p>This project implements a comprehensive machine learning solution to predict customer churn using Azure cloud services. The workflow covers the complete lifecycle: training, deployment, automated data ingestion, scoring, storage, and visualization.</p>
                        
                        <p>Machine learning models were trained in <strong>Azure Machine Learning Studio</strong>, where three algorithms were rigorously evaluated to determine the optimal approach for churn prediction.</p>
                    </div>
                    <div class="highlight-box">
                        <h4>🏆 Best Model</h4>
                        <p><strong>Two-Class Boosted Decision Trees</strong></p>
                        <p>Selected for highest accuracy and deployed as real-time endpoint</p>
                    </div>
                </div>
            </div>

            <div class="section">
                <h2>🤖 Model Evaluation</h2>
                <div class="models-grid">
                    <div class="model-card">
                        <h4>Two-Class Logistic Regression</h4>
                        <p>Linear approach with good interpretability</p>
                    </div>
                    <div class="model-card">
                        <h4>Two-Class Decision Forest</h4>
                        <p>Ensemble method with robust performance</p>
                    </div>
                    <div class="model-card winner">
                        <h4>🏆 Two-Class Boosted Decision Trees</h4>
                        <p><strong>WINNER - Highest Accuracy</strong></p>
                        <span class="badge">Production Model</span>
                    </div>
                </div>
            </div>

            <div class="section">
                <h2>🔧 Approach</h2>
                <div class="approach-steps">
                    <div class="step">
                        <div class="step-number">1</div>
                        <h4>Model Training</h4>
                        <p>Train and evaluate models in Azure Machine Learning Studio</p>
                    </div>
                    <div class="step">
                        <div class="step-number">2</div>
                        <h4>Model Deployment</h4>
                        <p>Deploy the best-performing model as a real-time endpoint</p>
                    </div>
                    <div class="step">
                        <div class="step-number">3</div>
                        <h4>Pipeline Creation</h4>
                        <p>Build Azure Data Factory pipeline for automation</p>
                    </div>
                    <div class="step">
                        <div class="step-number">4</div>
                        <h4>Data Integration</h4>
                        <p>Store results in Azure SQL Database</p>
                    </div>
                    <div class="step">
                        <div class="step-number">5</div>
                        <h4>Visualization</h4>
                        <p>Create Power BI dashboards for insights</p>
                    </div>
                </div>
            </div>

            <div class="section">
                <h2>📊 Evaluation Results</h2>
                <p>Three models were comprehensively tested with detailed evaluation metrics comparison. The <strong>Boosted Decision Trees</strong> algorithm demonstrated superior accuracy and was selected for production deployment.</p>
                <div class="highlight-box" style="margin-top: 1rem;">
                    <p>📈 Model evaluation reports are available in the <code>results/</code> directory</p>
                </div>
            </div>

            <div class="section">
                <h2>📁 Repository Structure</h2>
                <div class="file-structure">
                    <pre>├── data/                # Data files or references
├── notebooks/           # Training notebooks or AML experiment exports  
├── results/             # Model evaluation results
├── pipeline/            # Azure Data Factory pipeline JSON/snapshots
├── deployment/          # Endpoint configuration or scoring scripts
├── powerbi/             # Power BI reports or screenshots
└── README.md            # Project documentation</pre>
                </div>
            </div>

            <div class="section">
                <h2>🛠️ Technology Stack</h2>
                <div class="tech-stack">
                    <div class="tech-item">
                        <strong>Azure ML Studio</strong>
                        <p>Model training and deployment</p>
                    </div>
                    <div class="tech-item">
                        <strong>Azure Data Factory</strong>
                        <p>Data ingestion and orchestration</p>
                    </div>
                    <div class="tech-item">
                        <strong>Azure SQL Database</strong>
                        <p>Storage of scored data</p>
                    </div>
                    <div class="tech-item">
                        <strong>Power BI</strong>
                        <p>Visualization and reporting</p>
                    </div>
                    <div class="tech-item">
                        <strong>Python</strong>
                        <p>ML algorithms in Azure ML</p>
                    </div>
                </div>
            </div>

            <div class="section">
                <h2>🔄 Workflow Summary</h2>
                <div class="workflow-flow">
                    <div class="workflow-item">Data Ingestion<br><small>Azure Data Factory</small></div>
                    <div class="arrow">→</div>
                    <div class="workflow-item">ML Scoring<br><small>Deployed Endpoint</small></div>
                    <div class="arrow">→</div>
                    <div class="workflow-item">Data Storage<br><small>Azure SQL Database</small></div>
                    <div class="arrow">→</div>
                    <div class="workflow-item">Visualization<br><small>Power BI</small></div>
                </div>
            </div>

            <div class="section">
                <h2>🚀 Next Steps</h2>
                <div class="next-steps">
                    <ul>
                        <li>Automate retraining as new data arrives</li>
                        <li>Implement monitoring for data drift and model performance</li>
                        <li>Add CI/CD pipelines for continuous integration and deployment</li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</body>
</html>
