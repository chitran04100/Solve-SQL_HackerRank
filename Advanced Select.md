### [Type of Triangle](https://www.hackerrank.com/challenges/what-type-of-triangle/problem)
Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:

- Equilateral: It's a triangle with  sides of equal length.
- Isosceles: It's a triangle with  sides of equal length.
- Scalene: It's a triangle with  sides of differing lengths.
- Not A Triangle: The given values of A, B, and C don't form a triangle.

**Input Format**

The TRIANGLES table is described as follows:
|  Column | Type |
|---|---|
| A  | INTEGER |
| B | INTEGER   |
| C  | INTEGER  |

Each row in the table denotes the lengths of each of a triangle's three sides.

**Solution**
```SQL
select 
    (case 
        when a+b>c and a+c>b and b+c>a then 
            (case 
                when a=b and a=c and b=c then "Equilateral"
                when a=b or a=c or b=c then "Isosceles"
                else "Scalene"
            end)
            else "Not A Triangle" end)
from Triangles
```
***
### [The PADS](https://www.hackerrank.com/challenges/the-pads/problem)

Generate the following two result sets:

1. Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).
2. Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order, and output them in the following format:
```There are a total of [occupation_count] [occupation]s.```
where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and [occupation] is the lowercase occupation name. If more than one Occupation has the same [occupation_count], they should be ordered alphabetically.

Note: There will be at least two entries in the table for each type of occupation.

**Input Format**

The OCCUPATIONS table is described as follows:
|  Column | Type |
|---|---|
| NAME  | STRING |
| OCCUPATION | STRING   |

Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.

**Solution**
```SQL
select concat(name,'(',left(Occupation,1),')')
from OCCUPATIONS 
order by name;

select concat('There are a total of ', count(*), ' ', lower(occupation),'s.')
from OCCUPATIONS
group by occupation
order by count(*)
```
***
### [Binary Tree Nodes](https://www.hackerrank.com/challenges/binary-search-tree-1/problem)

You are given a table, BST, containing two columns: N and P, where N represents the value of a node in Binary Tree, and P is the parent of N.

**Input Format**

|  Column | Type |
|---|---|
| N | INTEGER |
| P | INTEGER |

Write a query to find the node type of Binary Tree ordered by the value of the node. Output one of the following for each node:
- Root: If node is root node.
- Leaf: If node is leaf node.
- Inner: If node is neither root nor leaf node.

**Solution**
```SQL
select
    case 
        when p is null then concat(N, " Root")
        when n in (select p from BST) then concat(N, " Inner")
        else concat(N, " Leaf")
    end
from BST
order by n asc
```
***
### [New Companies](https://www.hackerrank.com/challenges/the-company/problem)
Amber's conglomerate corporation just acquired some new companies. Each of the companies follows this hierarchy:
**founder** => **lead manager** => *senior manager** => **manager** => **employee**
Given the table schemas below, write a query to print the company_code, founder name, total number of lead managers, total number of senior managers, total number of managers, and total number of employees. Order your output by ascending company_code.

Note:
- The tables may contain duplicate records.
- The company_code is string, so the sorting should not be numeric. For example, if the company_codes are C_1, C_2, and C_10, then the ascending company_codes will be C_1, C_10, and C_2.

**Input Format**

The following tables contain company data:

**Company**
|  Column | Type |
|---|---|
| company_code  | string |
| founder | string   |

**Lead_Manager**
|  Column | Type |
|---|---|
| lead_Manager_code  | string |
| company_code | string   |

**Senior_Manager**
|  Column | Type |
|---|---|
| senior_Manager_code  | string |
| lead_Manager_code  | string |
| company_code | string   |

**Manager**
|  Column | Type |
|---|---|
| manager_code  | string |
| senior_Manager_code  | string |
| lead_Manager_code  | string |
| company_code | string   |

**Employee**
|  Column | Type |
|---|---|
| employee_code  | string |
| manager_code  | string |
| senior_Manager_code  | string |
| lead_Manager_code  | string |
| company_code | string   |

**Solution**
```SQL
select c.company_code, c.founder, count(distinct l.lead_manager_code), count(distinct s.senior_manager_code), count(distinct m.manager_code), count(distinct e.employee_code)
from company c, lead_manager l, senior_manager s, manager m, employee e
where c.company_code = l.company_code
and l.company_code = s.company_code
and s.company_code = m.company_code
and m.company_code = e.company_code
group by c.company_code, c.founder
order by c.company_code asc
```
