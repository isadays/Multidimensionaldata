WebPivotTable is a pure Javascript application that can be used in any browser and needs no additional plugins.


Some MDX queries:

WITH 
SET [~0] AS {{[Delivery Date].[Month of Year].[All Periods]}} 
SET [~1] AS Exists({[Delivery Date].[Month of Year].[Month of Year].Members}, [~0]) 
SET [~2] AS {[Measures].[Average Sales Amount], [Measures].[Internet Average Sales Amount]} 
SET [~3] AS {[Delivery Date].[Date].[Date].Members} 


WITH 
SET [~0] AS {{[Delivery Date].[Month of Year].[All Periods]}} 
SET [~1] AS Exists({[Delivery Date].[Month of Year].[Month of Year].Members}, [~0]) 
SET [~2] AS {[Measures].[Internet Average Unit Price], [Measures].[Internet Freight Cost], [Measures].[Growth in Customer Base], [Measures].[Average Sales Amount]} 
SET [~3] AS {{[Promotion].[Promotions].[All Promotions]}} 
SET [~4] AS Exists({[Promotion].[Promotions].[Category].Members}, [~3]) 
SET [~5] AS Exists({[Promotion].[Promotions].[Type].Members}, [~4]) 
SET [~6] AS Exists({[Promotion].[Promotions].[Promotion].Members}, [~5]) 

SELECT 
NON EMPTY  Hierarchize(Union(CrossJoin([~0],[~2]), CrossJoin([~1],[~2]))) ON COLUMNS , 
NON EMPTY  {Hierarchize({[~3],[~4],[~5],[~6]})} ON ROWS 
FROM [Adventure Works] 
 WHERE  Hierarchize(CrossJoin({[Delivery Date].[Date].[Date].Members},{[Source Currency].[Source Currency].&[US Dollar], [Source Currency].[Source Currency].&[Canadian Dollar], [Source Currency].[Source Currency].&[US Dollar], [Source Currency].[Source Currency].&[Canadian Dollar], [Source Currency].[Source Currency].&[Canadian Dollar], [Source Currency].[Source Currency].&[US Dollar], [Source Currency].[Source Currency].&[Canadian Dollar], [Source Currency].[Source Currency].&[US Dollar], [Source Currency].[Source Currency].&[Bahamian Dollar], [Source Currency].[Source Currency].&[Bahamian Dollar], [Source Currency].[Source Currency].&[EURO]}))
