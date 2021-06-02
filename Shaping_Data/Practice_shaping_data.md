# Practice: Connecting & Shaping Data with Power BI Desktop

#### Using your Adventure Works Power BI file, complete the following:



**1)** Create new queries to connect to the **AdventureWorks_Product_Categories** and **AdventureWorks_Product_Subcategories** files from the course resources:

- Name your queries **AW_Product_Category_Lookup** and **AW_Product_Subcategory_Lookup** 
- Confirm that headers have been promoted and that detected data types are correct 
- Disable the report refresh option for both connections



**2)** Make the following modifications to the **AW_Product_Lookup** query:

- Add a calculated column that extracts all characters before the dash ("-") in the **ProductSKU** column, named "**SKUType**"
- Update the **SKUType** calculation above to return all characters before *second* dash, instead of the first 
- Replace zeros (0) in the **ProductStyle** column with "*NA*"
- Update the **DiscountPrice** calculation to 15%, by multiplying the **ProductPrice** values by 0.85 (instead of 0.9) 

**3)** Using the Statistics tools in the Query Editor, confirm the following values *(06:04 mark)*:

- Average product cost (***$413.66***)
- Number of distinct product colors (***10***)
- Number of distinct customer names (***18,110***)
- Maximum annual customer income (***$170,000***)
- Count of order numbers (***56,046***)
- Count of distinct order numbers (***25,164***)

**4)** Make the following modifications to the **AW_Customer_Lookup** query:

- Add a new calculated column for the year of birth (named "**BirthYear**"), based on **BirthDate**
- Add a conditional column to categorize customer income (named "IncomeLevel"), based on the following criteria:
  - If **Annual****Income** >= $150,000, then **IncomeLevel** = "*Very High*"
  - If ***\*Annual\**\**Income\**** >= $100,000, then **IncomeLevel** = "*High*"
  - If ***\*Annual\**\**Income\**** >= $50,000, then **IncomeLevel** = "*Average*"
  - Otherwise **IncomeLevel** = "*Low*"

**5)** Apply all changes, and confirm that new tables and fields are accessible within both the **Data** and **Relationships** views (recommend saving a backup copy of the report (i.e. *"AdventureWorks_Report_Backup"*)







