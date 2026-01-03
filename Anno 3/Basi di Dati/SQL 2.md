1. Creare una tabella paesiricchi che contiene tutte le nazioni con popolazione > 0 e con ricchezza media per abitante (gnp/population) maggiore o uguale alla ricchezza media per abitante di tutto il mondo. La tabella deve avere i seguenti attributi: code, name, capital, continent, population, lifeexpectancy, gnp e la ricchezza media per abitante (gnp/population). Restituire il numero di righe della tabella paesiricchi
```postgreSQL 
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
```postgreSQL
ALTER TABLE richcountry
ADD CONSTRAINT richcountry_pkey PRIMARY KEY (code);

ALTER TABLE richcountry
ADD CONSTRAINT code_length CHECK (LENGTH(code) <= 3)
```

3. Trovare la percentuale di paesi ricchi rispetto al numero di nazioni con popolazione > 0
```postgreSQL
SELECT (SELECT COUNT(*) FROM richcountry) *100 /(SELECT COUNT(*) FROM country WHERE population > 0)
```

4. Aggiornare la colonna abitantinoncitta con il numero di abitanti della nazione che non vivono in città
```postgreSQL
UPDATE richcountry c
SET noncitypopulation = population - (
	SELECT COUNT(city.population)
	FROM city
	WHERE countrycode = c.code
)
```

5. Aggiornare la colonna abitantinoncitta con il numero di abitanti della nazione che non vivono in città
```postgreSQL
UPDATE richcountry c
SET noncitypopulation = population - (
	SELECT COUNT(city.population)
	FROM city
	WHERE countrycode = c.code
)
```

8. Trovare il nome della nazione, il continente della nazione con aspettativa di vita più breve nella tabella paesiricchi e le stesse informazioni nella tabella country. Restituire inoltre la differenza fra le due aspettative di vita e inserire nella risposta solo la differenza
```postgreSQL
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

9. Creare una tabella countrylanguagepaesiricchi aventi gli stessi campi di countrylanguage e contenente le lingue dei paesi ricchi. Restituire il numero di righe della tabella countrylanguagepaesiricchi
```postgreSQL
CREATE TABLE richcountrylanguage AS
	SELECT *
	FROM countrylanguage
	WHERE countrycode IN (
		SELECT code
		FROM richcountry
	)
	
SELECT COUNT(*)
FROM richcountrylanguage
```

10. Aggiungere la chiave primaria, la chiave esterna ed eventuali vincoli NOT NULL alla tabella countrylanguagepaesiricchi
```postgreSQL
ALTER TABLE richcountrylanguage
ADD CONSTRAINT richlanguage_pkey
PRIMARY KEY (countrycode, language);

ALTER TABLE richcountrylanguage
ADD CONSTRAINT richlanguage_fkey
FOREIGN KEY (countrycode) REFERENCES richcountry(code)
```

11. Per tutte quelle nazioni che hanno ALMENO due lingue NON ufficiali e non hanno alcuna lingua ufficiale, in countrylanguagepaesiricchi porre ufficiale quella/e lingua/e che è/sono parlata/e dalla percentuale più alta della popolazione di quella nazione. Restituire il numero di righe aggiornate
```postgreSQL
UPDATE richcountrylanguage l
SET isofficial = 'true'
WHERE (
	SELECT COUNT(*)
	FROM richcountrylanguage
	WHERE l.countrycode = countrycode AND isofficial = 'false'
) > 1 AND countrycode NOT IN (
	SELECT countrycode
	FROM richcountrylanguage
	WHERE isofficial = 'true'
) AND percentage = (
	SELECT MAX(percentage)
	FROM richcountrylanguage
	WHERE l.countrycode = countrycode
)
```

12. Creare una tabella citypaesiricchi aventi gli stessi campi di city e contenente le citta' dei paesi ricchi. Restituire il numero di righe della tabella citypaesiricchi.
```postgreSQL
CREATE TABLE richcountrycity AS
	SELECT *
	FROM city
	WHERE countrycode IN (
		SELECT code
		FROM richcountry
	)
	
SELECT COUNT(*)
FROM richcountrycity
```

13. Aggiungere la chiave primaria, la chiave esterna su countrycode ed eventuali vincoli NOT NULL alla tabella citypaesiricchi come quelli presenti nella tabella city.
```postgreSQL
ALTER TABLE richcountrycity
ADD CONSTRAINT richcity_pkey
PRIMARY KEY (id);

ALTER TABLE richcountrycity
ADD CONSTRAINT richcity_fkey
FOREIGN KEY (countrycode) REFERENCES richcountry(code)
```

14. Aggiungere la chiave esterna su capital nella tabella paesiricchi che fa riferimento alla tabella citypaesiricchi con la politica di reazione ON DELETE CASCADE
```postgreSQL
ALTER TABLE richcountry
ADD CONSTRAINT richcountry_capital_fkey
FOREIGN KEY (capital) REFERENCES richcountrycity (id) 
ON DELETE CASCADE
```

15. Rimuovere le città nella tabella citypaesiricchi che non sono capitali e che hanno una popolazione maggiore della capitale della nazione in cui si trovano. Restituire il numero di righe cancellate.
```postgreSQL
DELETE FROM richcountrycity c
WHERE id NOT IN (
	SELECT capital
	FROM richcountry
) AND population > (
	SELECT richcountrycity.population
	FROM richcountrycity JOIN richcountry ON capital = id
	WHERE code = c.countrycode
)
```

16. Rimuovere le lingue non ufficiali nella tabella countrylanguagepaesiricchi parlate in al più tre stati dei paesiricchi come non ufficiali. Restituire il numero di righe cancellate.
```postgreSQL
DELETE FROM richcountrylanguage l
WHERE (
	SELECT COUNT(*)
	FROM richcountrylanguage
	WHERE l.language = language AND isofficial IS FALSE
) <= 3 AND isofficial IS FALSE
```