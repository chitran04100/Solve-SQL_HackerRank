**Input Format**

The CITY table is described as follows:

**CITY TABLE**

|  Field | Type |
|---|---|
| ID  | NUMBER |
| NAME | VARCHAR2(17)   |
| COUNTRYCODE | VARCHAR2(3)  |
| DISTRICT |  VARCHAR2(20) |
| POPULATION | NUMBER |

### [Revising Aggregations - The Count Function](https://www.hackerrank.com/challenges/revising-aggregations-the-count-function/problem)
*Query a count of the number of cities in CITY TABLE having a Population larger than 100,000*

**Solution**
``` SQL
select count(*)
from city
where population > 100000
```
### [Revising Aggregations - The Sum Function](https://www.hackerrank.com/challenges/revising-aggregations-sum/problem)
*Query the total population of all cities in CITY TABLE where District is California.*

**Solution**
```SQL
select sum(population)
from city
where district = 'California'
```
### [Revising Aggregations - Averages](https://www.hackerrank.com/challenges/revising-aggregations-the-average-function/problem)
*Query the average population of all cities in CITY TABLE where District is California.*

**Solution**
```SQL
select avg(population)
from city
where district = 'California'
```
### [Average Population](https://www.hackerrank.com/challenges/average-population/problem)
*Query the average population for all cities in CITY, rounded down to the nearest integer.*

**Solution**
```SQL
select floor(avg(population))
from city
```
### [Japan Population](https://www.hackerrank.com/challenges/japan-population/problem)
*Query the sum of the populations for all Japanese cities in CITY. The COUNTRYCODE for Japan is JPN.*

**Solution**
```SQL
select sum(population)
from city
where COUNTRYCODE = 'JPN'
```
### [Population Density Difference](https://www.hackerrank.com/challenges/population-density-difference/problem)
*Query the difference between the maximum and minimum populations in CITY.*

**Solution**
```SQL
select max(population) - min(population)
from city
```
***
**Input Format**

The STATION table is described as follows:


|  Field | Type |
|---|---|
| ID  | NUMBER |
| CITY | VARCHAR2(21)   |
| STATE  | VARCHAR2(2)  |
| LAT_N |  NUMBER |
| LONG_W | NUMBER |

where LAT_N is the northern latitude and LONG_W is the western longitude.

### [Weather Observation Station 2](https://www.hackerrank.com/challenges/weather-observation-station-2/problem)
*Query the following two values from the STATION table:*
- The sum of all values in LAT_N rounded to a scale of 2 decimal places.
- The sum of all values in LONG_W rounded to a scale of 2 decimal places._

**Solution**
```SQL
select round(sum(lat_n),2),round(sum(long_w),2)
from station 
```
### [Weather Observation Station 13](https://www.hackerrank.com/challenges/weather-observation-station-13/problem)

*Query the sum of Northern Latitudes (LAT_N) from STATION having values greater than 38.7880 and less than 137.2345 . Truncate your answer to 4 decimal places.*

**Solution**
```SQL
select round(sum(lat_n),4)
from station 
where lat_n > 38.7880 and lat_n < 137.2345
```
### [Weather Observation Station 14](https://www.hackerrank.com/challenges/weather-observation-station-14/problem)
*Query the greatest value of the Northern Latitudes (LAT_N) from STATION that is less than 137.2345. Truncate your answer to 2 decimal places.*

**Solution**
```SQL
select round(max(lat_n),4)
from station 
where lat_n < 137.2345
```
### [Weather Observation Station 15](https://www.hackerrank.com/challenges/weather-observation-station-15/problem)
*Query the Western Longitude (LONG_W) for the largest Northern Latitude (LAT_N) in STATION that is less than 137.2345. Round your answer to 4 decimal places.*

**Solution**
```SQL
select round(long_w,4)
from station
where lat_n < 137.2345
order by lat_n desc
limit 1
```
### [Weather Observation Station 16](https://www.hackerrank.com/challenges/weather-observation-station-16/problem)
*Query the smallest Northern Latitude (LAT_N) from STATION that is greater than 38.7880. Round your answer to 4 decimal places.*

**Solution**
```SQL
select round(min(lat_n),4)
from station 
where lat_n > 38.7880
```
### [Weather Observation Station 17](https://www.hackerrank.com/challenges/weather-observation-station-17/problem)
*Query the Western Longitude (LONG_W) where the smallest Northern Latitude (LAT_N) in STATION is greater than 38.7880. Round your answer to 4 decimal places.*

**Solution**
```SQL
select round(long_w,4)
from station
where lat_n > 38.7880
order by lat_n asc
limit 1
```
### [Weather Observation Station 18](https://www.hackerrank.com/challenges/weather-observation-station-18/problem)
Consider P1(a,b) and P2(c,d) to be two points on a 2D plane.

- a happens to equal the minimum value in Northern Latitude (LAT_N in STATION).
- b happens to equal the minimum value in Western Longitude (LONG_W in STATION).
- c happens to equal the maximum value in Northern Latitude (LAT_N in STATION).
- d happens to equal the maximum value in Western Longitude (LONG_W in STATION).

*Query the Manhattan Distance between points P1 and P2 and round it to a scale of 4 decimal places.*

**Solution**
```SQL
select round((abs(max(lat_n)-min(lat_n)) + abs(max(long_w)-min(long_w))),4)
from station
```
### [Weather Observation Station 19](https://www.hackerrank.com/challenges/weather-observation-station-19/problem)
Consider P1(a,c) and P2(b,d) to be two points on a 2D plane where (a,b) are the respective minimum and maximum values of Northern Latitude (LAT_N) and (c,d) are the respective minimum and maximum values of Western Longitude (LONG_W) in STATION.

*Query the Euclidean Distance between points P1 and P2 and format your answer to display 4 decimal digits.*

**Solution**
```SQL
select round(sqrt(power(max(lat_n)-min(lat_n),2)+power(max(long_w)-min(long_w),2)),4)
from station
```
### [Weather Observation Station 20](https://www.hackerrank.com/challenges/weather-observation-station-20/problem)
A median is defined as a number separating the higher half of a data set from the lower half. 

*Query the median of the Northern Latitudes (LAT_N) from STATION and round your answer to 4 decimal places.*

**Solution**
```SQL
set @index := -1;
select round(avg(lat_2),4)
from
    (select @index := @index + 1 as id_2, lat_n as lat_2
    from station
    order by lat_2) as station_2
where id_2 in (floor(@index/2),ceiling(@index/2))
```
***
### [The Blunder](https://www.hackerrank.com/challenges/the-blunder/problem)
Samantha was tasked with calculating the average monthly salaries for all employees in the EMPLOYEES table, but did not realize **her keyboard's 0 key was broken** until after completing the calculation. She wants your help finding the difference between her miscalculation (using salaries with any zeroes removed), and the actual average salary.

*Write a query calculating the amount of error (i.e.: **actual - miscalculated** average monthly salaries), and round it up to the next integer.*

**Input Format**

The EMPLOYEES table is described as follows:


|  Field | Type |
|---|---|
| ID  | INTEGER |
| NAME | STRING   |
| SALARY  | INTEGER  |

Note: Salary is measured in dollars per month and its value is < 10^5.

**Solution**
```SQL
select ceiling(avg(salary) - avg(salary_error))
from 
    (select salary, replace(salary,'0','') as salary_error
    from employees) as employees_error
```
***
### [Top Earners](https://www.hackerrank.com/challenges/earnings-of-employees/problem)
We define an employee's total earnings to be their monthly **salary X months** worked, and the maximum total earnings to be the maximum total earnings for any employee in the Employee table. 

*Write a query to find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings. Then print these values as 2 space-separated integers.*

**Input Format**

The Employee table containing employee data for a company is described as follows:


|  Field | Type |
|---|---|
| EMPLOYEE_ID  | INTEGER |
| NAME | STRING   |
| MONTHS | INTEGER   |
| SALARY  | INTEGER  |

where employee_id is an employee's ID number, name is their name, months is the total number of months they've been working for the company, and salary is the their monthly salary.

**Solution**
```SQL
select months*salary as earnings, count(*)
from employee
group by earnings
order by earnings desc
limit 1
```
