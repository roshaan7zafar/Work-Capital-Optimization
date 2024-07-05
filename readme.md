## MS SQL Server Database Set Instructions on AWS RDS

Amazon Web Services (AWS) provides a fully managed Relational Database Service (RDS) that allows you to easily set up and manage MS SQL Server databases in the cloud. In this section, we will walk you through the steps to create an MS SQL Server database on AWS RDS, both using Excel files and .bak files through Amazon S3.

Step 1: Download and Install SQL Server Management Studio (SSMS)
Before setting up the database, you need to have SQL Server Management Studio (SSMS) installed on your local machine. SSMS is a powerful tool for managing and querying SQL Server databases. You can download the latest version of SSMS from the Microsoft website: Download SQL Server Management Studio (SSMS). https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16


Step 2: Install Required Drivers
To connect to the SQL Server database on AWS RDS, you may need to install the necessary drivers on your local machine. 

Microsoft Access Database Engine: If you encounter the error "The 'Microsoft.ACE.OLEDB.16.0' provider is not registered on the local machine" while working with Excel files, you can download and install the Microsoft Access Database Engine from the Microsoft website: Download Microsoft Access Database Engine.

SQL Server Native Client: Install the SQL Server Native Client, which provides connectivity to SQL Server databases. You can download it from the Microsoft website: Download SQL Server Native Client.

ODBC Driver for SQL Server: If you plan to use ODBC to connect to the SQL Server database, you can download the ODBC Driver for SQL Server from the Microsoft website: Download ODBC Driver for SQL Server.

Step 3: Create an MS SQL Server Database on AWS RDS
Sign in to AWS Console: Log in to your AWS account and navigate to the AWS Management Console.

Open RDS Dashboard: Go to the RDS service and open the RDS dashboard.

Launch DB Instance: Click on the "Create Database" button to launch a new DB instance.

Select Engine: Choose "SQL Server" as the database engine.

Choose Use Case: Select the appropriate use case based on your requirements.

Specify DB Details: Provide the necessary details such as DB instance identifier, username, password, and other configuration settings.

Configure Advanced Settings: Customize advanced settings like VPC, security groups, backup retention period, etc.

Create Database: Review your settings and click on "Create Database" to initiate the database creation process.


Step 4: Connect to the MS SQL Server Database


Once the database is created, you can connect to it using SQL Server Management Studio or any other compatible client tool. To do this, you'll need the endpoint and credentials (username and password) you provided during the RDS instance creation.

Obtain Endpoint: In the RDS dashboard, locate your DB instance and note down its endpoint.

Open SSMS: Launch SQL Server Management Studio.

Connect to Database: In SSMS, click on "Connect" and enter the following details:

Server name: Provide the RDS endpoint.
Authentication: Choose "SQL Server Authentication."
Username and Password: Enter the credentials you specified during database creation.
Connect: Click on "Connect" to establish the connection to your MS SQL Server database on AWS RDS.


## Excel File


To upload an Excel file to tables in SQL Server Management Studio (SSMS) using the graphical user interface (GUI), you can follow these steps:
1. Launch SQL Server Management Studio and connect to the SQL Server instance where you want to upload the Excel file.
2. Expand the database node where you want to create the table and right-click on the "Tables" folder. Select "Tasks" and then "Import Data..." from the context menu. This will open the SQL Server Import and Export Wizard.
3. In the wizard, select the "Microsoft Excel" data source as the data source and specify the path to your Excel file.
4. Choose the appropriate Excel version and worksheet from the Excel source. You can preview the data by clicking the "Preview" button to ensure it is correct.
5. Click the "Next" button to proceed to the "Destination" screen. Select the destination database and table where you want to upload the data. If the table does not exist, you can choose to create a new table.
6. Click the "Edit Mappings" button to review and adjust the column mappings between the source and destination. You can modify the data types and other properties if necessary.
7. Once you have reviewed the mappings, click the "Next" button to proceed to the "Specify Table Copy or Query" screen. Here, you can choose to copy data to a new table or append it to an existing table.
8. Review the summary screen and click the "Finish" button to start the import process.
9. The import process will begin, and you can monitor its progress in the wizard. Once the import is complete, you will see a completion screen with the import summary.
10. Finally, you can verify the data by querying the table in SQL Server Management Studio.
By following these steps, you should be able to upload an Excel file to tables in SQL Server Management Studio using the GUI.


### .BAK File

To restore a .bak file from Amazon S3 to an SQL Server database, you can follow these steps:

Upload .bak File to S3: Using the AWS Management Console, navigate to the S3 service and upload the .bak file to a specified S3 bucket.

Open SQL Server Management Studio (SSMS): Launch SSMS on your local machine.

Connect to SQL Server: Connect to the SQL Server instance where you want to restore the .bak file. You can do this by providing the server name, authentication details, and login credentials.

Open Query Window: In SSMS, open a new query window to execute T-SQL commands.

Restore Database: Use the RESTORE DATABASE statement to restore the .bak file into a new or existing database. For example:

```
exec msdb.dbo.rds_restore_database
	@restore_db_name='wco-db1',
	@s3_arn_to_restore_from='arn:aws:s3:::wco-bucket/wcoDB.bak';

    
exec msdb.dbo.rds_task_status @db_name='wco-db1';


```


If you face error while uploading excel -
https://answers.microsoft.com/en-us/msoffice/forum/all/the-microsoftaceoledb160-provider-is-not/45dd60f3-69f5-4e9c-ba8d-2b2bcc4bc78c

sql server native client - https://www.microsoft.com/en-us/download/details.aspx?id=50402

odbc driver for sql server - https://learn.microsoft.com/en-us/sql/connect/odbc/download-odbc-driver-for-sql-server?view=sql-server-ver16
