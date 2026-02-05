# SQL Server to PostgreSQL Data Migration Pipeline

This project implements an end-to-end data migration pipeline for transferring enterprise data from Microsoft SQL Server to PostgreSQL using Python.

It was designed to simulate a real-world database migration scenario, focusing on data integrity, validation, automation, and reliability rather than simple one-time exports.

The pipeline handles schema replication, bulk data transfer, validation, and reporting through a structured Jupyter Notebook workflow.

---

## Project Motivation

In enterprise environments, database migrations are high-risk operations.  
A failed migration can result in data loss, downtime, and business disruption.

This project was built to demonstrate how a production-style migration process can be implemented using open-source tools, with an emphasis on:

- Auditability
- Data quality
- Repeatability
- Validation
- Performance
- Transparency

Instead of manually exporting and importing tables, the pipeline automates the entire process and verifies that the target system is an accurate replica of the source.

---

## Design Philosophy

The pipeline was designed around three core principles:

### 1. Reliability First

Every migration step is validated before and after execution:

- Baseline row counts are captured
- Data quality checks are performed
- Primary and foreign keys are verified
- Referential integrity is enforced

No table is considered successfully migrated until it passes validation.

---

### 2. Automation Over Manual Processes

All major tasks are automated:

- Schema extraction
- Type conversion
- Table creation
- Data loading
- Verification
- Reporting

This minimizes human error and enables repeatable executions.

---

### 3. Production-Oriented Workflow

The project mirrors real enterprise migration practices:

- Environment-based configuration
- Transaction management
- Rollbacks on failure
- Batched inserts
- Logging and reporting

The workflow is structured as a controlled ETL pipeline rather than a one-off script.

---

## What This Pipeline Does

### 1. Pre-Migration Auditing

Before any data is moved, the pipeline audits the SQL Server database:

- Captures baseline row counts
- Detects null values in critical fields
- Identifies invalid email formats
- Finds orphaned foreign keys
- Flags future-dated records

This establishes a trusted reference point for validation.

---

### 2. Schema Extraction and Mapping

The pipeline extracts metadata from SQL Server system catalogs and builds PostgreSQL-compatible schemas.

Key steps include:

- Reading column definitions
- Mapping SQL Server types to PostgreSQL types
- Preserving nullability constraints
- Reconstructing primary keys
- Creating target tables automatically

This removes the need for manual schema recreation.

---

### 3. Data Transformation

During extraction, the data is normalized to match PostgreSQL conventions:

- Column names converted to lowercase
- Boolean fields normalized
- Type inconsistencies resolved
- Format adjustments applied

This ensures compatibility and consistency.

---

### 4. High-Performance Data Loading

Data is loaded using bulk inserts with `psycopg2.execute_values`, which provides:

- Batched inserts
- Reduced network overhead
- Improved throughput
- Transaction safety

Target tables are truncated and reset before loading to avoid conflicts.

---

### 5. Post-Migration Validation

After loading, the pipeline validates the migration:

- Row counts compared with baseline
- Primary key uniqueness verified
- Foreign key relationships checked
- Data types inspected

Any mismatch is reported immediately.

---

### 6. Reporting and Visualization

The final stage generates validation reports and visualizations:

- Row count comparisons
- Log-scaled bar charts
- Summary validation output

This provides stakeholders with clear confirmation of migration success.

---

## Technical Stack

The project uses widely adopted, production-ready tools:

- Python 3 for orchestration
- pandas for data handling
- pyodbc for SQL Server connectivity
- psycopg2 for PostgreSQL access
- matplotlib for reporting
- python-dotenv for configuration management
- Jupyter Notebook for structured execution

This stack enables portability and maintainability.

---

## Project Structure

Data-Migration-sql-server-to-postgres/
  │
- ├── run_migration_uat.ipynb # Main migration workflow
- ├── generate_data.py # Synthetic data generator
- ├── .env # Environment configuration
- ├── .gitignore # Version control rules
- └── README.md # Documentation


The notebook acts as the main orchestration layer, while configuration is isolated through environment variables.

---

## Architectural Overview

The pipeline follows a classic ETL model:

SQL Server → Extraction → Transformation → Loading → Validation → Reporting



Each phase is isolated, auditable, and restartable.

This design allows partial re-runs and controlled recovery in case of failure.

---

## Key Engineering Decisions

### Use of System Catalogs

Instead of hardcoding schemas, the pipeline queries SQL Server metadata to dynamically generate PostgreSQL tables.

This makes the solution adaptable to new databases.

---

### Environment-Based Configuration

All credentials are stored in `.env` files to:

- Avoid hardcoding secrets
- Enable environment portability
- Support deployment pipelines

---

### Bulk Loading Strategy

Using `execute_values` provides orders-of-magnitude performance improvement compared to row-by-row inserts.

This approach is essential for large datasets.

---

### Validation as a First-Class Step

Validation is treated as part of the pipeline, not an afterthought.

This reflects real enterprise migration standards.

---

## Limitations

- Designed for batch migrations
- No real-time synchronization
- No change data capture (CDC)
- Assumes relatively stable schemas

These trade-offs were made to focus on correctness and reliability.

---

## Future Enhancements

Potential extensions include:

- Incremental replication
- Workflow orchestration (Airflow/Prefect)
- Dockerized deployment
- Cloud-native migration support
- Automated CI/CD validation

---

## Learning Outcomes

This project demonstrates:

- Practical ETL pipeline design
- Database internals knowledge
- Data quality engineering
- Migration risk management
- Performance optimization
- Validation-driven development

It reflects production-oriented thinking rather than scripting.

---

## Author

Developed by **Nte Daniels**

Focus Areas:  
Data Engineering | ETL Pipelines | Analytics | Database Systems

---

## License

MIT License

