# MSSQL-to-PostgreSQL

MSSQL-to-PostgreSQL is a migration tool designed to help users move databases from Microsoft SQL Server or Azure SQL to PostgreSQL (on-premises or managed/cloud). It supports schema, data, indexes, constraints, sequences, and views (with certain limitations). The tool can either push directly to a PostgreSQL server or export migration scripts. It provides a wizard interface plus command-line options for automation.

**Key Features**

- Schema and Data: Migration	Migrates tables, data, indexes, constraints, and sequences from SQL Server / Azure SQL into PostgreSQL. 
- Views Migration: Can migrate many views—approximately 90% of SQL Server view syntax is supported. 
- Safe / Custom Type Mapping: Provides safe mappings from MSSQL types to PostgreSQL, such as datetime2(n) → timestamp(n), varbinary(max) → bytea, etc. Allows customizing the mapping per column. 
- Migration Modes: Multiple modes of operation: direct server-to-server migration; export to SQL script file (for use when direct connection isn’t available). 
- Merge / Synchronize Options: When the target PostgreSQL database already exists, you can choose to overwrite, merge, or synchronize the data. 
- Performance: Fast migration engine (nominally 10MB+/sec on modern hardware) and optimized reading/writing algorithms. 
- Spatial Data: Support for spatial data types during migration. 
- SSL / Security: Supports SSL connections to PostgreSQL, which can be critical when migrating to cloud or secured environments. 
- Command-line / Automation / Profiles: Has CLI support and can save “profiles” of migration settings so you can re-use or schedule migrations. Also supports “Quick Launch” mode using saved profiles. 
- Customization: Users can fine-tune what gets migrated - select specific tables or views, skip or include indexes, customize default values, column names, schema names, etc. 

**Scope of Use**

This product is suited to the following contexts and constraints:

- Source databases: Microsoft SQL Server (on prem) or Azure SQL. It works with all versions of SQL Server. 
- Target platforms: PostgreSQL v9.0 and later (on-premises or cloud), including managed services (e.g. Azure, Amazon RDS), and also Heroku. 
- Operating systems: Windows (various versions, including Windows Server versions). A Linux environment is possible only via WINE. 
- Privileges required: The user account used for migration must have sufficient rights in SQL Server (source) and PostgreSQL (target) to read schema + data and write the converted schema/data. 
- Usage modes:
-- One-time migration (schema + full data)
-- Partial migrations (selected tables, filtered data via SELECT queries)
-- Script export (generate SQL script that can be applied later)
-- Merge / synchronize into existing PostgreSQL databases
- Not supported components: Stored procedures, functions and triggers are not migrated by this tool (those require a separate “Code Converter” add-on). Foreign keys and views in the trial version are limited. 

**Advantages**

Here are the main benefits of using this product vs doing everything manually or using less specialized tools.

- Reduced Migration Effort and Risk: The tool minimizes manual work by converting schema, constraints, sequences, indexes, and data automatically; less risk of mistakes in type mapping or missing objects.
- Flexible Target Options: You can migrate directly, or generate SQL script files to apply later, giving flexibility in disconnected or controlled environments.
- Performance Optimized: Bulk-migrations (especially using COPY in PostgreSQL mode) accelerate data transfer; the ability to skip or batch objects (tables/views) helps manage large databases.
- Merge/Synchronization Capability: When the target database already has data, the ability to “merge” or “synchronize” avoids full overwrite and reduces downtime or data loss.
- Customization and Control: Fine-grained control over what objects are migrated (tables, views), ability to customize data type mapping, rename columns if needed, and filter data via SELECT queries.
- Support for Spatial Data & Complex Types: Spatial data and other SQL Server-specific types are handled, so you don’t lose special-purpose data (e.g. geometry columns) during migration.
- Secure and Suitable for Cloud or Remote Targets: SSL support ensures secure connections. Working with targets in cloud DB services is possible.
- Automation Friendly: Profiles, CLI, and Quick Launch allow repeated use, habitual migration tasks, or scheduled migration/refresh operations.

**Possible Limitations / Considerations**

To have a balanced view, note some of the trade-offs or things to watch out for. MSSQL-to-PostgreSQL does not migrate stored procedures/functions/triggers — business logic in those must be ported manually or via a supplemental tool.
OS dependency — Windows is fully supported; Linux requires WINE which may bring its own limitations.

Dependency on privileges — you need sufficient permissions on both source/target; indirect restrictions (firewalls, network latency) can impact performance.
