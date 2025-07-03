# Problem

Consider  and  to be two points on a 2D plane.

 happens to equal the minimum value in Northern Latitude (LAT_N in STATION).
 happens to equal the minimum value in Western Longitude (LONG_W in STATION).
 happens to equal the maximum value in Northern Latitude (LAT_N in STATION).
 happens to equal the maximum value in Western Longitude (LONG_W in STATION).
Query the Manhattan Distance between points  and  and round it to a scale of  decimal places.

Input Format

![image](https://github.com/user-attachments/assets/656f0e7e-5517-4205-9dc7-dbe9b8f7eaee)

The STATION table is described as follows:

Station.jpg

where LAT_N is the northern latitude and LONG_W is the western longitude.

# Solution

WITH cte AS (/* tabela temporária

    SELECT 
    
        MIN(LAT_N) AS a, 
        MIN(LONG_W) AS b, 
        MAX(LAT_N) AS c, 
        MAX(LONG_W) AS d 
        
    FROM station
    
), cte1 AS (

    SELECT 
    
        ABS(c - a) AS p1, 
        ABS(d - b) AS p2
        
    FROM cte
)

SELECT CAST(ROUND(p1 + p2, 4) AS DECIMAL(10,4)) AS ManhattanDistance

FROM cte1;

# Simpler Solution

SELECT CAST(

  ROUND(
    ABS(MAX(LAT_N) - MIN(LAT_N)) + ABS(MAX(LONG_W) - MIN(LONG_W))
  ,4) AS DECIMAL(10,4)
  
) AS ManhattanDistance
FROM STATION;
