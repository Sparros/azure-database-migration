# azure-database-migration985

This GitHub repository serves as documentation for setting up a Windows Virtual Machine (VM) to emulate the functions of a Windows server within a production environment. The VM acts as a secure and dedicated repository for the company's database, replicating an on-premise system.

## Project Milestones
### 1. Virtual Machine Setup
Set up a Windows Virtual Machine as the cornerstone of the production environment.
Configure network settings and firewall rules for secure operations.
Establish connection to the VM using the RDP protocol for efficient management.
### 2. Database Setup
Install SQL Server and SQL Server Management Studio (SSMS) on the VM.
Initiate a remote connection to the VM using Microsoft Remote Desktop and RDP protocol.
Create a production database by restoring the AdventureWorks database from the provided backup file.
### 3. Azure SQL Database Migration
#### 3.1 SQL Server Configuration
Create an Azure SQL Database to serve as the target for migrating your on-premise database.
Ensure that the associated SQL Server uses SQL login as the chosen authentication method.
Confirm that the SQL Server has the appropriate firewall rules, specifically with your IP address added to the firewall settings.
#### 3.2 Azure Data Studio Configuration
Install and configure Azure Data Studio on your production Windows VM.
Use Azure Data Studio to establish a connection to the existing on-premise database.
Establish a connection to the newly created Azure SQL Database. This connection serves as the conduit for schema and data migration between the two databases.
#### 3.3 Schema Migration
Install the SQL Server Schema Compare extension within Azure Data Studio.
Leverage this extension to compare and subsequently migrate the schema from the on-premise database to the Azure SQL Database.
#### 3.4 Data Migration
Install the Azure SQL Migration extension within Azure Data Studio.
Use this extension to facilitate the smooth transfer of data from your on-premise database to the Azure SQL Database, ensuring a successful and seamless data migration process.
### 4. Validation
To confirm the success of the database migration process:

Carry out a comprehensive validation by thoroughly inspecting the data, schema, and any configurations of the migrated database.
Ensure that the migration has been executed successfully and adheres to principles of data integrity.
