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

### Other functions in Date tool

**Name of Month:** January, February ...December

**Start of Year:** 1/1/2021, 1/1/2021

**Year:** 2020, 2021

# Adding a rolling calendar

## Create a blank query

Get data > blank query, it will take you straight to the Query Editor, with the name Query 1, change the query name to Rolling_Calendar

**Step1: Add start date**

Inside the formular bar:

```
f(x) = #date (2021,11,1)
```

press enter, basically just create a single value

**Note:** date should be in lower case

**Step 2: Get the list of the dates**

Click f(x) button, 

```
List.Dates(Source, Number.From(DateTime.LocalNow())- Number.From(Source), #duration(1,0,0,0))
```

Press enter, it will create a whole list of dates starting from 11/1/2021, and end with the current date. If we will refresh this query a week from now, that end date will extend 7 more days. It is dynamic rolling of dates. 

**Step 3: Convert list to table**

Click List Tools on the top > To Table, no delimiter

**Step 4: Format the name of the column**

Format as a date instead of text, by left click the data type on the column header, select Date, then change column name to Date
