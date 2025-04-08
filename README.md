# Data Pipeline for Airbnb Data Ingestion, Transformation, and Visualization

This project involves the end-to-end implementation of a data pipeline to ingest, transform, and visualize Airbnb data. The pipeline integrates various tools to ensure efficient data processing, transformation, and orchestration.

## Components

### 1. **Data Ingestion**
- **Source**: Airbnb data is ingested into Amazon S3 for storage.
- **Storage**: Amazon S3 is used as the data storage solution, providing scalability and reliability.

### 2. **Data Transformation**
- **Tool**: Snowflake is used as the data warehouse for transforming and processing the data.
- **dbt**: 
  - dbt is used to model and transform the data within Snowflake, creating views, tables, incremental, and ephemeral models.
  - **SCD Type 2**: Implemented Slowly Changing Dimension (SCD) Type 2 using dbt snapshots to track historical changes.
  - **Data Staleness**: Managed data staleness by maintaining source data and scheduling tests to ensure data freshness.
  - **Testing**: 
    - Custom and generic tests are created using dbt macros for data quality validation.
    - Used dbt's **Expectations Framework** for advanced testing, ensuring robust data accuracy.
    - **dbt Exposure**: Documented dashboards and exposed data models for better insight and usage.
  - **Permissions**: Managed table permissions with dbt hooks to ensure secure access to data.

### 3. **Orchestration**
- **Tool**: Dagster is used for pipeline orchestration, enabling automated workflow management.
  - **Partitioned Incremental Models**: Partitioning and incremental models are implemented to optimize performance and backfilling.
  - **Job Scheduling**: Automates job scheduling for efficient data processing workflows.

### 4. **Visualization**
- **Tool**: Preset is used for data visualization and dashboarding, providing intuitive visual insights into the data.
  
## Tools Used
- **Snowflake**: Data warehousing solution to store and process transformed data.
- **dbt**: Data transformation and testing framework to model and test data.
- **Dagster**: Workflow orchestration tool for managing pipeline execution and scheduling.
- **Amazon S3**: Cloud storage for ingesting and storing raw data.
- **Preset**: A visualization tool for creating interactive dashboards and data visualizations.

## Project Workflow
1. **Data Ingestion**: Raw Airbnb data is loaded into Amazon S3.
2. **Data Transformation**: The data is processed in Snowflake using dbt to transform raw data into structured views, tables, and incremental models.
3. **Testing**: Data is tested for accuracy and freshness using dbt's testing framework and custom dbt macros.
4. **Orchestration**: Dagster schedules and orchestrates the entire workflow, including incremental model updates and backfilling.
5. **Visualization**: Dashboards are created using Preset to visualize key metrics and provide insights into the Airbnb data.

## Setup and Configuration

### Prerequisites
- Snowflake account
- dbt installed and configured
- Dagster environment set up for orchestration
- Amazon S3 bucket for data storage
- Preset account for visualization

### How to Run
1. **Data Ingestion**: Configure S3 ingestion to upload Airbnb data into the designated bucket.
2. **Data Transformation**: Set up dbt profiles and run dbt models to transform raw data into structured data.
   ```bash
   dbt run

### Resources:
- Learn more about dbt [in the docs](https://docs.getdbt.com/docs/introduction)
- Learn how to integrate dbt with [Snowflake](https://www.getdbt.com/data-platforms/snowflake)
- Step-by-step dbt setup for Snowflake in the [Quickstart Guide](https://quickstarts.snowflake.com/guide/data_teams_with_dbt_cloud/)
- Comprehensive guide to dbt on Snowflake [here](https://medium.com/%40dipan.saha/dbt-on-snowflake-a-comprehensive-guide-a849e893a2e)

