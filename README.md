<a href="https://www.theta.co.nz/solutions/cyber-security/">
<img src="https://avatars0.githubusercontent.com/u/2897191?s=70&v=4" 
title="Theta Cybersecurity" alt="Theta Cybersecurity">
</a>

<!-- project title -->
<!-- first.last@theta.co.nz -->
<!-- development/test/production -->

# Power BI for Intermediates: part two

Power BI Training Material & Guides

<!---add link to the power BI pdf -->
[Power BI for Intermediates: part two](https://theta.co.nz/cyber) 

---
***1.2.1 Calculated Tables***

> DAX expression that creates a table with one column. 

    Calculated Table 1 =
    {"A", "B", "C"}
      
> Expression creates a calculated table using the table constructor and the DATE() function.

    Calculated Table 2 =
      {DATE(2020, 7, 22), DATE(2020, 7, 23), DATE(2020, 8, 2)}
      
> DAX expression of a table constructor; where you define rows of data using parenthes () where the values are seperated with a comma. 

    Calculated Table 3 =
    {
            ( "A", 1.5, DATE(2017, 1, 1), CURRENCY(199.99) ),       
            ( "B", 2.5, DATE(2017, 1, 2), CURRENCY(249.99) ),      
            ( "C", 3.5, DATE(2017, 1, 3), CURRENCY(299.99) )
        }

> DAX expression shows the following:
    
    Australian Customers Sales =
    SUMMARIZECOLUMNS (
      DimCustomer[CustomerKey]
      , FILTER(
			VALUES(DimGeography[EnglishCountryRegionName])
			, DimGeography[EnglishCountryRegionName] = "Australia")
        , "Customer Full Name", CONCATENATEX(DimCustomer, DimCustomer[FirstName] & " " & DimCustomer[LastName])
		, "Sales Amount", SUM(FactInternetSales[SalesAmount]) 
    )


---

***1.2.2 Calculated Columns***

> Create a calculated column.

    Full Name = CONCATENATE(DimCustomer[FirstName] & " ", DimCustomer[LastName])

---

***1.2.3 Measures***

> Create a Sales Amount measure in the FactInternetSales table.

    Sales Amount = SUM(FactInternetSales[SalesAmount])
    
---

***1.2.5 Time Intelligence***

> DAX expression calculating cumulative sum  of sales, Month-to-Date (MTD).

    Sales Amount MTD =
        TOTALMTD([Sales Amount], 'DimDate'[Date])

> DAX expression calculating cumulative sum  of sales, Year-to-Date (YTD).

    Sales Amount YTD = 
    TOTALYTD([Sales Amount], 'DimDate'[Date])
    
---

***1.2.5.3.1 Generating Date Table in Power Query***

> Generate a Date table using Power Query (M) language.
       
let
Source = List.Dates(#date(2010, 1, 1), Duration.Days(Duration.From(#date(2014, 12, 31) -
#date(2010, 1, 1))), #duration(1, 0, 0, 0) ),
#"Converted to Table" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
#"Renamed Columns" = Table.RenameColumns(#"Converted to Table",{{"Column1", "Date"}}),
#"Added Custom" = Table.AddColumn(#"Renamed Columns", "DateKey", each Text.Combine({Date.ToText([Date], "yyyy"), Date.ToText([Date], "MM"), Date.ToText([Date], "dd")})),
#"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Date", type date},
{"DateKey", Int64.Type}}),
#"Year Column Added" = Table.AddColumn(#"Changed Type", "Year", each Date.Year([Date])),
#"Quarter Column Added" = Table.AddColumn(#"Year Column Added", "Quarter", each "Qtr
"&Text.From(Date.QuarterOfYear([Date]))),
#"MonthOrder Column Added" = Table.AddColumn(#"Quarter Column Added", "MonthOrder",
each Date.ToText([Date], "MM")),
#"Short Month Column Added" = Table.AddColumn(#"MonthOrder Column Added", "Month
Short", each Date.ToText([Date], "MMM")),
#"Month Column Added" = Table.AddColumn(#"Short Month Column Added", "Month", each
Date.MonthName([Date])),
#"Changed Columns Type" = Table.TransformColumnTypes(#"Month Column Added",{{"Year",
Int64.Type}, {"MonthOrder", Int64.Type}})
in
#"Changed Columns Type"

---

***1.2.5.3.1 Generating Date Table in Power Query***

> Create a Date table using DAX.
        
    Date with DAX =
        ADDCOLUMNS(CALENDAR(DATE(2007,1,1), DATE(2020,12,31))
                , "DateKey", VALUE(FORMAT([Date], "YYYYMMDD"))
                , "Month", FORMAT([Date], "MMMM")
                , "Month Short", FORMAT([Date], "MMM")
                , "MonthOrder", FORMAT([Date], "MM") 
                , "Quarter", CONCATENATE("Qtr ", QUARTER([Date]))
                , "Year", YEAR([Date])
            )

---
[Theta](https://www.theta.co.nz/cyber)
