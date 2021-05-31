# Data view

We have several queries imported now. If you click data view, you see the  preview of all the queries. The format of a column in the query is that you can see when you put it in a table in a visual.

For example:
In AW_Calendar_Lookup table, Date column has the date format Thursday, June 8, 2017, which is 6/8/2017 in Query Editor. 

In Data view, you can see Table Tools tab and Column Tools tab if you have a table or column selected. 

## Column Tools

### Format data type in Column Tools tab

#### Format the column with Date data type to short date 

Go to AW_Calendar_Lookup table, select Date column > Table Tools tab > Confirm the data type as Date> Format, click down arrow, select the first one, short date. Now the value change to the format of 6/8/2017.

The same procedure for columns: Start of week, start of Month, Start of Year

Then in AW_Sales query, format OrderDate and StockDate also as short date.

#### Add $ Sign for currency

Go to AW_Product_Lookup query, select ProductCost column> Column Tools tab, confirm the data type as decimal number> Select $ sign under format, default is dollar sign. If you click down arrow beside dollar sign, you can select other currencies.

The same procedure for ProductPrice and DiscountPrice column.

## Data category

We can change data category 

Import from Raw_Data folder AdventureWorks_Territories.csv file to Query Editor> change query name to AW_Territories_Lookup > close & Load

Data view> select AW_Territories_Lookup> Select country column> Column tools tab, Data category> select Country

The same procedure for Continent column, select Continent. 

You can see the **globe icon** to the left of the fields, indicates these columns are categorized as geographical fields.

**Note:**

PowerBI will almost always recognized these fields properly by default automatically. If we have not gone through the steps above, just plug these countries and do a map visual, 99.9% of time will work exactly what you expect and you'll get accurate results. But as best practice, it really couldn't hurt to explicitly define what type of data category you are working with.



 





