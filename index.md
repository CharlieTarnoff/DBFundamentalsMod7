# Module 7: Functions
### CTarnoff, 2.27.21

## Introduction
This paper will focus on when to use a SQL User Defined Function and the differences between Scalar, Inline, and Multi-Statement Functions. 

## When to Use a SQL UDF
User Defined Functions (UDFs) allow the user to write a calculation or action and return that calculation back as a value (either single or multiple.) A UDF can be referenced as little or as much as you user wants and relieves the need to write the same code over and over again since the function is stored in the database. It’s also possible to set permissions on UDFs, giving certain users the ability to call the function. 

## Differences Between a Scalar, Inline and Multi-Statement Functions
A scalar function only returns a single value as an expression from a UDF. For example, a UDF that takes two integers and multiplies them would be a scalar function since the result of the expression only returns a single value. 

An inline function is a type of table-valued function and can only contain one select statement in it. It only returns a single set of rows. 

A multi-statement function is a type of table-valued function and returns a table of data. The user is able to structure this table with a higher degree of freedom than an inline function. Unlike an inline function, a multi-statement function can use multiple select statements. See below for an example of a multi-statement function.

```
CREATE FUNCTION dbo.fProductInventoriesWithPreviousMonthCountsWithKPIs(@CountVsPreviousCountKPI int)
	RETURNS TABLE AS 
	RETURN
	SELECT TOP 100000
		ProductName,
		InventoryDate,
		InventoryCount,
		PreviousMonthCount,
		CountVsPreviousCountKPI
	FROM vProductInventoriesWithPreviousMonthCountsWithKPIs
		WHERE CountVsPreviousCountKPI = 0
	ORDER BY ProductName, Month(InventoryDate), InventoryCount
GO
```

## Summary
I found Module 7 to be a challenging topic conceptually but saw the value that user defined functions can have when it comes to writing code in terms of time saved. I look forward to further practice with functions as they seem to be a common and useful tool with SQL.

