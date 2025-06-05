# Data Engineering Solutions: ETL, Data Warehousing, and Security Architecture

This repository contains solutions and architectural designs for core data engineering tasks, including automated ETL pipelines, dimensional data warehousing, and secure data access strategies. The work was completed as part of the CM2606 Data Engineering module at Robert Gordon University, Aberdeen.

## Table of Contents

- [ETL Pipeline on AWS with Apache Airflow](#etl-pipeline-on-aws-with-apache-airflow)
- [Dimensional Data Warehouse Design](#dimensional-data-warehouse-design)
- [Secure Data Access & Compliance Architecture](#secure-data-access--compliance-architecture)
- [Improvements and Future Work](#improvements-and-future-work)

---
## Refer the provided video (ETL_Video.mp4)
## ETL Pipeline on AWS with Apache Airflow

- **Infrastructure:** Deployed on AWS EC2 (t2.medium, Ubuntu), with Python virtual environment and Apache Airflow.
- **Security:** Configured IAM roles for S3 access, secure Airflow variables for API keys, and security groups for controlled network access.
- **Pipeline Design:**  
  - **API Health Check:** HTTP Sensor ensures OpenWeatherMap API is available before proceeding.
  - **Data Extraction:** HTTP Operator fetches weather data.
  - **Transformation & Load:** Python Operator flattens JSON data, transforms it into a pandas DataFrame, and streams CSV files to S3 with timestamped filenames.
  - **Monitoring:** Airflow UI provides real-time task monitoring and error tracking.
- **Scheduling:** DAG scheduled daily with retries and catchup disabled to prevent retroactive runs.
- **Evaluation:** Verified output by comparing with OpenWeatherMap dashboard; ensured correct CSV structure and timely execution.

---

## Dimensional Data Warehouse Design

A star schema was designed for a retail scenario (SuperMart), supporting advanced analytics and reporting.

- **Dimension Tables:**
  - **Store:** Location details for performance analysis by region.
  - **Product:** Product hierarchies for category and supplier analysis.
  - **Time:** Enables trend, seasonality, and period-over-period analysis.
  - **Customer:** Supports segmentation, loyalty analysis, and targeted marketing.
- **Fact Table:**  
  - **Sales Fact:** Contains transactional metrics (quantity, sales, discounts, profit) linked by foreign keys to all dimensions.
- **Aggregate Tables:**  
  - **Monthly Sales by Store & Category:** Optimizes monthly and category-based reporting.
  - **Daily Sales by Membership Level:** Enables analysis of loyalty program impact and customer behavior.
- **Star Schema Diagram:** Provided for clarity on table relationships and keys.

---

## Secure Data Access & Compliance Architecture

A layered security model was proposed for healthcare analytics (HIPAA/GDPR compliance):

- **Authentication:**  
  - Multi-Factor Authentication (MFA) for all users.
  - Single Sign-On (SSO) via OAuth 2.0/OpenID Connect.
  - Mutual TLS for service-to-service authentication.
  - Adaptive authentication based on risk context.
- **Authorization:**  
  - Hybrid Role-Based (RBAC) and Attribute-Based Access Control (ABAC) using policy engines (e.g., OPA).
  - Just-In-Time privilege elevation for sensitive tasks.
- **Data Protection:**  
  - AES-256 encryption at rest, TLS 1.3 in transit.
  - Column-Level Security (CLS) and Dynamic Data Masking (DDM) for sensitive fields.
  - Key management with HSMs or AWS KMS.
- **Auditing & Compliance:**  
  - Immutable audit logs (AWS CloudTrail, SIEM integration).
  - Automated data retention and lifecycle management.
  - Real-time monitoring and alerting for security events.
- **API Gateway:**  
  - Centralized API gateway (AWS API Gateway/Azure API Management) for secure, rate-limited, and tokenized access to aggregated, de-identified research datasets.

---

## Improvements and Future Work

- Migrate Airflow metadata backend from SQLite to PostgreSQL for parallelism and fault tolerance.
- Add real-time alerting (email/Slack) for ETL task status.
- Enhance data masking and access controls for evolving compliance needs.
- Expand aggregate tables and reporting for deeper business insights.

---

## Author

Chirath Setunge  

