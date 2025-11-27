1. Creare una tabella paesiricchi che contiene tutte le nazioni con popolazione > 0 e con ricchezza media per abitante (gnp/population) maggiore o uguale alla ricchezza media per abitante di tutto il mondo. La tabella deve avere i seguenti attributi: code, name, capital, continent, population, lifeexpectancy, gnp e la ricchezza media per abitante (gnp/population). Restituire il numero di righe della tabella paesiricchi
```SQL 
CREATE TABLE richcountry AS
	SELECT code, name, capital, continent, population, lifeexpectancy, gnp, gnp/population AS gnpavarage
	FROM country
	WHERE population > 0 AND gnp/population > (
		SELECT SUM(gnp)/SUM(population)
		FROM country
		WHERE population > 0
	)
```

2.  Aggiungi la chiave primaria e i check neccessari
```SQL
ALTER TABLE richcountry
ADD CONSTRAINT richcountry_pkey PRIMARY KEY (code);

ALTER TABLE richcountry
ADD CONSTRAINT code_length CHECK (LENGTH(code) <= 3)
```

3. Trovare la percentuale di paesi ricchi rispetto al numero di nazioni con popolazione > 0
```SQL
SELECT (SELECT COUNT(*) FROM richcountry) *100 /(SELECT COUNT(*) FROM country WHERE population > 0)
```

4. Aggiornare la colonna abitantinoncitta con il numero di abitanti della nazione che non vivono in città
```SQL
UPDATE richcountry c
SET noncitypopulation = population - (
	SELECT COUNT(city.population)
	FROM city
	WHERE countrycode = c.code
)
```

8. Trovare il nome della nazione, il continente della nazione con aspettativa di vita più breve nella tabella paesiricchi e le stesse informazioni nella tabella country. Restituire inoltre la differenza fra le due aspettative di vita e inserire nella risposta solo la differenza
```SQL
WITH low_rich AS(
	SELECT name, continent, lifeexpectancy
	FROM richcountry
	WHERE lifeexpectancy = (
		SELECT MIN(lifeexpectancy)
		FROM richcountry
	)
),
low_count AS(
	SELECT name, continent, lifeexpectancy
	FROM country
	WHERE lifeexpectancy = (
		SELECT MIN(lifeexpectancy)
		FROM country
	)
)
SELECT (
	SELECT lifeexpectancy
	FROM low_rich
) - (
	SELECT lifeexpectancy
	FROM low_count
)
```