Given the CITY and COUNTRY tables

Note: CITY.CountryCode and COUNTRY.Code are matching key columns.

**Input Format**

The **CITY** and **COUNTRY** tables are described as follows:

**CITY**

|  Column | Type |
|---|---|
| ID  | NUMBER |
| NAME | VARCHAR2(17)   |
| COUNTRYCODE | VARCHAR2(3)  |
| DISTRICT |  VARCHAR2(20) |
| POPULATION | NUMBER |

**COUNTRY**

|  Field | Type |
|---|---|
| CODE  | VARCHAR2(3) |
| NAME | VARCHAR2(44)   |
| CONTINENT | VARCHAR2(13)  |
| REGION |  VARCHAR2(25) |
| SURFACEAREA | NUMBER |
| INDEPYEAR |  VARCHAR2(5) |
| POPULATION | NUMBER |
| LIFEEXPECTANCY |  VARCHAR2(4) |
| GNP | NUMBER 
| GNPOLD |  VARCHAR2(9) |
| LOCALNAME |  VARCHAR2(44) |
| GOVERNMENTFORM |  VARCHAR2(44) |
| HEADOFSTATE |  VARCHAR2(32) |
| CAPITAL |  VARCHAR2(4) |
| CODE2 |  VARCHAR2(2) |


### [Asian Population](https://www.hackerrank.com/challenges/asian-population/problem)
*Query the sum of the populations of all cities where the CONTINENT is 'Asia'.*

**Solution**
``` SQL
select sum(city.population)
from city join country
on city.countrycode = country.code
where country.continent = "Asia"
```


### [African Cities](https://www.hackerrank.com/challenges/african-cities/problem)

*Query the names of all cities where the CONTINENT is 'Africa'.*

**Solution**
``` SQL
select city.name
from city join country
on city.countrycode = country.code
where country.continent = "Africa"
```


### [Average Population of Each Continent](https://www.hackerrank.com/challenges/average-population-of-each-continent/problem)
*Query the names of all the continents (COUNTRY.Continent) and their respective average city populations (CITY.Population) rounded down to the nearest integer.*

**Solution**
``` SQL
select country.continent, floor(avg(city.population))
from city join country
on city.countrycode = country.code
group by country.continent
```

***
### [The Report](https://www.hackerrank.com/challenges/the-report/problem)

**Input Format**

You are given two tables: Students and Grades. 

Students contains three columns ID, Name and Marks.

**STUDENTS**

|  Field | Type |
|---|---|
| ID  | INTEGER |
| NAME | STRING   |
| MARKS | INTEGER   |


**GRADES**

|  Grade | Min_Mark | Max_Mark |
|---|---|---|
| 1  | 0 | 9 |
| 2  | 10 | 19 |
| 3  | 20 | 29 |
| 4  | 30 | 39 |
| 5  | 40 | 49 |
| 6  | 50 | 59 |
| 7  | 60 | 69 |
| 8  | 70 | 79 |
| 9  | 80 | 89 |
| 10  | 90 | 100 |

Ketty gives Eve a task to generate a report containing three columns: Name, Grade and Mark. Ketty doesn't want the NAMES of those students who received a grade lower than 8. The report must be in descending order by grade -- i.e. higher grades are entered first. If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically. Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order.

*Write a query to help Eve.*

**Solution**
``` SQL
select (case when grade >= 8 then name else null end), grade, marks
from Students join Grades
on marks between min_mark and max_mark
order by grade desc, name asc
```
***
### [Top Competitors](https://www.hackerrank.com/challenges/full-score/problem)
Julia just finished conducting a coding contest, and she needs your help assembling the leaderboard! Write a query to print the respective hacker_id and name of hackers who achieved full scores for more than one challenge. Order your output in descending order by the total number of challenges in which the hacker earned a full score. If more than one hacker received full scores in same number of challenges, then sort them by ascending hacker_id.

**Input Format**

The following tables contain contest data:

**HACKERS**

|  Field | Type |
|---|---|
| HACKER_ID  | INTEGER |
| NAME | STRING   |

**DIFFICULTY**

|  Field | Type |
|---|---|
| DIFFICULT_LEVEL  | INTEGER |
| SCORE | INTEGER   |

**CHALLENGES**

|  Field | Type |
|---|---|
| CHALLENGES_ID  | INTEGER |
| HACKER_ID  | INTEGER |
| DIFFICULT_LEVEL  | INTEGER |

**SUBMISSIONS**

|  Field | Type |
|---|---|
| SUBMISSIONS_ID  | INTEGER |
| HACKER_ID  | INTEGER 
| CHALLENGES_ID  | INTEGER |
| SCORE | INTEGER   |

**Solution**
``` SQL
SELECT h.hacker_id, h.name
FROM submissions s
JOIN challenges c
    ON s.challenge_id = c.challenge_id
JOIN difficulty d
    ON c.difficulty_level = d.difficulty_level 
JOIN hackers h
    ON s.hacker_id = h.hacker_id
WHERE s.score = d.score 
    AND c.difficulty_level = d.difficulty_level
GROUP BY h.hacker_id,  h.name
HAVING COUNT(s.hacker_id) > 1
ORDER BY COUNT(h.hacker_id) DESC, h.hacker_id ASC
```
***
### [Contest Leaderboard](https://www.hackerrank.com/challenges/contest-leaderboard/submissions/code/145601969)

You did such a great job helping Julia with her last coding contest challenge that she wants you to work on this one, too!

The total score of a hacker is the sum of their maximum scores for all of the challenges. Write a query to print the hacker_id, name, and total score of the hackers ordered by the descending score. If more than one hacker achieved the same total score, then sort the result by ascending hacker_id. Exclude all hackers with a total score of  from your result.

**Input Format**

The following tables contain contest data:

**HACKERS**

|  Field | Type |
|---|---|
| HACKER_ID  | INTEGER |
| NAME | STRING   |

**SUBMISSIONS**

|  Field | Type |
|---|---|
| SUBMISSIONS_ID  | INTEGER |
| HACKER_ID  | INTEGER 
| CHALLENGES_ID  | INTEGER |
| SCORE | INTEGER   |

**Solution**
``` SQL
select h.hacker_id, h.name, sum(scores.score) as result
from hackers as h inner join 
	(select s.hacker_id, max(s.score) as score
	from submissions as s
	group by s.hacker_id, s.challenge_id) as scores
on h.hacker_id = scores.hacker_id
group by h.hacker_id, h.name
having result > 0
order by result desc, h.hacker_id
```
