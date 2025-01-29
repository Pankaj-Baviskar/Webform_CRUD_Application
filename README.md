# ASP.NET WebForms CRUD Application

This project is a simple ASP.NET WebForms application that enables CRUD (Create, Read, Update, Delete) operations on a database table named `Widget`. The application follows structured specifications to ensure efficient functionality.

## 📌 Features
- Displays a list of `Widget` records on the landing page.
- Provides options to create, update, and delete records.
- Allows CRUD operations through a modal, inline editing, or a separate page.
- Utilizes Microsoft SQL Server stored procedures for database interactions.
- Includes basic form validation and error handling.
- Updates the list dynamically after database changes.
- Designed for desktop browsers; mobile responsiveness is not a requirement.

## 🛠 Database Setup
The application relies on a SQL Server database named `DotNetDevSample`. The `Widget` table is structured as follows:

```sql
CREATE TABLE dbo.Widget (
    WidgetID INT IDENTITY(1,1) NOT NULL,
    InventoryCode NVARCHAR(50) NOT NULL,
    Description NVARCHAR(MAX) NULL,
    QuantityOnHand INT NOT NULL,
    ReorderQuantity INT NULL
);
```

### Stored Procedures
**Fetch all widgets:**
```sql
ALTER PROCEDURE dbo.sp_GetWidgetList
AS
BEGIN 
    SELECT WidgetID, InventoryCode, Description, QuantityOnHand, ReorderQuantity FROM dbo.Widget;
END
```

**Insert a new widget:**
```sql
ALTER PROCEDURE dbo.sp_SaveWidget
    @InventoryCode NVARCHAR(50),
    @Description NVARCHAR(MAX),
    @QuantityOnHand INT,
    @ReorderQuantity INT
AS
BEGIN
    INSERT INTO dbo.Widget (InventoryCode, Description, QuantityOnHand, ReorderQuantity)
    VALUES (@InventoryCode, @Description, @QuantityOnHand, @ReorderQuantity);
END
```

**Update an existing widget:**
```sql
CREATE PROCEDURE dbo.sp_UpdateWidget
    @WidgetID INT,
    @InventoryCode NVARCHAR(50),
    @Description NVARCHAR(MAX),
    @QuantityOnHand INT,
    @ReorderQuantity INT
AS
BEGIN
    UPDATE dbo.Widget
    SET InventoryCode = @InventoryCode,
        Description = @Description,
        QuantityOnHand = @QuantityOnHand,
        ReorderQuantity = @ReorderQuantity
    WHERE WidgetID = @WidgetID;
END
```

**Delete a widget:**
```sql
CREATE PROCEDURE dbo.sp_DeleteWidget
    @WidgetID INT
AS
BEGIN
    DELETE FROM dbo.Widget WHERE WidgetID = @WidgetID;
END
```

## 🚀 Getting Started
Follow these steps to set up and run the application locally:

1. Install **.NET Framework** and **ASP.NET WebForms**.
2. Install **Microsoft SQL Server** and **SQL Server Management Studio (SSMS)**.
3. Clone this repository.
4. Open the project in **Visual Studio** or **JetBrains Rider**.
5. In SSMS, create a new database named `DotNetDevSample`.
6. Run the provided SQL scripts to create the `Widget` table and stored procedures.
7. Update the `web.config` file with your SQL Server connection string.
8. Build and run the project.
9. Open the application in your browser and start performing CRUD operations.

## 📂 Project Structure

```
📦 Webform_CRUD_Application
 ┣ 📂 App_Code          # Business logic and data access
 ┣ 📂 App_Data          # Contains SQL database files (if applicable)
 ┣ 📂 Scripts           # JavaScript files
 ┣ 📂 Styles            # CSS files
 ┣ 📜 Default.aspx      # Main landing page with widget list
 ┣ 📜 InsertUpdateWidget.aspx  # Form for adding/updating widgets
 ┣ 📜 Web.config        # Configuration file (database connection, etc.)
```

## 🛠 Technology Stack
- **ASP.NET WebForms** for building the application.
- **C#** for server-side logic.
- **ADO.NET** for database communication.
- **Microsoft SQL Server** for data storage.
- **HTML, CSS, JavaScript** for front-end.

## 📦 Deployment Steps
1. Publish the application from **Visual Studio/Rider**.
2. Deploy the published files to your web server.
3. Configure the database connection on the server.
4. Set up IIS (Internet Information Services) or a hosting environment to run the WebForms app.
5. Access the application via the provided URL.

## 📌 Summary
This ASP.NET WebForms application offers a structured approach to managing `Widget` records with a clean UI, stored procedure-based database operations, and basic validation. Feel free to modify and extend the application based on your needs! 🎯
