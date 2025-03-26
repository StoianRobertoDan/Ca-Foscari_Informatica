```sql
SELECT s.Provincia
FROM Srudenti s JOIN Esami e ON s.matricola = e.Candidato
GROUP BY s.Provincia
HAVING AVG(e.Voto) >= ALL (SELECT AVG(e.Voto)
						  FROM Srudenti s JOIN Esami e ON s.matricola = e.Candidato
						  GROUP BY s.Provincia)

// al posto di questo si può usare le viste


```

Nome di ogni cane che ha entrambi i genitori e i loro genitori della sua stessa razza
```sql
CREATE VIEW StessaRazza (Figli, Padre, Madre, Razza)
AS  SELECT c.Cod, p.Cod, m.Cod, c.Razza
	FROM Cani c JOIN Cani p ON c.Padre = p.Cod JOIN Cabu m ON c.Madre = m.Cod
	WHERE c.Razza = p.Razza AND c.Razza = m.Razza
SELECT c.Nome
FROM Cani c JOIN SressaRazza f ON c.Cod = f.Figlio JOIN StessaRazza p ON f.Padre = p.Figlio JOIN StessaRazza m ON f.Madre = m.Figlio
```


