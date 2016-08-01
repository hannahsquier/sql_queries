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

12.
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

13.
```sql
SELECT name, continent,
       CASE WHEN continent='Oceania' THEN 'Australasia'
       WHEN continent='Eurasia' OR name = 'Turkey' THEN 'Europe/Asia'
       WHEN continent='Caribbean' AND name LIKE 'B%' THEN 'North America'
       WHEN continent='Caribbean' AND name NOT LIKE 'B%' THEN 'South America'
       ELSE continent END

FROM world
ORDER BY name ASC
```

##SELECT Nobel
1.
```sql
SELECT *
  FROM nobel
 WHERE yr = 1950
```

2.
```sql
SELECT winner
  FROM nobel
 WHERE yr = 1962
   AND subject = 'Literature'
```

3.
```sql
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein'
```

4.
```sql
SELECT winner
FROM nobel
WHERE yr >= 2000 AND subject='Peace'
```
5.
```sql
SELECT *
FROM nobel
WHERE subject = 'Literature' AND yr >= 1980 AND yr <= 1989
```

6.
```sql
SELECT * FROM nobel
  WHERE winner IN ('Theodore Roosevelt',
                  'Woodrow Wilson',
                  'Jimmy Carter')
```

7.
```sql
SELECT winner
FROM nobel
WHERE winner LIKE 'John %'
```
8.
```sql
SELECT *
FROM nobel
WHERE (subject='Physics' AND yr = 1980) OR (subject='Chemistry' AND yr=1984)
```

9.
```sql
SELECT *
FROM nobel
WHERE yr = 1980 AND subject != 'Chemistry' AND subject != 'Medicine'
```

10.
```sql
SELECT *
FROM nobel
WHERE (yr < 1910 AND subject='Medicine') OR (yr >= 2004 AND subject='Literature')
```
11.
```sql
SELECT *
FROM nobel
WHERE winner LIKE 'peter gr_nberg'
```
12.
```
SELECT *
FROM nobel
WHERE winner LIKE 'eugene O''neill'
```