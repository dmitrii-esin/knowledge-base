# Databricks Overview

## Overview
- **Objective**: Understand and utilize Databricks for managing and analyzing large datasets.
- **Importance**: Databricks simplifies working with big data by providing an efficient, scalable platform for data preparation, real-time analysis, and machine learning.
- **Prerequisites**: Basic knowledge of big data concepts and familiarity with Apache Spark.

## Key Concepts
- **Data Warehouse vs Data Lake**: 
  - **Data Warehouse**: Structured and verified, suitable for long-term unchanged data.
  - **Data Lake**: Unverified, ideal for machine learning and AI applications.
- **Delta Lake**: Enhances data lakes with reliability by supporting ACID transactions, rollbacks, and versioning.
- **DataFrame**: A distributed collection of data organized into named columns.
- **Databricks Components**:
  - **Workspace**: Organizes projects.
  - **Clusters**: Sets of compute resources.
  - **Notebooks**: Documents for code and execution.
  - **Jobs**: Automates tasks.
  - **Delta Lake**: Provides a reliable data lake.
  - **Pre-packaged Libraries**: Facilitates interaction with SQL databases, cloud platforms, and programming languages like Python, Java, and Scala.
- **Databricks Volumes and File System**: Essential for data storage and management within the platform.
- **Pipeline**: The main unit of execution in Databricks.

## Tools and Technologies
- **Apache Spark**: Foundation of Databricks, a distributed big data processing engine that uses distributed RDD (Resilient Distributed Dataset) system.

## Learning Resources
- **Documentation**:
  - [Databricks Official Documentation](https://docs.databricks.com/) - Comprehensive resource for all Databricks functionalities.

## Practical Exercises
- **Exercise 1**: Set up a Databricks workspace and create a simple cluster.
- **Exercise 2**: Import data into Delta Lake and perform basic data transformations.
- **Exercise 3**: Build a simple data processing pipeline using Databricks notebooks.

## Projects
- **Project 1**: Analyze real-time data streams using Databricks and Apache Kafka to gain insights from live data sources.

## Challenges and Solutions
- **Challenge 1**: Managing large datasets efficiently.
  - **Solution**: Utilize Delta Lake for scalable and reliable data management within Databricks.

## Key Takeaways
- **Takeaway 1**: Databricks provides an integrated platform based on Apache Spark to simplify big data processing and analysis.
- **Takeaway 2**: Delta Lake is crucial for ensuring data reliability in a data lake environment.

## Additional Notes
- **Deployment Models**: Databricks can be deployed on-premise or on cloud platforms such as Azure, Google Cloud, and AWS.
- **Interaction with Databricks**: Can be done through CLI, UI, SDK, and JDBC driver.
- **Basic Workflow**:
  1. Configure parameters, pricing, deployment, account, and security settings.
  2. Create a workspace and set up clusters and notebooks.
  3. Connect to external data sources and ingest data either through batch or streaming methods.
  4. Use Delta Live Tables for reliable data processing pipelines.
  5. Optionally, use Lakehouse Federation or Delta Sharing for cross-platform data sharing without data duplication.
- **Data Ingestion Methods**:
  - **Batch Ingestion**: Ingest a set data rows for infrequent processing from sources like CSV, Amazon S3, SQL Server, Salesforce, etc.
  - **Streaming Ingestion**: Recommended for real-time processing using Apache Kafka, Amazon Kinesis, etc.
  - **DIY Ingestion**: Custom ingestion using custom connectors.
  - **Ingestion Alternatives**: Using Lakehouse Federation or Delta Sharing to query shared data across platforms and clouds without copying data into Databricks.

This markdown organizes essential information about Databricks, making it easier to reference key aspects and functionalities for effective learning and application.


<!-- source:
Databricks is a cloud-based platform for managing and analyzing large datasets using the Apache Spark open-source big data processing engine.
Databricks is designed to make working with big data easier and more efficient, by providing tools and services for data preparation, real-time analysis, and machine learning. Some key features of Databricks include support for various data formats, integration with popular data science libraries and frameworks, and the ability to scale up and down as needed.

Data warehouse (structured and verified, good for long-term unchanged data) vs data lake (unverified, good for ML, AI)

Delta-lake - brings reliability for data-lake (Branded set of technologies and the framework, allows ACID transactions, rollback, versioning/)

Databricks components 
Workspace (to organize the project)
Clusters (set of compute resources)
Notebooks (code document, execution unit)
Jobs (to automate the work)
Delta lake (reliable data lake)
Pre-packaged libraries (working with SQL dbs, cloud platforms, python function, java, scala libs, etc.)

A DataFrame is a distributed collection of data organized into named columns.
Data-bricks volumes, databricks file system


Pipeline - main unit of execution.

Based on Apache Spark engine (distributed RDD system)

Interaction with the databricks
CLI
UI
SDK
*JDBC driver

Deployment models: 
on-prem, cloud (Azure, Google, AWS)

Basic workflow:
Configure the params, pricing, etc, deployment, account and security settings
Create workspace (clusters => notebooks)
Connect databricks to external data sources
Ingest your data into the workspace 
Batch ingestion of a set data rows for infrequent processing: CSV, Amazon S3, SQL server, SalesForce etc. Streaming tables using SQL to load your data incrementally, cloud object storage connector for AWS/Google/Azure Data Lake or fully-managed connectors.
Streaming (RECOMMENDED) ingestion for real-time processing using Apache Kafka, Amazon Kinesis, etc.
Delta Live Tables to build reliable data processing pipelines (combination of A and B)
DIY Ingestion (custom ingestion by using custom connector)
Ingestion alternatives if you don’t want to copy data into data bricks: using Lakehouse Federation or Delta Sharing to query share data across platforms and clouds
Onboard data to your workspace (Load data using streaming tables in Databricks SQL): build query, run, monitor history, build pipelines for data orchestration, process your data -->





