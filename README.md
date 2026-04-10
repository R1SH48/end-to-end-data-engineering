# End-to-End Data Pipeline: Kaggle to Databricks

## 🚀 Overview
This project demonstrates a professional workflow for handling large-scale datasets (>1GB) that exceed standard browser or CloudShell upload limits.

## 🏗️ Architecture
1. **Source**: Kaggle Dataset via `kagglehub`.
2. **Bridge**: AWS EC2 (t3.micro) used for high-speed transfer.
3. **Storage**: Amazon S3 (ap-south-1).
4. **Processing**: Databricks Community Edition using PySpark.

## 🛠️ Key Technical Challenges Overcome
- **1GB Upload Limit**: Bypassed AWS CloudShell storage limits by using an EC2 instance with SCP for data transfer.
- **S3 Connectivity**: Configured `s3a` connector options in Spark to securely access S3 buckets without mounting.
- **DBFS Restrictions**: Navigated `DBFS_DISABLED` errors by utilizing modern Spark configurations and DataFrame options.

## 📊 How to Run
1. Configure AWS IAM with `S3FullAccess`.
2. Use `scp` to move data from local to EC2.
3. Transfer data from EC2 to S3 using AWS CLI.
4. Run the provided Databricks notebook to ingest and query the data.
