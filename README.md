##SELECT Basics
1.
```sql
SELECT population FROM world
  WHERE name = 'Germany'
```

2.
```sql
SELECT name, population FROM world
  WHERE name IN ('Ireland', 'Iceland', 'Denmark');
```

3.
```sql
SELECT name, area FROM world
  WHERE area BETWEEN 200000 AND 250000
```

##SELECT from WORLD
1.
```sql
SELECT name, continent, population FROM world
```

2.
```sql
SELECT name FROM world
WHERE population>200000000
```

3.
```sql
SELECT name, 
       gdp/population AS 'per capita GDP'
   FROM world
   WHERE population > 200000000
```

4.
```sql
SELECT name, population/1000000
   FROM world
  WHERE continent = 'South America'
```

5.
```sql
SELECT name, population
   FROM world
  WHERE name IN ('France', 'Germany', 'Italy')
```

6. 
```sql
SELECT name 
   FROM world
  WHERE name LIKE '%United%'
```

7.
```sql
SELECT name, population, area
  FROM world
 WHERE area > 3000000 OR population > 250000000
```

8.
```sql
 SELECT name, population, area
  FROM world
  WHERE area > 3000000 XOR population > 250000000
```

9.
```
SELECT name, ROUND(population/1000000, 2), ROUND(gdp/1000000000, 2) AS "GDP in billions"
  FROM world
 WHERE continent = 'South America'
```

10.
```sql
SELECT name, ROUND(gdp/population, -3) AS "per capita GDP"
  FROM world
 WHERE gdp >= 1000000000000
 ```

11.
```sql
SELECT name, 
       CASE WHEN continent='Oceania' THEN 'Australasia'
            ELSE continent END
  FROM world
 WHERE name LIKE 'N%'
```

13.
```sql
SELECT name, 
       CASE WHEN continent='Europe' THEN 'Eurasia'
            WHEN continent='Asia' THEN 'Eurasia'
            WHEN continent='North America' THEN 'America'
            WHEN continent='South America' THEN 'America'
            WHEN continent='Caribbean' THEN 'America'
            ELSE continent END
  FROM world
 WHERE name LIKE 'A%' OR NAME LIKE 'B%'
```