# Fitness Centre Medallion Data Platform

## Problem Statement

Modern fitness centres collect large volumes of data from registration portals, IoT heart rate devices, workout tracking systems, and mobile apps. However, this data is frequently siloed, arrives at different speeds, and is difficult to analyze in real time. As a result, business leaders lack actionable insights for improving user experience, optimizing resources, and boosting retention.

---

## Solution Overview

This project demonstrates a production-grade, modular medallion architecture for a fitness centre analytics platform, built on Azure Data Lake Storage Gen2, Databricks, Delta Lake, and Kafka. It highlights cloud provisioning, robust data engineering practices, and automated deployment using CI/CD.

---

## Architecture Overview
**Cloud-Ready Architecture:** Implements the medallion architecture (bronze, silver, gold) on Azure Data Lake Storage Gen2 and Databricks with robust access controls and Unity Catalog.

**End-to-End Pipeline:** Covers streaming ingestion (Kafka multiplexed user/device streams), batch CDC updates, and modular table setup from landing to analytics-ready gold outputs.

**Production Best Practices:**

- Modular notebooks, reusable functions, data validation, checkipoints, assert/verify steps  
- Streaming ingestion with Autoloader (Cloudfiles), CDC with upsert (merge) logic in PySpark  
- Parameterized orchestration using Databricks widgets for job control  

**CI/CD Enabled:** Full version control with git, automated lint/test/build/deploy using GitHub Actions and Databricks Jobs API.

**Security & Compliance:** All cloud credentials and secrets are handled via managed services and not stored in this repository.

**Clear Documentation:** Architecture is explained with diagrams, a step-by-step runbook, and code comments.

</br>

<p align="center">
  <img width="1200" height="620" alt="Fitness Centre Medallion Data Platform Architecture drawio (1)" src="https://github.com/user-attachments/assets/31b2ead3-87c0-4173-af8b-5ee5a4dea24b" />
</p>

---

## Technical Features

- Provisioned ADLS Gen2, managed access via Access Connector  
- Databricks workspace set up with Unity Catalog for centralized governance  
- Notebooks organized as reusable modules:  
  - Setup notebook creates all databases/tables across bronze, silver, gold layers  
  - Batch/Stream Loaders: Autoloader for ingestion from ADLS/Kafka topics  
  - CDC/Upsert Logic: Implements robust merge patterns for user profile updates  
  - Validation: Setup and table assertion checks  
  - Configurable Runs: Environment and microbatch interval set via widgets  
- Automated CI/CD pipeline:  
  - Git-managed source  
  - Actions workflows for test, deploy, and secret management  

---

## Data Sources & Pipeline Workflow

- Sources include registration, user profile (CDC streams), BPM stream, workout sessions  
- Kafka multiplex topics used for streaming ingestion  
- Medallion Layer Structure:
  - Raw: Raw landing data ingestion 
  - Bronze: Structured raw Delta tables
  - Silver: Cleansed, deduplicated, CDC-upserted business entities  
  - Gold: Aggregated datasets supporting analytics and reporting  
- Modular notebook scripts for setup, ingestion, transformation, validation, and orchestration
  
</br>
<img width="1396" height="736" alt="Screenshot 2025-11-19 at 16 34 09" src="https://github.com/user-attachments/assets/84d5ed38-6023-45e0-9d27-a97ea47121e6" />

---

## Validation and Testing

- Data assertions and validation implemented in setup and batch-test notebooks  
- End-to-end pipeline correctness ensured by automated tests integrated.  
- Regular integrity checks to maintain data quality across layers

</br>
<img width="1249" height="643" alt="Screenshot 2025-11-19 at 16 24 52" src="https://github.com/user-attachments/assets/70a6a5d3-a768-479f-b76a-d88f47abeb22" />

---

## CI/CD & Deployment Implementation

- Code and notebooks version-controlled with GitHub  
- GitHub Actions workflows for deployment automation  
- Deployment triggered via Databricks Jobs API with environment-specific configurations  
- Secrets managed securely with GitHub Secrets and Azure Key Vault integration

</br>
<img width="1040" height="461" alt="Screenshot 2025-11-19 at 16 21 18" src="https://github.com/user-attachments/assets/3b760844-1935-476f-8b36-616a5603f11b" />

---

## Business Impact & Usage

- **Live Decision Support:** Provides managers with real-time gym usage data and equipment demand, enabling better scheduling and resource planning.  
- **Personalized Fitness Experiences:** Tracks individual performance and health metrics to offer tailored recommendations, improving member satisfaction and reducing churn.  
- **Retention and Revenue Growth:** Analytics on workout habits and attendance help identify at-risk members, allowing for timely intervention and offers.  
- **Operational Optimization:** Enables data-driven staff allocation and maintenance scheduling based on actual patterns, reducing costs.  
