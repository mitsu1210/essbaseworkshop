# Lab 14: Essbase and ADW

## Introduction


### Objectives



### Required Artifacts


Estimated time to complete this lab is three hours.

### Additional Resources


## Part 1 - Provisioning an ADW Instance

## Part 2 - Uploading data file to ADW

## Part 3 - Create a Connection and Datasource for Oracle Autonomous Data Warehouse

### Define a connection and Datasource between Essbase and Autonomous Data Warehouse.

1.	In Essbase, on the Sources page, click Connections.
From the Actions menu to the right of an application name, launch the inspector and click Sources. (Screenshot required )
2.	Click Create Connection and select Oracle Database.
3.	Select Autonomous using the toggle switch.
4.	Enter a connection name and a service name.
5.	Drag and drop a wallet file, or click to upload.
Obtain a wallet file by selecting Download Client Credentials (Wallet) from your Autonomous Data Warehouse Administration page in Oracle Cloud Infrastructure.
6.	Enter your Autonomous Data Warehouse username, password, and optionally, a description.
7.	Click Test to validate the connection, and if successful, click Create.
8.	Verify that the connection was created successfully and appears in the list of connections. Next, you will create a Datasource for the Autonomous Data Warehouse connection.
9.	Click Datasources, and click Create Datasource.
10.	From the Connection drop-down box, select the name of the connection you just created; for example, EssbaseADW. For application-level Datasources, select the application-level connection name, in the format appName.connectionName.
11.	Provide a name for the Datasource; for example, ADW_DS.
12.	Optionally enter a description of the Datasource; for example, Autonomous Data Warehouse Datasource.
13.	In the Query field, provide the appropriate SQL query that selects the Autonomous Data Warehouse data you want to make available in this Datasource.
14.	Click Next. If the SQL statement was correct to query an Autonomous Data Warehouse area, you should see the queried columns populated.
15.	Change any additional source-specific parameters, if applicable, and click Next.
16.	Review the preview panel. You should see the results of the SQL query fetching columns of data from Autonomous Data Warehouse.
17.	If the preview looks correct, click Create to finish creating the Datasource.

## Part 4 - Build Dimensions Using SQL with ADW

1.	We will delete some members from Sample Basic, and then create a load rule to rebuild the Market dimension from the ADW table.
2.	In the Essbase web interface, on the Applications page, expand the Sample application, and select the cube, Basic.
3.	From the Actions menu to the right of Basic, select Outline.
4.	Click the Market dimension, and then click member East.
5.	Click Edit to lock the outline for editing.
6.	Delete some of the states from the East market. For example, delete Connecticut, New Hampshire, and Massachusetts.
7.	Click Save, and then verify that East now contains only the states Florida and New York.
Next, you will create dimension build rules and repopulate the Market dimension, from the SQL table, with the states you have removed.
8.	Close the Outline browser tab.
9.	On the Applications page, from the Actions menu to the right of Basic, launch the inspector, click Scripts, then choose the Rules tab.
10.	Click Create > Dimension Build (Regular) to begin defining new dimension build rules.
11.	In the Name field, enter the name of the rules file as MarketSQLDimbuild. Leave the other options as-is, and click Proceed.
12.	Click the Dimensions button.
13.	Click the field containing the text Select existing dimension, select Market, and click Add, then OK.
14.	On the New Rule - MarketSQLDimbuild page, click the Dimension drop-down field and select Market.
15.	Click the Type drop-down field and select Generation. Increment the generation number to 2.
16.	Click the Generation Name field and type REGION.
The Market dimension is generation 1, and you added a child named Region.
17.	Click Create > Regular to create a second dimension build rule field.
18.	Name the field STATE and associate it with dimension Market, at generation 3.
19.	Click the Source button to begin associating a data source with the dimension build rules.
20.	In the General tab, enter the valid connection string.
a.	For Oracle Call Interface connections: In the Name field of the General group, enter the valid OCI connection string.
b.	For DSN-less connections, such as Oracle DB, Microsoft SQL Server, and DB2: You must leave the Name field of the General group empty. Instead, enter the connection string in the Server field of the SQL/Datasource Properties group. The format is oracle://host:port/sid for and Oracle database.
21.	In Oracle SQL Developer (or your alternate SQL tool of choice), write and test a SELECT statement selecting some columns from the table SAMPLE_BASIC_TABLE: Select distinct market,statename from SAMPLE_BASIC_TABLE
22.	If the SQL query is valid, it should return the requested table columns, Market and Statename, from the database to which your SQL tool is connected:
23.	Copy the SELECT statement to your clipboard. The results of this query are the dimensions you will load into the Sample Basic cube.
24.	Back in the Edit Source dialog for your dimension build rule, paste the SQL statement into the Query field of the SQL/Datasource Properties group.
25.	Click OK,, then Verify, Save and Close. to save and close the MarketSQLDimbuild rule.
26.	Refresh the list of rules in the Scripts list to ensure that MarketSQLDimbuild has been added to the list of rule files for the cube Sample Basic.
27.	Click Close.
Next, you will use this rule file to load the members back into the Market dimension.
28.	Click Jobs, and click New Job > Build Dimension.
29.	Enter Sample as the application name, and Basic as the database name.
30.	For the script name, select the name of the dimension build rule file you created, MarketSQLDimbuild.
31.	Select SQL as the load type.
32.	Leave Connection blank, unless you already have a saved SQL connection you wish to use.
33.	Enter the user name and password of one of your SQL database schema users.
34.	Leave Data File blank.
35.	From the Restructure Options drop-down list, select Preserve All Data.
36.	Click OK to begin the job.
The dimension build begins. Click the Refresh symbol to watch the status, and when it completes, click Job Details from the Actions menu.
37.	Inspect the outline to verify that your dimensions were built (verify that Connecticut, New Hampshire, and Massachusetts exist as children under East).

## Part 5 - Load ADW Data to Essbase Using SQL

This task flow demonstrates how to clear data from a cube, create data load rules, load data (using SQL) from an RDBMS server, and verify in Smart View that the data was loaded.
Before beginning this task flow, complete prerequisites and obtain a valid connection string. See Build Dimensions and Load Data Using SQL for details.
1.	After building the dimensions, you will clear data from the cube, and then load the data again from a table. In Essbase, click Jobs, and click New Job.
2.	Select Clear Data as the job type. Select application Sample and database Basic, and click OK.
3.	Click OK to confirm that you want to clear data. The job begins. Click the Refresh symbol to watch the status, and when it completes, click Job Details from the Actions menu.
4.	Connect to the Sample Basic cube from Smart View, and do an ad hoc analysis.
5.	Notice that data was cleared. For example:
Keep the worksheet open. Next, you will create load rules that use SQL to repopulate the Sales data from the table.
6.	On the Applications page, expand the Sample application, and select the cube, Basic.
7.	From the Actions menu to the right of Basic, launch the inspector, click Scripts, then choose the Rules tab.
8.	Click Create > Data Load to begin defining new load rules.
9.	In the Name field, enter the name of the rule file as SalesSQLDataload.
10.	In the Data Dimension drop-down box, select the Measures dimension.
11.	Leave the other options as-is, and click Proceed.
12.	In Oracle SQL Developer (or your alternate SQL tool of choice), write and test a SELECT statement selecting some columns from the table SAMPLE_BASIC_TABLE: Select Product,Year,Scenario,Statename,Sales from SAMPLE_BASIC_TABLE
13.	Ensure that the SQL query is valid and returns a result in your SQL tool. If the SQL query is valid, it should return the requested table columns, PRODUCT, YEAR, SCENARIO, STATENAME, and SALES, from the database to which your SQL tool is connected:
14.	Copy the SQL query to a text file or your clipboard. You will need to use this in an upcoming step. The results of this query are the data you will load into the Sample Basic cube.
15.	Note the order of dimensions in your SQL query. The dimensions of the load rule fields must appear in the same order. This means that when you add fields, you should first add the last dimension listed in the SQL query (Sales). Each time you add a new field, it appears in front of the previous one, so when you are finished adding all fields, the dimensional order will match that of the SQL query.
16.	In Essbase, in the New Rule browser tab for your SalesSQLDataload rule, select Sales from the Select drop-down box.
17.	Click Create > Regular to create a second load rule field. From the Select drop-down box, select Market (which maps to Statename in your SQL query).
18.	Click Create > Regular to continue adding fields, in this order: Scenario, Year, and Product.
Your load rule fields should now be arranged like this:
19.	Click the Source button to begin associating a data source with the load rules.
20.	In the General tab, enter the valid connection string.
a.	For Oracle Call Interface (OCI) connections: In the Name field of the General group, enter the valid connection string.
b.	For DSN-less connections, such as Oracle Database, Microsoft SQL Server, and DB2: You must leave the Name field of the General group empty. Instead, enter the connection string in the Server field of the SQL/Datasource Properties group.
21.	Click OK.
22.	Verify, save, and close the SalesSQLDataload rule.
23.	Refresh the list of rules in the Scripts list to ensure that SalesSQLDataload has been added to the list of rule files for the cube Sample Basic, and then close the database inspector.
Next, you will load the data from Jobs.
24.	Click Jobs, and click New Job > Load Data.
25.	Enter Sample as the application name, and Basic as the database name.
26.	For the script name, select the name of the dimension build rule file you created, SalesSQLDataload.
27.	Select SQL as the load type.
28.	Leave Connection blank, unless you already have a saved SQL connection you wish to use.
29.	Enter the user name and password of one of your SQL database schema users.
30.	Leave Data File blank.
31.	Click OK to begin the job.
The data load begins. Click the Refresh symbol to watch the status, and when it completes, click Job Details from the Actions menu.
32.	Go back to the worksheet in Smart View, and refresh it to verify that the data was loaded from the table.
