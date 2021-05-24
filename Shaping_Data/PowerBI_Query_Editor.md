# The Power BI Query Editor

## Table name
On the right hand side of Query Editor, we've got Properties pane, the important thing to call out here is table name. It's really important to be strategic and clear with your table names right off the bat, because it can be pretty big headache to change them later on, especially if you've already reference them in multiple calculated fields and measures. So rule of thumb, **be strategic and careful about your table names from step one**. 



## Applied Steps

This is really, really powerful because what is happening here is that every time you make a change to your data, every time you apply some sort of shaping or transformation operator, Power BI will record an applied step using that M code and add it to the list. And what that means is that every time this connection is refreshed, Power BI will run through that same set of steps to shape and transform your data. That is a great way to automate things like data cleansing and ETL processes. 



## Query editing tools

3 primary tabs/Categories

* Home tab: including general settings, data source setting, parameters, table properties, etc

* Transform tab: including tools to modify existing columns (splitting/grouping, transposing, extracting text, etc)
* Add column tab: create new columns in your table. And you can define those new columns based on things like conditional rules or text operations, calculations, data operator, etc.



## Upload a csv file to query editor

Get data > Text/CSV file> select the CSV file in the computer. As soon as you select file, you will see the preview window. This has a couple of options worth paying attention to:

* File origin
* Delimiter
* Data type detection: PowerBi takes a sneak peek and detect the data type. You can also select **Do not detect data types**, so you can manually add data types in the query editor.  By default, PowerBI automatically detect the data types based on the first 200 rows. 

Then click **Transform Data** to land on the query editor page. You can bypass the query editor by clicking **Load** button directly to load the table to the workbook. But launching power editor is a great way to make sure things look good. 

## 2 Required Steps when you connect to data or upload a table to query editor

* Update table name
* Scroll through the column headers to make the data types and column headers look good. 

## Format column to proper case 

**Goal: We want to change the proper case for AW_Customers_Lookup query**

Upload AdventureWorks_Customers.csv file to Query Editor

Hold shift key, select Prefix, FirstName, LastName three columns> click transform Tab> Format> Capitalize Each Word

## Merge columns

**Goal: We want to add full name to AW_Customers_Lookup query**

Hold shift key, select Prefix, FirstName, LastName three columns> click Add Column Tab > Merge columns > Seperator: Space; New column name: FullName.

Then rename the applied step from default Inserted Merge Column to **Inserted FullName Column**

