# 🏠 Airbnb End-to-End Data Engineering Pipeline using dbt & Snowflake

## 📋 Project Overview

This project demonstrates a complete modern data engineering workflow using **Snowflake**, **dbt (Data Build Tool)**, **AWS**, and **Git**. The pipeline processes Airbnb data through a Medallion Architecture (Bronze → Silver → Gold) to create analytics-ready datasets.

The project showcases industry-standard practices including:

* Incremental data processing
* Medallion architecture
* Slowly Changing Dimensions (SCD Type 2)
* dbt Snapshots
* Custom Macros
* Data Testing
* Data Lineage
* Modular SQL Transformations

---

# 🏗️ Architecture

## Data Flow

```text
Source Data
    ↓
Snowflake Staging Layer
    ↓
Bronze Layer
    ↓
Silver Layer
    ↓
Gold Layer
    ↓
Analytics & Reporting
```

### Medallion Architecture

```text
STAGING
   ↓
BRONZE
   ↓
SILVER
   ↓
GOLD
```

---

# 🛠️ Technology Stack

| Component           | Technology   |
| ------------------- | ------------ |
| Data Warehouse      | Snowflake    |
| Transformation Tool | dbt Core     |
| Cloud Platform      | AWS          |
| Version Control     | Git & GitHub |
| Language            | SQL + Jinja  |
| Development Tool    | VS Code      |
| Documentation       | dbt Docs     |

---

# 📂 Project Structure

```text
aws_dbt_snowflake_project
│
├── analyses
│   ├── explore.sql
│   ├── if_else.sql
│   └── loop.sql
│
├── macros
│   ├── generate_schema_name.sql
│   ├── multiply.sql
│   ├── tag.sql
│   └── trimmer.sql
│
├── models
│   ├── bronze
│   │   ├── bronze_bookings.sql
│   │   ├── bronze_hosts.sql
│   │   └── bronze_listings.sql
│   │
│   ├── silver
│   │   ├── silver_bookings.sql
│   │   ├── silver_hosts.sql
│   │   └── silver_listings.sql
│   │
│   ├── gold
│   │   ├── fact.sql
│   │   ├── obt.sql
│   │   └── ephemeral
│   │       ├── bookings.sql
│   │       ├── hosts.sql
│   │       └── listings.sql
│   │
│   ├── sources
│   │   └── sources.yml
│   │
│   └── properties.yml
│
├── snapshots
│   ├── dim_bookings.yml
│   ├── dim_hosts.yml
│   └── dim_listings.yml
│
├── tests
│   └── source_tests.sql
│
├── seeds
├── dbt_project.yml
├── profiles.yml
└── README.md
```

---

# 🥉 Bronze Layer

The Bronze layer stores raw source data with minimal transformation.

### Models

* bronze_bookings
* bronze_hosts
* bronze_listings

### Purpose

* Raw data ingestion
* Initial standardization
* Incremental loading

---

# 🥈 Silver Layer

The Silver layer cleans, validates, and transforms data.

### Models

* silver_bookings
* silver_hosts
* silver_listings

### Transformations

* Null handling
* Data type conversions
* Data quality validation
* Business rule implementation

---

# 🥇 Gold Layer

The Gold layer provides business-ready datasets for analytics and reporting.

### Models

#### OBT (One Big Table)

Combines:

* Listings
* Hosts
* Bookings

into a single denormalized analytical table.

#### Fact Model

Creates a structured analytical fact table for reporting and dashboarding.

### Purpose

* Business Intelligence
* Reporting
* Dashboard Consumption

---

# 🔄 Incremental Models

The Bronze and Silver layers use dbt Incremental Models.

### Benefits

* Faster execution
* Lower compute costs
* Processes only new records

Example:

```sql
{{ config(materialized='incremental') }}
```

---

# 📸 Snapshots (SCD Type 2)

Snapshots track historical changes over time.

### Snapshot Models

* dim_bookings
* dim_hosts
* dim_listings

### Benefits

* Historical analysis
* Change tracking
* Point-in-time reporting

---

# ⚙️ Custom Macros

Reusable SQL logic created using Jinja.

### Available Macros

#### generate_schema_name.sql

Automatically routes models into:

* Bronze Schema
* Silver Schema
* Gold Schema

#### multiply.sql

Reusable multiplication function.

#### tag.sql

Business tagging logic.

#### trimmer.sql

String cleanup utility.

---

# 🧪 Data Testing

Custom tests ensure data quality.

### Test Coverage

* Source validation
* Null checks
* Business rule validation

Run:

```bash
dbt test
```

---

# 🚀 Running the Project

## Validate Configuration

```bash
dbt debug
```

## Run Models

```bash
dbt run
```

## Run Specific Layer

```bash
dbt run --select bronze.*
dbt run --select silver.*
dbt run --select gold.*
```

## Run Tests

```bash
dbt test
```

## Execute Snapshots

```bash
dbt snapshot
```

## Generate Documentation

```bash
dbt docs generate
dbt docs serve
```

---

# 📊 Snowflake Schemas

The project automatically creates and manages:

```text
AIRBNB.BRONZE
AIRBNB.SILVER
AIRBNB.GOLD
```

### Final Models

| Schema | Model           |
| ------ | --------------- |
| BRONZE | bronze_bookings |
| BRONZE | bronze_hosts    |
| BRONZE | bronze_listings |
| SILVER | silver_bookings |
| SILVER | silver_hosts    |
| SILVER | silver_listings |
| GOLD   | fact            |
| GOLD   | obt             |

---

# 📈 Key Learning Outcomes

* Data Warehousing Concepts
* Medallion Architecture
* Snowflake Data Engineering
* dbt Core Development
* Incremental Data Processing
* SCD Type 2 Implementation
* Data Testing
* Git & GitHub Workflow
* Modular SQL Development

---

# 🔐 Best Practices Implemented

* Layered architecture
* Reusable macros
* Incremental processing
* Historical tracking with snapshots
* Version control using Git
* Data quality validation
* Environment-based configuration

---

# 👨‍💻 Author

**Krish (Krishna Prasad M)**

Data Engineering Project using Snowflake, dbt, AWS, SQL, and GitHub.

---

# ⭐ Future Enhancements

* CI/CD Integration using GitHub Actions
* Data Quality Dashboard
* Power BI Dashboard Integration
* Apache Airflow Orchestration
* Real-Time Data Processing
* Advanced Monitoring & Alerting
