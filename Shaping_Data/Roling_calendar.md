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
