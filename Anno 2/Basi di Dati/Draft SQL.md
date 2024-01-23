Forma:
- Select: 
	- Quello che voglio tirare fuori come tabella.
- From: 
	- Le tabelle che vengono prese in considerazione dalla query (meno  tabelle prendiamo in considerazione meglio è) e le varie specificazioni.
- Where:
	- Condizione di giunzione

Es:
- Select s.Nome, s.Cognome, s.Tutor
- From Studenti s
- Where s.Tutor is not NULL

Es: 
- Prendere nome e cognome delle persone e dei nonni che hanno  lo stesso lavoro.
- Persone (Id, Nome, Cognome, IdPadre, Lavoro)
	- PK(Id), IdPadre FK(Persone).
- Proced:
	- Select f.Cognome AS CogNipote, f.Nome AS NomNipote, n.Cognome AS CogNonno, n.Nome AS NomNonno 
	- From persone f, persone p, persone n
	- Where f.IdPadre = p.Id AND p.IdPadre = n.Id AND f.Lavoro = n.Lavoro

Es con <>:
- Selezionare studenti che vivono nella stessa provincia dello studente con matricola 71346 escluso lo studente stesso.
- Procedimento 1:
	- Select:
		- *
	- From:
		- Studenti
	- Where:
		- Provincia = (
			- Select:
				- Provincia
			- From:
				- Studenti
			- Where:
				- Matricola <>'71346')
- Procedimento 2:
	- Select 
		- Altri.*
	- From:
		- Studenti s JOIN Studenti Altri USING (Provincia)
	- Where:
		- s.Matricola = '71346' AND Altri.Matricola <> '71346'

Es con EXIST:
- Studenti con voto maggiore a 27.
- Procedimento 1:
	- Select:
		- *
	- From:
		- Studenti.s
	- Where:
		- EXIST (
			- Select:
			- From:
				- Esami e
			- Where:
				- e.Voto >27 AND e.candidato = s.Matricola)
- Procedimento 2:
```sql
	Select DISTINCT s.*
	From: Studenti s JOIN Esami e ON s.Matricola = e.Candidato
	Where: e.voto > 27
```


Es: 
- Cancella gli studenti che non hanno sostenuto esami
```sql
Delete from Studenti
Where Matricola NOT IN (Select Candidati
					   From Esami)
```
Oppure 
```sql
DELETE FROM Studenti S
WHERE NOT EXISTS (SELECT *
				 FROM Esami e
				 WHERE s.Matricola = e.Candidato)
```


### Creazione schemi.
Tabelle:
- Base:
	- I **metadati** appartengono allo schema.
	- I dati vengono fisicamente memorizzati.
- Viste:
	- I **metadati** sono presenti nello schema.
	- I dati non sono fisicamente salvati ma sono il risultato di un'espressione.

Le tabelle di base sono create con il comando **CREATE TABLE** e va specificato:
- Nome
- Tipo di dato:
	- Predefinito
	- Definito dall'utente (si chiamano domini e si creano con il comando **CREATE DOMAIN):
		- ```CREATE DOMAIN NomeDominio AS Nometipo ```


ES IMPO: Prendere la provincia con la media più grande (massima)
```sql
SELECT Provincia
FROM MediaProvincia
WHERE Media = (SELECT MAX(Media)
			  FROM MediaProvincia)
```


```sql 
CREATE VIEW StezzaRazza(Idf, Padre, Madre, Razza) 
AS  SELECT f.Cod, p.Cod, m.Cod, f.Razza
	FROM Cani f JOIN Cani m ON f.Madre = m.Cod JOIN Cani p ON f.Padre = p.Cod
	WHERE f.Razza = m.Razza AND f.Razza = p.Razza
SELECT a.Nome
FROM StessaRazza c JOIN StessaRazza m ON c.Madre = m.Idf JOIN StessaRazza p ON c.Padre = p.Idf JOIN Cani ca ON c.Idf = ca.Cod
```

La VIEW rimane nel database fino a quando non si usa una DROPVIEW.
Al contrario usare il costrutto WITH permette di fare la stessa cosa ma la tabella che crea viene eliminata subito dopo aver finito la select


```sql
SELECT s.*
FROM Studenti s
EXCEPT
SELECT s.*
FROM Studenti s JOIN Esami e ON s.Matricola = e.Candidato
WHERE e.Voto<>30
```


Per ogni pizza sotto i 9 euro e ordinata almeno una volta, restituire il nome della pizza, il nome del cliente che l'ha ordinata il maggior numero di volte e il numero di volte ordinata da quella persona. il tutto deve essere ordinato rispetto al nome della pizza.
```sql
WITH pizzeEconomiche(Codpizza, Nomepizza, Nomecliente, Numerovolte)
AS SELECT pi.Codpizza, pi.Nomepizza, o.Nomecliente, COUNT(*)
  FROM pizze pi JOIN ordini o USING(CodPizza)
  WHERE pi.Prezzo < 9
  GROUP BY pi.Codpizza, pi.Nomepizza, o.Nomecliente;
  
```


--Diminuire il prezzo del 10% delle pizze cui costo di produzione
--(costo di tutti gli ingredienti e la loro quantità) è inferiore 
---del 50% del prezzo della pizza
????

``` sql
UPDATE pizze
SET prezzo = prezzo * 0.9
WHERE codpizza IN(SELECT 
				 FROM pizze pi JOIN ricette r USING(codpizza) JOIN ingredienti i USING(codingrediente)
				 GROUP BY pi.codpizza, pi.prezzo
				 HAVING SUM(r.quantita = i.costobase) < pi.prezzo/2)
```
