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

  SUM(CASE WHEN teamid=team1 THEN 1 ELSE 0 END) AS score1, team2,
  SUM(CASE WHEN teamid=team2 THEN 1 ELSE 0 END) AS score2

  FROM game LEFT JOIN goal ON matchid = id
GROUP BY mdate, team1, team2
ORDER BY mdate, matchid, team1, team2
```

##More JOIN

1.
```sql
SELECT id, title
 FROM movie
 WHERE yr=1962
```

2.
```sql
SELECT yr
  FROM movie
 WHERE title="Citizen Kane"
```

3.
```sql
SELECT id, title, yr
  FROM movie
 WHERE title LIKE '%Star Trek%'
```

4.
```sql
SELECT title
  FROM movie
 WHERE id IN (11768, 11955, 21191)
```

5.
```sql
SELECT id
  FROM actor
 WHERE name="Glenn Close"
```

6.
```sql
SELECT id
 FROM movie
  WHERE title="Casablanca"
```

7.
```sql
SELECT name
 FROM actor JOIN casting ON id=actorid JOIN movie ON movieid=movie.id
WHERE movie.id="11768"
```

8.
```sql
SELECT name
 FROM actor JOIN casting ON id=actorid JOIN movie ON movieid=movie.id
WHERE movie.title="Alien"
```

9.
```sql
SELECT title
  FROM movie JOIN casting ON id=movieid JOIN actor ON actorid=actor.id
 WHERE name="Harrison Ford"
```

10.
```sql
SELECT title
  FROM movie JOIN casting ON id=movieid JOIN actor ON actorid=actor.id
 WHERE name="Harrison Ford" AND ord > 1
```

11.
```sql
SELECT title, actor.name
  FROM movie JOIN casting ON id=movieid JOIN actor ON actor.id=actorid
 WHERE yr=1962 AND ord=1
```

14.
```sql
SELECT actor.name
  FROM actor JOIN casting ON actorid=id JOIN movie ON movie.id=movieid
  WHERE ord = 1
 GROUP BY actor.name
 HAVING COUNT(*) >= 30
```

15.
```sql
SELECT movie.title, COUNT(*) AS actor_count
  FROM movie JOIN casting ON movie.id=movieid JOIN actor ON actorid=actor.id
 WHERE yr=1978
 GROUP BY title
 ORDER BY actor_count DESC
```
##Count and Sum
1.
```sql
SELECT SUM(population)
FROM world
```

2.
```
SELECT DISTINCT continent
  FROM world
```

3.
```sql
SELECT SUM(gdp)
  FROM world
 WHERE continent="Africa"
```

4.
```sql
 SELECT COUNT(*)
FROM world
WHERE area > 1000000
```

5.
```sql
SELECT sum(population)
FROM world
WHERE name IN ('France','Germany','Spain')
```

6.
```sql
SELECT continent, COUNT(*)
FROM world
GROUP BY continent
```

7.
```sql
SELECT continent, COUNT(*)
FROM world
WHERE population > 10000000
GROUP BY continent
```

8.
```sql
SELECT continent
FROM world
GROUP BY continent
HAVING SUM(population) > 100000000
```

##SELECT within SELECT

1.
```sql
SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')
```

2.
```sql
SELECT name
FROM world
WHERE continent = 'Europe' AND gdp/population >
(SELECT gdp/population
FROM world
WHERE name = 'United Kingdom')
```

3.
```sql
SELECT name, continent
FROM world
WHERE continent IN
(SELECT continent
FROM world
WHERE name in ('Argentina', 'Australia'))
ORDER BY name
```

4.
```sql
SELECT name, population
FROM world
WHERE population BETWEEN (SELECT population FROM world WHERE name='Canada') AND (SELECT population FROM world WHERE name='Poland')
```

5.
```sql
SELECT name,
  CONCAT(ROUND(population / (SELECT population FROM world WHERE name='Germany') * 100, 0), '%')
FROM world
WHERE continent = 'Europe'
```

Self Join
1.
```sql
SELECT COUNT(*)
FROM stops
```

2.
```
SELECT id
FROM stops
WHERE name='Craiglockhart'
```

3.
```sql
SELECT id, name
FROM stops JOIN route ON route.stop=stops.id
WHERE num=4 AND company='LRT'
```