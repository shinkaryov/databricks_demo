# Databricks Serverless ETL Demo

Welcome to the demonstration pipeline for data processing (ETL) using **PySpark** and **Databricks Asset Bundles (DAB)**. 
This project is designed as a practical example for RDBMS students to explore modern Data Engineering practices, RDBMS concepts, and Cloud-native workflows.

🐾 *The chief data expert and project mascot is Set the Labrador, who is always strictly monitoring our data quality!*

## Project Structure

```text
repo/
├── resources/              # Infrastructure definitions (Unity Catalog Schema & Serverless Job)
│   └── pipelines.yml
│   └── schemas.yml  
├── databricks.yml          # Main bundle configuration file
├── pipelines.yml           # Infrastructure definitions (Unity Catalog Schema & Serverless Job)
├── etl/
│   └── Process.ipynb       # Core PySpark notebook with transformation logic
└── README.md               # This file
```

## Project Structure

Before running this demo, ensure you have:

1. Access to a Databricks Workspace (Free Edition or a paid tier with Unity Catalog and Serverless Compute enabled).
2. This repo connected to Git folder in Databricks

## Deployment (UI / ClickOps)
This project uses an Infrastructure as Code (IaC) approach, meaning all resources are created automatically without writing manual SQL scripts for schemas or manually configuring job clusters. We will deploy everything directly from the Databricks UI.

## Step-by-Step Deployment:

1. Open your Databricks workspace and navigate to the repo folder.
2. Open any databricks.yml file, change link to your workspace url and press on the rocket.
3. In the Deployments panel:
      - Source: verify it points to flights_etl_pipeline.
      - Target: select your desired deployment environment from the dropdown (e.g., prod or dev).
      - Review the Bundle resources listed below (you should see the flights schema and the Flights_Serverless_ETL job).
      - Click the 🚀 Deploy button.

Databricks will automatically read the pipelines.yml and schemas.yml file, register the schema in Unity Catalog, and create the job.

##  Running the Pipeline
Once the deployment is successful, you can trigger the ETL process:
1. In the Databricks UI sidebar, go to Workflows > Jobs.
2. Search for the newly created job named Flights_Serverless_ETL.
3. Click the Run now button in the top right corner.

What happens under the hood?
1. The job launches instantly using Serverless Compute (no waiting for VMs to spin up).
2. The Process.ipynb notebook receives the target schema name and table name dynamically via Databricks Widgets.
3. Raw data is transformed (feature engineering, aggregations) and saved securely as a highly optimized Delta Table inside your Unity Catalog schema.
