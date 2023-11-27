Es C:
- Aeroporti (Città, Nazione, NumPiste)
- Voli (codVolo_, GiornoSett_, CittaPart*, OraPart, CittaArr*, OraArr, TipoAereo*)
	- CittaPart FK(Aereoporti) 
	- CittaArr FK(Aereoporti) 
	- TipoAereo FK(Aerei)
- Aerei(TipoAereo, NumPasseggeri, QtaMerci)

1. Troviamo il numero di voli internazionali che partono giovedì da Napoli
```sql
SELECT *
FROM Voli v JOIN Aeroporti a ON v.CittaArr = a.Citta
WHERE v.CittaPart = 'Napoli' AND a.Nazione<>'Italia' AND v.GiornoSett = 'Giovedi'
```
Scrivere il calcolo relazionale:
$$\gamma\ count(*) (\sigma_{CittaPort='Napoli'\wedge GiornoSett='giovedì'}(Voli)\rhd\lhd_{CittaArr=Citta}\sigma_{Nazione<>'Italia'}(Aeroporti)$$

2. Cancellare gli aereoporti di cui non si conosce il numero delle piste e i voli che hanno come partenza o arrivo tali aereoporti.
```sql
DELETE FROM Voli
WHERE CittaPart IN (SELECT Citta
				  FROM Aeroporti
				  WHERE Num.Piste IS NULL)
	OR CittaArr IN (SELECT Citta
				  FROM Aeroporti
				  WHERE Num.Piste IS NULL)

DELETE FROM Aeroporti
WHERE Num.Piste IS NULL
```
Se si cancella prima gli aeroporti e poi i voli si riceve un messaggio di errore per "violazione dei vincoli di integrità referenziali" perché in Voli ci sono le **chiavi esterne** che punterebbero, dopo la delete, a indirizzi inesistenti.

3. Restituire le citta francesi da cui partono più di venti voli alla settimana diretti in Italia.
```sql
SELECT v.cittaPart
FROM Voli v JOIN Aeroporti p ON v.CittaPart = p.Citta JOIN Aeroporti a ON v.CittaArr = a.Citta
WHERE p.Nazione = 'Francia' AND a.Nazione = 'Italia'
GROUP BY v.CittaPart
HAVING count(*) > 20
```

4. Restituire gli aereoporti italiani che hanno solo voli interni. Risolvere questa query in due modi diversi: 
	- utilizzando operatori insiemistici 
	- con una sottoselect.
```sql
SELECT Citta
FROM Aeroporti
WHERE Nazione = 'Italia'
EXCEPT 
SELECT v.CittaPart AS Citta
FROM Voli v JOIN Aeroporti a ON v.CittaArr = a.Citta
WHERE a.Nazione<>'Italia'
```
(Nella prima select prendo tutte le città italiane e si sottrae la seconda select che prende tutte le citta che hanno voli fuori dall'Italia)
```sql
```