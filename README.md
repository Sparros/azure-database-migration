# azure-database-migration985

This GitHub repository serves as documentation for setting up a Windows Virtual Machine (VM) to emulate the functions of a Windows server within a production environment. The VM acts as a secure and dedicated repository for the company's database, replicating an on-premise system.

The project unfolds through carefully planned milestones, each addressing crucial aspects of database migration, disaster recovery simulation, and data access control. Follow the step-by-step instructions to  transition from on-premise databases to Azure SQL, ensuring data integrity, security, and resilience.


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
  #### 4. Validation
  To confirm the success of the database migration process:

  Carry out a comprehensive validation by thoroughly inspecting the data, schema, and any configurations of the migrated database.
  Ensure that the migration has been executed successfully and adheres to principles of data integrity.


### 4. Database Development Environment
#### 4.1 Production Database Backup
Generate a full backup of the production database hosted on the Windows VM. This backup duplicates your database, providing a safety net in the event of unforeseen issues.
Store the resultant backup file in a designated location on your computer.
#### 4.2 Azure Blob Storage Configuration
Configure an Azure Blob Storage account to serve as a secure online repository for your database backups.
Upload the previously created database backup file to the Blob Storage container, adding an extra layer of backup protection through the presence of a redundant copy stored remotely.
#### 4.3 Development Environment Provisioning
Provision a new Windows VM mirroring the development setup to act as a controlled experimentation environment.
Install SQL Server on this VM to mimic the necessary database infrastructure.
Restore the database backup onto this new "sandbox" environment, allowing safe exploration and experimentation with new concepts while keeping the main production data unaffected.
#### 4.4 Automated Backup Solution for Development
On your development Windows VM, utilize SSMS to establish a Management Task that automates regular backups of your development database.
Configure a weekly backup schedule to ensure consistent protection for your evolving work and simplify recovery for your development environment if needed.

### 5. Disaster Recovery Simulation
In this phase, we simulate a scenario where critical data is deliberately removed from the production database to replicate a situation where data integrity is compromised. The documentation of this simulated data loss will serve as a blueprint for our recovery testing.
#### 5.1 Simulating Data Loss
To simulate data loss, we deliberately dropped the "Employee" table from the "AdventureWorks2022" database. The SQL command used for this operation is as follows:
```sql
USE AdventureWorks2022;
GO

DROP TABLE Employee;
```
#### 5.2 Recovery Testing
##### 5.2.1 Using Azure SQL Database Backup
Identify and select the appropriate backup point using the Azure portal or Azure Data Studio.
##### 5.2.2 Validation
After the restoration is complete, validate its success by examining the restored data through the connection in Azure Data Studio.

##### 5.2.3 Production Database Update
Since the restored database now functions as the production database, delete the database that suffered data loss in the Azure portal. Confirm that the restored database is functioning as expected before proceeding with the deletion.

#### 5.3 Confirming Simulation Success
After completing the simulation, confirm its success by examining the Azure SQL Database using the connection already established in Azure Data Studio.


### 6. Geo-Replication and Failover Testing
In this milestone, we configure geo-replication for the production database to enhance data protection by establishing a synchronized copy of the Azure SQL Database in a secondary region. Geo-replication provides strategic redundancy, ensuring continuous data availability and minimizing potential downtime during unforeseen disruptions.
#### 6.1 Setting Up Geo-Replication
Begin by setting up geo-replication for your production Azure SQL Database. This process involves creating a synchronized replica of your primary database. The replica resides on a separate SQL server located in a different geographical region from your primary database server. This geographical separation is crucial as it bolsters redundancy and resilience, minimizing shared risks.
#### 6.2 Failover Testing
##### 6.2.1 Planned Failover
1. Orchestrate a planned failover to the secondary region, simulating real-world challenges. This act transitions operations to the secondary copy.
2. Evaluate the availability and data consistency of the failover database. This step provides valuable insights into the failover mechanism and its impact on your data ecosystem.
##### 6.2.2 Failback
After evaluating the secondary region, perform a failback to the primary region. This demonstrates the cyclical nature of your failover strategy and ensures that operations can seamlessly return to the primary database when the secondary region is stable.
##### 6.3 Ensuring Data Resilience
Geo-replication, combined with failover testing, ensures that your data ecosystem remains resilient in the face of unforeseen disruptions. The synchronized copy in the secondary region acts as a safeguard against downtime, providing a seamless transition in the event of a primary region failure.


### 7. Integration with Microsoft Azure Active Directory
In this milestone, we integrate Microsoft Azure Active Directory with our Azure SQL Database setup, introducing a more organized way to manage access to our data.
#### 7.1 Setting Up Admin and Database Reader Accounts
##### 7.1.1 Enabling Azure Active Directory Authentication
Begin by enabling Microsoft Azure Active Directory (AAD) authentication for the SQL Server hosting your Azure SQL production database. This step integrates Microsoft Azure Active Directory as a trusted identity provider, allowing users to authenticate using their Microsoft Azure Active Directory credentials.
##### 7.1.2 Admin Account Creation
Choose a Microsoft Azure Active Directory admin with privileged permissions within your Azure SQL Database environment. This admin will have authority over user management and access control. Ensure that you can establish a connection to the production database using Microsoft Azure Active Directory credentials within Azure Data Studio.
#### 7.2 Database Reader User Provisioning
##### 7.2.1 Creating a DB Reader User in Azure Active Directory
Generate a new user account in Microsoft Azure Active Directory, which will serve as your DB Reader user. This user account will be assigned read-only access to the production database.
##### 7.2.2 Assigning db_datareader Role
In Azure Data Studio, ensure that you're connected to the production database using the Microsoft Azure Active Directory admin credentials. Proceed to assign the `db_datareader` role to the previously created DB Reader User. This role provides the user with read-only privileges.
##### 7.2.3 Testing Permissions
Reconnect to your production database using Azure Data Studio and the credentials of the new DB Reader Azure Active Directory user. Test out the permissions of the user to ensure the correct role has been assigned to this user. This step is crucial in verifying that the DB Reader user has the intended read-only privileges.
#### 7.3 Data Access Control
By integrating Microsoft Azure Active Directory, we have introduced a more organized approach to managing access to our data. The use of an admin account for overseeing the production database and dedicated DB Reader accounts with restricted read-only access ensures data accuracy and consistency in our production environment.




