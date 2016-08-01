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
```sql
SELECT *
FROM nobel
WHERE winner LIKE 'eugene O''neill'
```

13.
```sql
SELECT winner, yr, subject
  FROM nobel
 WHERE winner LIKE 'Sir%'
ORDER BY yr DESC, winner
```

14.
```sql
SELECT winner, subject
  FROM nobel
 WHERE yr=1984
 ORDER BY subject IN ('Physics','Chemistry'), subject,winner
 ```

##Join operations
1.
```sql
SELECT goal.matchid, goal.player
  FROM goal
  WHERE teamid = 'GER'
```

2.
```sql
SELECT id,stadium,team1,team2
  FROM game
 WHERE id = 1012
```

3.
```sql
SELECT goal.player, goal.teamid, game.stadium, game.mdate
  FROM game JOIN goal ON (matchid=id)
 WHERE teamid='GER'
```

4.
```sql
SELECT team1, team2, player
  FROM game JOIN goal ON matchid=id
 WHERE player LIKE 'Mario%'
```

5.
```sql
SELECT player, teamid, coach, gtime
  FROM goal JOIN eteam ON teamid=id
 WHERE gtime<=10
```

6.
```sql
SELECT mdate, teamname
  FROM eteam JOIN game ON team1=eteam.id
 WHERE coach='Fernando Santos'
```

7.
```sql
SELECT player
  FROM game JOIN goal ON matchid=id
 WHERE stadium='National Stadium, Warsaw'
```

8.
```sql
SELECT DISTINCT player
  FROM game JOIN goal ON matchid = id
    WHERE  teamid != 'GER' AND (team1='GER' OR team2='GER')
```

9.
```sql
SELECT teamname, COUNT(*)
  FROM eteam JOIN goal ON id=teamid
GROUP BY teamname
ORDER BY teamname
```

10.
```sql
 SELECT stadium, COUNT(*)
FROM game JOIN goal ON id=matchid
GROUP BY stadium
```

11.
```sql
SELECT matchid, mdate, COUNT(*)
  FROM game JOIN goal ON matchid = id
 WHERE (team1 = 'POL' OR team2 = 'POL')
GROUP BY matchid, mdate
```

12.
```sql
SELECT matchid, mdate, COUNT(*)
FROM goal JOIN game on matchid = id
WHERE teamid='GER'
GROUP BY matchid, mdate
```

13.
```sql
SELECT mdate,
  team1,
  COUNT(CASE WHEN teamid=team1 THEN 1 ELSE 0 END) AS score1, team2,
  COUNT(CASE WHEN teamid=team2 THEN 1 ELSE 0 END) AS score2

  FROM game JOIN goal ON matchid = id,
GROUP BY mdate, team1, team2, teamid
ORDER BY mdate, matchid, team1, team2
```