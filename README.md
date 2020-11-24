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
[Power BI PDF](https://theta.co.nz/cyber) 

---
***1.2.1 Calculated Tables***

> DAX expression that creates a table with one column (Figure 13). 

    Calculated Table 1 =
      {“A”, “B”, “C”}
      
> Expression creates a calculated table using the table constructor and the DATE() function.

    Calculated Table 2 =
      {DATE(2020, 7, 22), DATE(2020, 7, 23), DATE(2020, 8, 2)}
      
> DAX expression of a table constructor; where you define rows of data using parenthes () where the values are seperated with a comma. 

    Calculated Table 3 =
    {
        ( “A”, 1.5, DATE(2017, 1, 1), CURRENCY(199.99) ),       
        ( “B”, 2.5, DATE(2017, 1, 2), CURRENCY(249.99) ),      
        ( “C”, 3.5, DATE(2017, 1, 3), CURRENCY(299.99) )
    }

> DAX expression in Figure 16 shows the following:
    
    Australian Customers Sales =
    SUMMARIZECOLUMNS (
      DimCustomer[CustomerKey]
      , FILTER(
        VALUES(‘DimGeography’[EnglishCountryRegionName])
        , ‘DimGeography’[EnglishCountryRegionName] = “Australia”)
        , “Customer Full Name”, CONCATENATEX(DimCustomer, DimCustomer[FirstName] & “ “ &
        DimCustomer[LastName])
          , “Sales Amount”, SUM(FactInternetSales[SalesAmount]) 
    )


---

***1.2.1 Calculated Tables***

> this is a block of subtext

    Calculated Table 1 =
      {“A”, “B”, “C”}


- 2020 <a href="https://www.theta.co.nz" target="_blank">Theta</a>.
