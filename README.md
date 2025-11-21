# SQL Data Warehouse

A portfolio project that demonstrates how to design and build a SQL Server data warehouse using the Medallion Architecture (Bronze → Silver → Gold). It includes ETL patterns, a star-schema analytical model, and SQL-based analytics examples.

## Project Goals
- Show a clear end-to-end warehouse design on SQL Server.
- Practice Medallion layering with Bronze (raw), Silver (cleansed), and Gold (analytics) schemas.
- Provide starter scripts you can adapt for your own datasets and environment.

## Repository Structure
- `scripts/init_database.sql` — Drops/recreates the `DataWarehouse` database and sets up the `bronze`, `silver`, and `gold` schemas.
- `datasets/` — Placeholder for sample data files you want to load into the warehouse layers.
- `docs/` — Space for architecture diagrams, ERDs, and design notes.
- `tests/` — Placeholder for automated checks (e.g., dbt tests or SQL unit tests) if you add them later.

## Getting Started
1. **Prepare SQL Server**
   - Ensure you have access to a SQL Server instance (local or remote).
   - Create a login with permissions to create/drop databases and schemas.

2. **Initialize the Warehouse**
   - Review the warning at the top of `scripts/init_database.sql`—it will drop and recreate a database named `DataWarehouse`.
   - Run the script in SQL Server Management Studio or `sqlcmd`:
     ```bash
     sqlcmd -S <server> -U <user> -P <password> -i scripts/init_database.sql
     ```

3. **Load Data**
   - Place raw source files in `datasets/` and design your Bronze ingestion process (e.g., bulk insert or SSIS/ADF pipeline).
   - Create transformation scripts to promote data to Silver (cleansed/conformed) and Gold (facts/dimensions). Store them in `scripts/` or a dedicated `etl/` folder.

4. **Modeling Guidance**
   - **Bronze**: Land raw files with minimal transformation; keep source fidelity.
   - **Silver**: Standardize types, deduplicate, and apply business rules.
   - **Gold**: Build star schemas (facts/dimensions) and semantic views for BI tools.

5. **Testing and Quality**
   - Add SQL assertions or dbt tests under `tests/` to validate constraints, nullability, and referential integrity.
   - Consider data freshness checks on Bronze loads and row-count reconciliation between layers.

## Extending the Project
- Add pipeline orchestration (e.g., Azure Data Factory, Synapse pipelines, or Airflow) and version the pipeline definitions under `scripts/` or `orchestration/`.
- Document lineage and SLAs in `docs/`, including data contracts for upstream sources.
- Include performance tuning examples (indexes, partitioning, columnstore) on large fact tables.
- Contribute sample dashboards or query notebooks demonstrating Gold-layer analytics.

## Notes
- This repository currently includes placeholders for datasets, documentation, and tests—fill them with artifacts that match your domain.
- Always keep backups before rerunning the initialization script, as it drops the existing `DataWarehouse` database.
