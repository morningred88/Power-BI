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

## Extract tools based on delimiters

**Goal: We need to extract the user name and domain name from the email address in AW_Customers_Lookup query. **

User name is the text in email address before @

Domain name is the text in email address between @ and .com. Then change the domain name to proper case, and replace dash with space

* **Add UserName column extracted from email**

Select EmailAdress column > Add Column tab > Extract > Text Before Delimiter > Delimiter: @

Rename Inserted Text Before Delimiter column to UserName

* **Add Domain column extracted from email**

Select EmailAdress column > Add Column tab > Extract > Text Between Delimiters >Start Delimiter: @; End Delimiter: .com

Rename Inserted Text Before Delimiter column to **Domain**

* **change the domain name to proper case, and replace dash with space**

Select Domain column > Transform tab > format> Capitalized Each Word

Select Domain column > Transform tab > Replace Values> Value to Find: - ; Replace with: type space key

 ## Working with numerical values

### Statistics tools 

Statistics tools are **only** accessible from the Transform Tab in the Query Editor.

## Date & Time Tools

### Load source data

Get data> load AdventureWorks_Calendar csv file> Transform> 

We can add the calendar to track the sales by date, by week or by year

**Note:** If you want to work with Date tool, you need select the column having Date data type. 

### Add name of day

Monday, Tuesday...

Select Date column> Add Column > Date >Day > Name of Day

### Add start of week: First date of the week

Shows start date of the week 

Select Date column> Add Column > Date >Week > Start of Week

**Note:**

By default, Power Bi starts the week with Sunday

We can change it by updating the M code

f(x) = Table.AddColumn(#"Inserted Day Name", "Start of Week", each Date.StartOfWeek([Date]), type date)

We have two ways to change it, for example, we can change the week starts with Monday:

**Option 1: Add number 1 to Date**

f(x) = Table.AddColumn(#"Inserted Day Name", "Start of Week", each Date.StartOfWeek([Date],1), type date)

**Option 2: Add Day.Monday to Date**

f(x) = Table.AddColumn(#"Inserted Day Name", "Start of Week", each Date.StartOfWeek([Date], Day.Monday), type date)

Option 2 is more readable. 

### Latest

Latest returns a single value (latest day compared to today's date) from the selected date column. And it can only be accessible from the "Transform" tab.

### Other functions in Date tool

**Name of Month:** January, February ...December

**Start of Year:** 1/1/2021, 1/1/2021

**Year:** 2020, 2021

## Generating index & Conditional columns

### Add index column

Add index column to create a sequential list of unique values to identify each row. If a table no primary key, you can add index column as primary key. You can start the value from 0 or 1, or any custom number. 

### Add conditional columns

#### Data source

Load the csv file AdventureWorks_Sales_2017 from Raw data folder, then click Transform Data.

Change query name to AW_Sales_2017

#### Goal

We plan to add a new conditional column to record the quantity type

If column OrderQuantity equals 1, Then Output for the new column should be Single Item.

If column OrderQuantity is greater than 1, Then Output for the new column should be Multiple Items.

#### Add conditional column in Query Editor

Add Column> Conditional column

New column name: **QuantityType**

If column OrderQuantity equals 1, Then Output for the new column should be **SingleItem**.

Else If column OrderQuantity is greater than 1, Then Output for the new column should be **MultipleItems**.

Otherwise: **Other**

click ok to complete

## Grouping & Aggregating records

### Data source

AW_Sales_2017 query

using Transform> Group by tool

### Goal 1: Group by basic option

For AW_Sales_2017 query, we want to see how much the product quality has been sold for each unique ProductKey.

Select ProductKey coliumn > Transform tab> Group by tool>

Check **Basic**

Group by: **ProductKey**

New Column name: TotalQuantity

Operations: Sum

Column: OrderQuantity

Click OK. 

This collapse our data into a 2 column table with new aggregated quality field that we named it as TotalQuantity and unique list of product keys

### Goal 2: Group by Advanced option

For AW_Sales_2017 query, we want to see how much the product quality has been sold for every combination of ProductKey and cutomerkey.

Select ProductKey coliumn > Transform tab> Group by tool>

Check **Advanced**

Group by: **ProductKey**, **CustomerKey**

New Column name: TotalQuantity

Operations: Sum

Column: OrderQuantity

Click OK. 

This collapse our data into a 3 column table containing each unique combinations of ProductKey and CustomerKey.

**Notes:**

* The only difference between basic and advanced option in group by is: you can only group by one column for basic, which multiple columns for advanced. 
* Even group by function is under Transform tab, it add a new aggregation column. This function will create a new table instead of the original one. 



## Pivoting & Unpivoting data

### Definition

Pivoting: change rows to columns

Unpivoting: Change column to rows

### Data source

Add csv file Unpivot_Demo.csv from Raw Data folder to Power BI, click transform data

What we have here is that Unit Sales and Total Revenue, these 2 matrix  broken down by year

### Goal

Our goal is transform the current table in Unpivot_Demo.csv to a rectangular table: Each matrix as column, each observation as row. We want to transform it to a table that has three columns, Year, Unit Sales, Total Revenue, that give us the format we can take to the model and analyze.

### Table transformation by pivoting/unpivoting

* Add headers: Transform tab> Use First Row as Headers
* Select first column, Transform tab>Unpivot columns, select unpivot other columns. Now year column is correct, but we still need to pivot unit sales and Total Revenue to columns
* Select first column, select Pivot column, value column: value
* Rename column header from Attribute to Year

### Efficient way: Transpose

Transpose table operation rotates your table to 90 degrees, turning your rows into columns and columns into rows.

* Transform tab > Transpose, we are pretty much done, just need to remove the current header, and add  column header for the year column
* Use First Row as Headers
* Add Header for year column: Year

### Tips for Transpose & Unpivot:

1. **Delete promote header steps before you use Transpose.**

   Transpose is a table operation. It flips the whole tables. We must ensure table does not have headers. Otherwise, we would have lost a row of data, because Transpose flip rows to columns, the heading just tend to disappear. 

2. **We must have a Promoted Header step before unpivoting**

   When we use Unpivot, a section of the table is transposed. This is done by making all the headings of that section appear on a single column to be name **Attribute** by default, and everything under the headings now becomes a separate column to be named **Value** by default. 

**Reference:**

To Transpose or Unpivot? What you need to know about table structuring in Power Query

By ahmedoye

https://community.powerbi.com/t5/Community-Blog/To-Transpose-or-Unpivot-What-you-need-to-know-about-table/ba-p/1013559

## Merging Queries

### Definition

Merging queries allows you to join tables based on a common column, which adds column to an existing table.

### Merging options:

* Merge Queries: Merge to the existing table
* Merge Queries as new: Merge and create a new table

**Note:**

Just because we can merge tables, doesn't mean we should, because it will create a lot duplicative and redundant data, and will consume a lot of memory. We can avoid entirely by creating table relationships instead.  

**In general, it is better to keep tables separate and define relationships between them. **

## Appending Queries 

### Definition

Appending queries allow you to stack 2 or more tables that share the exact same column structure and data type. 

### Appending options:

* Append Queries: Append to the existing table
* Append Queries as new: Append and create a new table

### Merging queries vs Appending queries

Both merging and appending are similar by adding information to the existing table. 

But they are different, merging making table wider by adding more columns, and appending makes table taller by adding more rows.

### SQL Query equivalent

Merge = join

Append = union

### Appending queries with 3 tables

#### Data Source  and Goal:

Appending 3 tables AdventureWorks_Sales_2015.csv, AdventureWorks_Sales_2016.csv, and AdventureWorks_Sales_2017.csv, into 1 table. 

#### Method 1

We can import all 3 tables into PowerBi, then Home tab> Append Queries> Append Queries as new> Check Three or more tables> Add all 3 tables

**Disadvantage:**

We are required to keep all 3 tables in the query editor, because the new created appending table is dependent from the 3 sales tables. It looks messy. 

#### Method 2: Use the folder option

Create a new folder and put all 3 sales file in it, import folder into Power BI.

* Create a new folder under Raw Data folder, name it AW_Sales, drag the 3 sales table into it.
* Go to PowerBI report file, Get Data > more >folder > Connect, browse the folder path> The preview shows the 3 csv files and their attributes. The first column named Content is the actual data content from each table > Under Combine button, select Combine & Transform data > you can preview each table structure by selecting the file> Click OK > You can see the new query named AW_Sales has been added. The first column called Source is a newly added column that indicate the source file of the row of data. You can delete the column if the information is not needed.
* You can see a new folder called Transform file form AW_Sales, we need to keep the folder there but we don't need to edit or update it. 

**Advantage:**

The big advantages by adding foler is: **As you add new files, simply refresh the query and they will automatically append!**

## Configuring Power BI Data Source Setting

The Data Source Setting in the Query Editor allow you  to manage data connections and permissions. 

When you make connection to a local file, power Bi take a snapshot to the exactly file path to that exact file name. If anything changes to the file, or if you rename it or move it to a new location, that path won't automatically update, you will need to go to **Data Source Settings**, click change the source and browse to the current version. 

### Steps for Data source setting in Query Editor

* Rename the source file name for AW_Product_Lookup. Rename AdventureWorks_Products.csv to AdventureWorks_Products2.csv.

* Click Transform data to launch Power Editor, select AW_Product_Lookup query, click Home tab> Refresh Preview.  You will receive the error message below: 

  DataSource.Error: Could not find file 'C:\Users\xldu\local-repository\Power-BI\Raw_Data\AdventureWorks_Products.csv'.

* Click Home tab in Query editor > Data Source Setting> select the file path> click Change Source button> browse the current file location

* Test: Back to query editor, click Refresh Preview, the error is gone. 

## Configure Power BI Query refresh settings

By default, **all** queries in the model will refresh when you use the **Refresh** command from the Home Tab.

From the query editor, right click the query, uncheck **Include in report fresh** to exclude individual queries from the refresh.

**Pro Tip:**

Exclude queries that don't change often, like lookups or static data tables. 

### Query refresh setting for AdventureWorks_Report.pbix file

Home tab > Refresh, you can see all queries all refeshing:

- AW_Calendar_Lookup
- AW_Customers_Lookup
- AW_Product_Lookup
- Rolling_Calendar
- Unpivot_demo
- AW_Sales

Set the first 5 queries excluded from refresh, only leave AW_Sales.

Home tab > Refresh, now you can only see that AW_Sales is refreshing.

## New Resource

New data source can be added Home>Get Data.

But you can also add new data source in Query Editor.

In Query Editor, you can also add new data source. For example, you can add CSV file to Power BI by click Home > New Source > Text/CSV.
