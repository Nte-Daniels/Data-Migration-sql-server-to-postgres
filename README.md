# Preface
This is a project that facilitates the Migration of Enterprise Data From SQL Server Database Into Postgres.

We will be using the following:
- SQL
- Python
- Jupyter Notebook


# Pseudocode

## High-level

1. Audit the data in SQL Server (before migration)
2. Extract the data from SQL Server (SSMS)
3. Transform the data
4. Load the data in postgreSQL
5. Validate the Data (after migration)
6. Generate a Validation report


## Low-Level

- Create a .env file
- Load env variables
- connect to SQL Server (pyodbc)
- Connect to postgres (psycopg2)
- Audit the Data
- For each table
- Get row count
- Extract all rows
- Transform the column names to lowercase
- Convert the data types
- Create tables in postgres
- Load tables into Postgres
- Run post-data migration checks
- Generate validation report.