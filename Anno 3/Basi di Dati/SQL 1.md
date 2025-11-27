1. Trovare l'aspettativa di vita della nazione in cui si trova la città di Yangor
```sql
SELECT lifeexpectancy
FROM country JOIN city ON code = countrycode
WHERE city.name = 'Yangor'
```

2. Trovare il numero di lingue ufficiali parlate da più del 50% della popolazione (percentage > 50) di una nazione nei continenti americani. Se una lingua è ufficiale e parlata da più del 50% della popolazione in più nazioni deve comparire una sola volta
```sql
SELECT count(DISTINCT language)
FROM country JOIN countrylanguage ON code = countrycode
WHERE (isofficial = true AND percentage > 50) AND (continent = 'South America' OR continent = 'North America')

```

3. Trovare il nome della capitale della nazione in cui si trova la città di Nukus
```sql
SELECT c2.name
FROM country JOIN city c1 ON code = countrycode JOIN city c2 ON capital = c2.id
WHERE c1.name = 'Nukus'

```

4.  Numero di nazioni per cui non si conosce la capitale
```sql
SELECT count(*) 
FROM country
WHERE capital IS null
```

5. Trovare il nome della nazione che ha raggiunto per prima l’indipendenza in Europa
```sql
SELECT name
FROM country
WHERE indepyear = (
	SELECT MIN(indepyear)
	FROM country
	WHERE continent = 'Europe')
```

6. Contare le forme di governo in cui compare la parola Monarchy
```sql
SELECT COUNT(DISTINCT governmentform)
FROM country
WHERE governmentform LIKE '%Monarchy%'
```

7. Trovare il nome delle nazioni africane in cui si parla sia inglese che francese come lingue ufficiali
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
SELECT name
FROM country JOIN countrylanguage l1 ON code = l1.countrycode JOIN countrylanguage l2 ON code = l2.countrycode 
WHERE (l1.language = 'English' AND l1.isofficial) AND (l2.language = 'French' AND l2.isofficial) AND continent = 'Africa'
```

8. Numero di nazioni per cui non esiste una città che abbia più abitanti della capitale di quella nazione. Si devono considerare solo le nazioni che hanno una capitale nota.
```sql
SELECT COUNT(*)
FROM country JOIN city c ON capital = id
WHERE c.population = (
	SELECT MAX(population)
	FROM city
	WHERE countrycode = c.countrycode)
```

9. Numero di nazioni per cui si conosce SOLO la capitale come città
```sql
SELECT COUNT(*)
FROM country JOIN city c ON capital = id
WHERE (
	SELECT COUNT(*)
	FROM city
	WHERE countrycode = c.countrycode) = 1
```

10. Restituire la superficie delle nazioni che appartengono a un continente che non ha città
```sql
SELECT SUM(surfacearea)
FROM country
WHERE continent NOT IN (
	SELECT DISTINCT continent
	FROM country JOIN city on code = countrycode
)
```

"Voi programmate a sentimento. Il next step è non capire un cazzo come faccio io..."
Cit Spanò

11. Per ogni continente, numero di nazioni in cui una delle lingue è l'italiano e numero di persone che la parlano (considerare la percentuale). Se l'italiano non è parlato in un continente riportare 0. Ordinare il risultato in ordine non crescente rispetto al numero dei parlanti italiano.
``` SQL
SELECT 
    c.continent,
    COUNT(cl.language) AS num_countries_italian,
    COALESCE(SUM(c.population * cl.percentage / 100), 0) AS num_speakers_italian
FROM country c LEFT JOIN (
    SELECT countrycode, percentage, language
    FROM countrylanguage
    WHERE language = 'Italian'
) AS cl
ON c.code = cl.countrycode
GROUP BY c.continent
ORDER BY num_speakers_italian DESC;
```

12. Per ogni lingua, nome della lingua, numero di nazioni e numero di continenti in cui tale lingua si parla come lingua ufficiale e numero di nazioni e numero di continenti in cui si parla come non ufficiale. Il risultato deve essere in ordine non crescente per il numero di nazioni ufficiali
```SQL
SELECT 
	l.language, 
	(SELECT COUNT(countrycode)
	FROM countrylanguage
	WHERE language = l.language AND isofficial = 'true'
	) AS off_nat,
	(SELECT COUNT(DISTINCT continent)
	FROM countrylanguage JOIN country ON code = countrycode
	WHERE language = l.language AND isofficial = 'true'
	) AS off_cont,
	(SELECT COUNT(countrycode)
	FROM countrylanguage
	WHERE language = l.language AND isofficial = 'false'
	) AS unoff_nat,
	(SELECT COUNT(DISTINCT continent)
	FROM countrylanguage JOIN country ON code = countrycode
	WHERE language = l.language AND isofficial = 'false'
	) AS unoff_cont
FROM (SELECT DISTINCT language FROM countrylanguage) AS l
ORDER BY off_nat DESC
```

13. Trovare la media delle popolazioni massime delle città presenti nei vari continenti
```SQL
SELECT AVG(city.population)
FROM city JOIN country c ON countrycode = code
WHERE city.population = (
	SELECT MAX(city.population)
	FROM city JOIN country ON countrycode = code
	WHERE country.continent = c.continent
)
```

14. Numero di nazioni asiatiche che hanno meno di 5 città con una popolazione inferiore a 500000
```sql
SELECT COUNT(*)
FROM country
WHERE continent = 'Asia' AND 5 > (
	SELECT count(*)
	FROM city
	WHERE city.population < 500000 AND countrycode = code
)
```

15. Nome della seconda città più popolosa in Europa
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