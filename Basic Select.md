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

### [Japanese Cities' Attributes](https://www.hackerrank.com/challenges/japanese-cities-attributes/problem)
*Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN.*

**Solution**
``` SQL
select *
from city
where countrycode = "JPN"
```

### [Japanese Cities' Names](https://www.hackerrank.com/challenges/japanese-cities-name/problem)
*Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is JPN.*

**Solution**
``` SQL
select name
from city
where countrycode = "JPN"
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

### [Weather Observation Station 1](https://www.hackerrank.com/challenges/weather-observation-station-1/problem)
*Query a list of CITY and STATE from the STATION table.*

**Solution**
``` SQL
select city, state
from station
```

### [Weather Observation Station 3](https://www.hackerrank.com/challenges/weather-observation-station-3/problem)
*Query a list of CITY names from STATION with even ID numbers only. You may print the results in any order, but must exclude duplicates from your answer.*

**Solution**
``` SQL
select distinct city
from station 
where ID%2=0
```

### [Weather Observation Station 4](https://www.hackerrank.com/challenges/weather-observation-station-4/problem)
*Let N be the number of CITY entries in STATION, and let N' be the number of distinct CITY names in STATION; query the value of N - N' from STATION. In other words, find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.*

**Solution**
``` SQL
select count(city) - count(distinct city)
from station
```

### [Weather Observation Station 5](https://www.hackerrank.com/challenges/weather-observation-station-5/problem)
*Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.*

**Solution**
``` SQL
(select city, length(city)
from station
order by length(city), city
limit 1)
union
(select city, length(city)
from station
order by length(city) desc, city
limit 1)
```

### [Weather Observation Station 6](https://www.hackerrank.com/challenges/weather-observation-station-6/problem)
*Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.*

**Solution**
``` SQL
SELECT distinct city
FROM station
WHERE left(city,1) IN ('a','e','i','o','u')
```

### [Weather Observation Station 7](https://www.hackerrank.com/challenges/weather-observation-station-7/problem)
*Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.*

**Solution**
``` SQL
SELECT distinct city
FROM station
WHERE right(city,1) IN ('a','e','i','o','u')
```

### [Weather Observation Station 8](https://www.hackerrank.com/challenges/weather-observation-station-8/problem)
*Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.*

**Solution**
``` SQL
SELECT distinct city
FROM station
WHERE left(city,1) IN ('a','e','i','o','u') AND
right(city,1) IN ('a','e','i','o','u')
```

### [Weather Observation Station 9](https://www.hackerrank.com/challenges/weather-observation-station-9/problem)
*Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.*

**Solution**
``` SQL
SELECT distinct city
FROM station
WHERE left(city,1) NOT IN ('a','e','i','o','u')
```

### [Weather Observation Station 10](https://www.hackerrank.com/challenges/weather-observation-station-10/problem)
*Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates.*

**Solution**
``` SQL
SELECT distinct city
FROM station
WHERE right(city,1) NOT IN ('a','e','i','o','u')
```

### [Weather Observation Station 11](https://www.hackerrank.com/challenges/weather-observation-station-11/problem)
*Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.*

**Solution**
``` SQL
SELECT distinct city
FROM station
WHERE left(city,1) NOT IN ('a','e','i','o','u') OR
right(city,1) NOT IN ('a','e','i','o','u')
```

### [Weather Observation Station 12](https://www.hackerrank.com/challenges/weather-observation-station-12/problem)
*Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.*

**Solution**
``` SQL
SELECT distinct city
FROM station
WHERE left(city,1) NOT IN ('a','e','i','o','u') AND
right(city,1) NOT IN ('a','e','i','o','u')
```
***
### [Higher Than 75 Marks](https://www.hackerrank.com/challenges/more-than-75-marks/problem)
*Query the Name of any student in STUDENTS who scored higher than  Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.*

**Input Format**

The STUDENTS table is described as follows:


|  Field | Type |
|---|---|
| ID  | INTEGER |
| NAME | STRING   |
| MARKS  | INTEGER  |

Name column only contains uppercase (A-Z) and lowercase (a-z) letters.

**Solution**
``` SQL
SELECT name 
FROM students
WHERE marks > 75
ORDER BY right(name,3), ID ASC
```
***

**Input Format**

The Employee table containing employee data for a company is described as follows:


|  Column | Type |
|---|---|
| EMPLOYEE_ID  | INTEGER |
| NAME | STRING   |
| MONTHS  | INTEGER  |
| SALARY  | INTEGER  |

where employee_id is an employee's ID number, name is their name, months is the total number of months they've been working for the company, and salary is their monthly salary.

### [Employee Names](https://www.hackerrank.com/challenges/name-of-employees/problem)
*Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table in alphabetical order.*

**Solution**
``` SQL
select name
from Employee
order by name
```

### [Employee Salaries](https://www.hackerrank.com/challenges/salary-of-employees/problem)
*Write a query that prints a list of employee names (i.e.: the name attribute) for employees in Employee having a salary greater than $2000 per month who have been employees for less than 10 months. Sort your result by ascending employee_id.*


**Solution**
``` SQL
select name
from Employee
where salary > 2000 and months <10
order by employee_id
```
