WebPivotTable is a pure Javascript application that can be used in any browser and needs no additional plugins.


Some MDX queries:

WITH 
SET [~0] AS {{[Delivery Date].[Month of Year].[All Periods]}} 
SET [~1] AS Exists({[Delivery Date].[Month of Year].[Month of Year].Members}, [~0]) 
SET [~2] AS {[Measures].[Average Sales Amount], [Measures].[Internet Average Sales Amount]} 
SET [~3] AS {[Delivery Date].[Date].[Date].Members} 
