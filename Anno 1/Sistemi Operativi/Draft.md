
es: 
- 1024 pagine
- overhead = 5ns
- si usa rtb da 32 da 1ns
- quanto hit rate ho bisogno per avere un overhead medio di 2ns
- il tempo medio è prob. di info in tlb * 1ns + miss * 5ns = 2ns 
- Ris: prob tlb = 0.75


22.11
File System:
- Organizza i file e gestisce l'accesso
- Dovrebbe essere indipendente dal dispositivo.
- Gestione dei guasti e sicurezza:
	- Funzionalità di backup e ripristino per prevenire perdita o corruzione di dati.
	- Funzionalità di crittografia e de-crittografia
- Directory: 
	- Contiene le informazioni dei file del System per la loro gestione e organizzazione.
	- Organizzazione:
		- In modo piatto:
			- Senza gerarchia, più semplice, tutto in una lista.
			- Ricerca lineare e i file devono avere nomi diversi.
		- Ad albero:
			- Gerarchico, più complesso.
			- Il nome è definito dal path quindi si possono avere nomi uguali e comunque non avere problemi.
- Metadata.
	- L'operazione open restituisce un descrittore di file (indice intero non negativo alla tabella dei file aperti).
	- L'operazione mount combina più file system in un unico spazio dei nomi, in modo che possano essere riferiti da una singola directory.
		- Assegna una directory chiamata punto di mount.
		- Il file system li gestisce con apposite tabelle di mount points.
		- Si possono fare soft links ma non hard links.

es:
	B: 6       5
	E: 8        4
	A: 10     3
	C: 2       2
	D: 4       1

 RR:
- quanto= 2min
	- B->E->A->C->D->B->E->A->D->B->E->A->E->A->A
	- Turnaround: 
		- A: 30
		- B: 20
		- C: 8
		- D: 18
		- E: 26
	- Turnaround medio: 
		- (26+20+8+18+30)/5 = 20.4min
Scheduling con priorità:
- B->E->A->C->D
- Turnaround:
	- A: 24-14 = 10
	- B: = 6
	- C: = 2
	- D: = 4
	- E: = 8
- turnaround totale:
	- (10+6+2+4+8)/5 = 30/5 = 6min 