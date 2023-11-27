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