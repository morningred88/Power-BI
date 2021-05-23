# The Power BI Query Editor

## Table name
On the right hand side of Query Editor, we've got Properties pane, the important thing to call out here is table name. It's really important to be strategic and clear with your table names right off the bat, because it can be pretty big headache to change them later on, especially if you've already reference them in multiple calculated fields and measures. So rule of thumb, **be strategic and careful about your table names from step one**. 



## Applied Steps

This is really, really powerful because what is happening here is that every time you make a change to your data, every time you apply some sort of shaping or transformation operator, Power BI will record an applied step using that M code and add it to the list. And what that means is that every time this connection is refreshed, Power BI will run through that same set of steps to shape and transform your data. That is a great way to automate things like data cleansing and ETL processes. 

