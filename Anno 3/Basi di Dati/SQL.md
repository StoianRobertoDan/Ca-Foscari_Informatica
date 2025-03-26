1.
```sql
select co.lifeexpectancy
from country co join city ci on co.code = ci.countrycode
where ci.name = 'Yangor'
```

2.
```sql
select count(distinct lg.language)
from country co join countrylanguage lg on co.code = lg.countrycode
where lg.isofficial = true and lg.percentage > 50 and (co.continent = 'North America' or co.continent = 'South America');
```

3.
```sql
select ca.name
from country co join city ci on co.code = ci.countrycode join city ca on co.capital = ca.id
where ci.name = 'Nukus';
```

4.
```sql
select count(*) 
from country
where capital is null;
```

5.
```sql
select c.name
from country c
where c.indepyear = (select min(indepyear) from country where continent = 'Europe');
```

6.
```sql
select count(distinct c.governmentform)
from country c
where c.governmentform like '%Monarchy%';
```

7.
```sql
WITH AfricaEng as(
	select co.code, co.name
	from country co join countrylanguage lg on co.code = lg.countrycode
	where lg.isofficial = true and lg.language = 'English' and co.continent='Africa'
),
AfricaFr as(
	select co.code, co.name
	from country co join countrylanguage lg on co.code = lg.countrycode
	where lg.isofficial = true and lg.language = 'French' and co.continent='Africa'
)
select ae.name
from AfricaEng ae join AfricaFr af on ae.code=af.code;
```


altro 7.
```sql
SELECT co.name 
FROM country co JOIN countrylanguage lg1 ON co.code = lg1.countrycode JOIN countrylanguage lg2 ON co.code = lg2.countrycode 
WHERE lg1.isofficial = true AND lg1.language = 'English' AND lg2.isofficial = true AND lg2.language = 'French' AND co.continent = 'Africa';
```

8.
```sql
SELECT COUNT(*) AS numero_nazioni
FROM nazioni n
WHERE n.capitale_id IS NOT NULL
  AND NOT EXISTS (
    SELECT 1
    FROM citta c
    WHERE c.nazione_id = n.id
      AND c.popolazione > (
        SELECT c_cap.popolazione
        FROM citta c_cap
        WHERE c_cap.id = n.capitale_id
      )
  );
```

9.
```sql
SELECT COUNT(*)
FROM country n
WHERE n.capital IS NOT NULL
  AND NOT EXISTS (
    SELECT 1
    FROM city c
    WHERE c.countrycode = n.code
      AND c.id != n.capital
   );
```

10.
```sql
SELECT SUM(n.surfacearea)
FROM country n
WHERE n.continent NOT IN (SELECT distinct co.continent
					 FROM country co JOIN city ci ON co.code = ci.countrycode)
```

"Voi programmate a sentimento. Il next step è non capire un cazzo come faccio io..."
Cit Spanò

11

14.
```sql
SELECT COUNT(DISTINCT country.code)
FROM country
WHERE continent = 'Asia' AND 5 > (
	SELECT count(*)
	FROM city
	WHERE city.population < 500000 AND countrycode = code
)
```

15.
```sql
WITH europeanCity AS(
	SELECT city.id, city.name, city.population
	FROM city JOIN country ON countrycode = code
	WHERE continent = 'Europe'
)
SELECT name 
FROM europeanCity
WHERE population = (
	SELECT MAX(population) 
	FROM europeanCity
	WHERE population != (
		SELECT max(population)
		FROM europeanCity
	)
) 
```

altro 15.
```sql
SELECT city.name 
FROM city JOIN country ON countrycode = code
WHERE country.continent = 'Europe'
ORDER BY city.population DESC LIMIT 1 OFFSET 1
```