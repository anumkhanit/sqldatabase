<h1>🗄️ Deploying SQL Database in Azure</h1>  
<p>A hands-on lab using Microsoft Azure to create and configure a cloud-based SQL Database. This is part one of a multi-part series on working with Azure SQL.</p>  

<h1>🧠 Overview</h1>  
<p>In this guide, you’ll deploy a fully managed SQL Database in Azure. You’ll create a resource group, configure a logical SQL server, set up a database, configure networking/firewall rules, and test connectivity from a client machine.</p>  

<h2>Environments and Technologies to use</h2>

- Microsoft Azure (Portal + CLI optional)
- SQL Server Management Studio (SSMS) or Azure Data Studio
- Azure CLI (optional, for automation)

<h2>Operating Systems to use</h2>

- macOS Sonoma (if you own MacBook Air M1 or M2; version doesn’t matter)
- Windows 10 or Windows 11 Home/Pro (if you own either of them)

-----

## 🔧 Part 1: Create a Resource Group

1.	Go to Azure Portal
2.	In the left menu, click Resource Groups > Create
3.	Set:
    - Name: `SQL-LaB`
    - Region: Closest to your location (e.g., East US)
5.	Click Review + Create > Create

***📌 Note: Always organize resources inside groups—it makes cleanup and management easier.***

-----

## 🌐 Part 2: Create a Logical SQL Server

1.	In the Azure search bar, type SQL Server > Create
2.	Fill in:
     - Name: `sqllab-server`
     - Region: Same as your resource group
     - Admin login: `labadmin`
     - Password: `SQLlab123!`
     - Choose resource group: `SQL-Lab`
3.	Click Review + Create > Create

***📌 Note: This “server” is logical, not physical—it hosts your SQL databases.***

-----

## 🗄️ Part 3: Create the SQL Database

1.	In the Azure Portal, search for SQL Databases > Create
2.	Fill in:
   - Database name: `DemoSQLDB`
   - Server: Select `sqllab-server`
   - Compute + Storage: Choose Basic (good for labs/testing)
   - Networking: Keep defaults for now
3.	Click Review + Create > Create

***📌 Note: Start small with compute/storage—you can scale up later.***

-----

## 🔒 Part 4: Configure Firewall & Networking

1.	Go to `SQL-Lab` > `DemoSQLDB` > `Networking`
2.	Under Firewall rules:
    - Click + Add client IP (this adds your computer’s current IP)
    - Save changes
3.	Ensure “Allow Azure services to access server” is ON

***📌 Note: If you switch networks (home → coffee shop), you’ll need to update firewall rules.***

-----

## 🖥️ Part 5: Connect via SSMS or Azure Data Studio

1.	Open SQL Server Management Studio (SSMS) or Azure Data Studio
2.	Server name: `sqllab-server.database.windows.net`
3.	Authentication: SQL Server Authentication
    - Login: `labadmin`
    - Password: `SQLlab123!`
4.	Click Connect

***✅ If successful, you’re connected to your cloud SQL Database.***

-----

## 🧪 Part 6: Run a Test Query at SQL

`CREATE TABLE Products (
    ProductID INT PRIMARY KEY IDENTITY,
    Name NVARCHAR(100),
    Price DECIMAL(10,2)`
`);`

`INSERT INTO Products (Name, Price) VALUES
('Azure Coffee Mug', 9.99),
('Cloud Hoodie', 29.95);`

`SELECT * FROM Products;`

***📌 Note: You’ve just created and queried your first Azure-hosted table!***

-----

## 💻 Part 7 (Optional - Use Bash): Deploy via Azure CLI

# Create a resource group
`az group create --name SQL-Lab --location eastus`

# Create a logical SQL server
`az sql server create \
    --name sqllab-server \
    --resource-group SQL-Lab \
    --location eastus \
    --admin-user labadmin \
    --admin-password SQLlab123!`

# Create the SQL database
`az sql db create \
    --resource-group SQL-Lab \
    --server sqllab-server \
    --name DemoSQLDB \
    --service-objective Basic`

***📌 Note: Azure CLI is great for automation and repeatable deployments.***

-----

## ✅ Conclusion

You’ve successfully:

- Created a resource group and logical SQL server
- Deployed a cloud-based SQL Database
- Configured firewall rules for client access
- Connected via SSMS/Azure Data Studio
- Created and queried your first table

## 🧠 Want to Learn More?

- [Azure SQL Database Docs](https://learn.microsoft.com/en-us/azure/azure-sql/database/?view=azuresql)

- [Azure CLI SQL Commands](https://learn.microsoft.com/en-us/cli/azure/sql?view=azure-cli-latest)

- [Azure Data Studio](https://learn.microsoft.com/en-us/azure-data-studio/)
