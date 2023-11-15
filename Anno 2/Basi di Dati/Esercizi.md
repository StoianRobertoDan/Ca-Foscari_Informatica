- Query per ricavare il codice degli utenti che hanno in prestito SOLO libri di fisica (cioè abbia "fisica" nella descrizione bibliografica).

Libri di fisica = LF =  $\pi(\delta_{standard = 'fisica'}(Termini) \rhd\lhd Indicizza \rhd\lhd DescrizioneBib \rhd\lhd_{Codice = CodDesc} Documenti)$
Utenti con un libro = UL = $\pi_{CodUtente, CodDesc}(Prestiti \rhd\lhd Documenti)$
Utenti con libri di fisica = UF = $\pi{CodUtente}(prestiti)\times LF$
Utenti con SOLO fisica = $\pi_{Codice}(Utenti) - (\pi_{CodUtente}(UL - UF))$
(UL - UF) toglie della tabella UL tutte le enduple che hanno libri di fisica. Rimangono così solo gli studenti che hanno ALMENO un libro non di fisica.

- Query per ricavare il codice degli utenti che hanno in prestito TUTTI libri di fisica (cioè abbia "fisica" nella descrizione bibliografica).

Usiamo LF e UL dell'esercizio precedente.
Basta fare $UL\div LF$  se $LF\ne0$ 

Se $LF=0$ :
	$\pi_{Codice}(Utenti) - (\pi_{Codice}(Utenti)\times LF-\rho_{CodUtente\leftarrow Codice}(UL))$

- Query per ricavare il codice degli utenti che hanno in prestito ESATTAMENTE TUTTI i libri di fisica (cioè abbia "fisica" nella descrizione bibliografica).

Dati gli esercizi di prima abbiamo Solo_Fisica e Tutto_Fisica.
Basta quindi prendere l'intersezione Solo_Fisica $\cap$ Tutto_Fisica.

- Query per avere gli Utenti (Nome, Cognome, Codice) che hanno preso in prestito più di 3 libri.

Numero libri = NL = $\rho_{count(*)\leftarrow numerolibri}(CodUtente\gamma_{count(*)}(Prestito))$
Utenti con più di 3 libri = $\pi_{CodUtente, NomeCognome}(\delta_{NumeroLibri>3}(NL\rhd\lhd_{CodUtente = Codice}Utenti))$

- Autori che hanno scritto il MASSIMO numero di libri

AL = $\rho_{count(*)\leftarrow numlibro}(Codice, NomeCognome \gamma{count(*)}(Autori \rhd\lhd_{Codice=CodAutore}))$
M = $\gamma_{max(numerolibri)}(AL)$ (lasciando vuoto prima si crea un unico gruppo)
Autori con max libri scritti = $\pi_{Codice, NomeCognome}(\delta_{numerolibri = M}(AL))$
