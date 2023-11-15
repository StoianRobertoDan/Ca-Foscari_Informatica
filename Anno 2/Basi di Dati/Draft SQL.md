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