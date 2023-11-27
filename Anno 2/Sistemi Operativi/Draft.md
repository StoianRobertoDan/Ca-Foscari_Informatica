Processi:
- Descrittore di processi dentro il blocco di controllo
- Necessità di possibilità di sospensione dei processi per aspettare la fine di un'istruzione come stampa/richiesta input ecc.
- 


17/10
Cambiare threads costa meno che cambiare processo perchè ci sono informazioni condivise tra threads che non vanno passati.

Stati del thread principali: Pronto, in esecuzione, bloccato. In particolare:
- Born (nato)
- Ready (pronto all'esecuzione)
- Running (in esecuzione)
- Dead (terminato)
- Blocked (bloccato da un evento I/O)
- Waiting (bloccato da un evento di un altro thread)
- Sleeping (bloccato per un determinato tempo)

Package di threads (Pthread)

Threading di diversi tipi:
- Threads a livello utente:
	- Processi con vari thread a livello utente. Modello molti (thread a livello utente) a 1 (a livello nucleo)
	- Creati a livello di esecuzione.
	- Non possono accedere alle strutture del nucleo
	- Ha più thread a livello utente ma solo uno a sistema operativo (uno per processo)
	- Vantaggi:
		- Si può definire uno scheduler a livello utente che può essere manipolato e modificato per essere ottimizzato
		- Se i thread devono comunicare o sincronizzarsi è più falice
		- Posso usare un sistema operativo che non è multithreating come se lo fosse
	- Possibile avere un processo con più thread o più processi (relativi allo stesso) con un thread ciascuno. La seconda permette di avere un parallellismo sia a livello superiore che inferiore.
	- Ogni descrittore di thread è raggruppato nella tabella di thread.
	- Gestito in tempo di esecuzione dal sistema e mantiene la lista dei thread bloccati e la lista di quelli pronti.
- Threads a livello kernel:
	- Modello con mapping di thread 1 a 1.
	- Lo scheduler agisce a livello più basso. Questo lo rende più efficiente ma anche meno flessibile.
	- Se un thread si blocca può scegliere di eseguirne un altro.
	- C'è una tabella dei processi e una dei thread nel nucleo.
- Threads combinati a livello utente e kernel:
	- Modello con mapping molti a molti (numero di thread a livello utente e kernel solitamente diversi, con più a livello utente)
	- Thread pooling (una pool di...). Thread workers (permanenti a livello kernel) a cui vengono assegnati i nuovi thread creati
	- Scheduler permette alla libreria di decidere come assegnare i thread

Attivazione dello scheduler:
- Obbiettivo:
	- Minimizzare le funzionalità dei thread nucleo
	- Ottimizzare le prestazioni dei thread utente
- Serve evitare transizioni non neccessarie utente/kernel


18/10

Scheduling
- L'uso della priorità nello scheduling, abbassando o alzando in base alle neccessità per evitare starvation
- Bisogna definire quali processi fare prima se hanno una scadenza o sono in realtime
- Burst della CPU in base al loro bound:
	- Se il processore è CPU-bound ha burst di CPU lunghi con minori attese per l'I/O
	- Se il processore è I/O-bound ha burst di CPU corti con più attese per l'I/O
	- Spesso si passa da un bound all'altro in base alle neccessità. se un processo è prettamente di un tipo di bound, saperlo ci da diversi vantaggi sulla
- Sistemi Batch: Richiedono una quantità di lavoro senza l'interruzione dell'utente.
- Sistemi interattivi: Richiedono una maggiore interazione con l'utente.
- Sistemi Real-time
- Obbiettivi:
	- Massimizzare il throughput
	- Minimizzare la latenza 
		- non è sempre collegato al punto di prima, anzi certe volte sono in conflitto. Avere tanti processi produce throughput maggiore ma la latenza è alta. Al contrario avere pochi processi può produrre poco throughput ma la latenza essere bassa.
	- Prevenire la starvation (attese troppo lunghe/infinite)
	- Completare i processi entro la loro scadenza temporale.
	- Massimizza l'uso del processore.
	- (Non tutti questi punti sono sempre possibili e la scelta di quali punti vanno messi in primo piano dipende dai processi e dall'uso della macchina)

Diversi livelli di Scheduling:
- Alto livello:
	- Determina quale job può competere per l'uso delle risporse
	- Controllo il numero di 
- Livello intermedio:
	- Determina quali processi possono
- Basso livello:
	- Assegna priorità.
	- Decide quali processori sono usati dai processi.

Scheduling con e senza prelazione:
- Con prelazzione:
	- Si possono interrompere processi e possono essere rimossi dall'attuale processore (per assegnare quel processore ad un altro processo).
	- Si può avere un miglioramento del tempo di risposta.
	- Importante per ambienti *interattivi*
	- I processi soggetti a prelazione rimangono in memoria.
- Senza prelazione:
	- I processi vengono eseguiti fino al loro compimento
	- Questo può bloccare processi più importanti dal essere eseguiti.

Priorità:
- Statica:
	- La priorità assegnata ad un processo non cambia
	- Facile da implementare
	- Basso overhead
	- Non reattiva alle variazioni dell'ambiente.
- Dinamica:
	- Reattiva ai vambiamenti
	- Favorisce l'interattività
	- Richiede maggior overhead giustificato dalla maggior capacità di reagire.


Algoritmi di scheduling
- Decide per ogni processo:
	- Quando eseguirlo
	- Quanto a lungo tenerlo in esecuzione
- Fa scelte su:
	- Prelazione.
	- Priorità.
	- Tempo di esecuzione (tempo totale, dall'inizio alla fine. Non sempre facile da detterminare).
	- Tempo fino al completamento (tempo dal momento corrente a quello finale).
	- Equità (ogni processo viene considerato in modo uguale).
- Scheduling FIFO (first in first out):
	- Si inserisce in coda e si prende dalla testa della lista (processi trattati in base al tempo di arrivo).
	- è uno schema semplice ma meno utilizzato perchè poco ottimizzato
	- Non ha ne priorità dinamica ne prelazione.
- Scheduling SJF (shorter job first):
	- I processi con tempo minore ricevono una priorità maggiore e viene eseguito per primi.
	- Tempo di attesa medio minore del FIFO.
	- Ha potenzialmente una larga variazione nel tempo di attesa (è buono per la media ma certi processi rischiano attese molto lunghe).
	- Senza prelazione che può portare a tempi di risposta lenti a richieste interattive.
	- Si basa sulla stima del tempo necessario per i vari processi
		- La stima può essere stimata male (inaccurata) o falsata dal processo stesso
		- Tutti i tempi devono essere disponibili
- Scheduling SRT (Shortest remaining time first):
	- La versione con prelazione del SJF.
	- Si possono interrompere i processi in esecuzione per far eseguire processi appena entrati in coda ma che hanno un tempo minore.
	- Teoricamente ottimo a livello di tempo medio di attesa.
	- Ha una variazione sui tempi di attesa ancora maggiore rispetto alla SJF e c'è rischio di Starving per i processi più lunghi.
- Scheduling RR (Round-Robin)
	- Basato sulla FIFO
	- Ogni processo ha un tempo di esecuzione limitato e se non viene finito in quel periodo viene messo in coda.
	- Usa la prelazione ma non la priorità dinamica
	- Facile da implementare
	- Richiede per il sistema di mantenere in memoria parecchi processi per minimizzare l'overhead
	- Spesso usato come parte di algoritmi più complessi.
	- Spesso usato per sistemi interattivi.


25/10

Gestione della memoria:
- Gestione gerarchica:
	- Memoria cache:
		- Ha velocità molto alte e dimensioni molto ridotte viene usata per salvare i dati più usati. Se i dati richiesti sono presenti in cache si risparmia molto tempo grazie alla sua velocità di accesso ma serve ottimizzarla bene per far fronte alle dimensioni piccole (es con )
	- Memoria primaria:
		- Memorizzazione di dati e programmi neccessari al momento
	- Memoria secondaria:
		- Memorizzazione di file e programmi che non servono al momento
- Organizzazione:
	- Un processo può usare per intero la memoria
	- Ad un processo viene concessa una partizione della memoria che può essere:
		- Statica
		- Dinamica
- Gestione e ottimizzazione:
	-  Quale e quanta memoria riservare e per un determinato processo?

Allocazione:
- Contigua:
	- Il programma è salvato in un blocco unito.
	- Può essere impossibile se il blocco richiesto è troppo grande.
	- Basso overhead.
	- Versione Mono Utente:
		- Assenza di modello d'astrazione e controllo ad un solo utente.
		- Il S.O. non deve essere danneggiato (sovrascritto) e servono dei registri **Boundaries** che indica da dove inizia la memoria non usata dal S.O. e che può essere usata.
			- Per ogni azione si controlla che gli indirizzi di memoria non siano fuori dal registri limite
	- Overlay:
		- Tecnica che permette di dividere il programma in sezioni logiche e si memorizzano solo quelle in uso.
		- Ha una zona in cui si salva quella parte del programma sempre in uso e poi una zona di memoria in cui si possono caricare sezioni diverse quando servono (togliendo quella precedente).
		- Svantaggi:
			- Difficile organizzare la sovrapposizione (aka overlay) per usare la memoria primaria in modo efficiente.
			- Complica la modifica dei programmi.
		- Ha un fine simile alla memoria virtuale (usare più memoria di quella disponibile).
		- L'esempio usato prende un solo utente e un solo programma ma si possono avere più programmi salvati in blocchi diversi della memoria, ogni blocco diviso nella parte fissa del programma e nella parte dedicata all'overlay (Overlay su più programmi).
	- Multiprogrammazione a partizioni fisse:
		- In un processore I/O bound che aspetta molto spesso per delle risposte I/O si può pensare di far lavorare la CPU su altri processi mentre aspetta la risposta per un processo.
		- Il processore passa rapidamente tra un processo e l'altro dando l'illusione di simultaneità.
		- Serve una memoria maggiore e serve proteggere la memoria dall'accesso sbagliato durante il cambio del processo.
			- Quando viene eseguito un processo dentro una partizione serve salvare nei registri gli indirizzi di boundaries della partizione in esecuzione.
			- Se si cambia partizione serve salvare i nuovi limiti.
		- Svantaggi:
			- Le prime implementazioni usavano indirizzi assoluti:
				- Se la partizione era occupata, il codice non poteva essere caricato.
			- Si è passati a indirizzi ricolanti (con ):
				- Si crea una coda unica che distribuisce gli imput in tutte le partizioni di memoria.
				- Il job viene eseguito in una partizione purchè sia grande abbastanza.
					- Questo crea il problema che si può inserire nelle partizioni grandi processi che hanno bisogno di poca memoria e i processi grandi   devono aspettare che si liberino tali partizioni.
			- Frammentazione:
				- Le partizioni sono spesso più grandi dei processi ma la memoria libera non viene usata e quindi è sprecata.
			- ![[Pasted image 20231031142206.png]]
			- ![[Pasted image 20231031142140.png]]
	- Multiprogrammazione a partizioni variabili:
		- Le partizioni vengono create in base alle necessità (con la stessa grandezza dei processi che ci vanno dentro). 
		- Non si crea memoria non sfruttata dentro le partizioni ma se ne crea tra le partizioni quando i processi finiscono e sono in coda processi troppo grandi per i singoli spazi tra le partizioni.
		- Si può ottimizzare gli spazzi spostando le partizioni in nuovi indirizzi per accumulare gli spazzi liberi vicini in modo da usa.
		- Strategie di posizionamento della memoria:
			- First fit: si inserisce il processo nella prima zona disponibile abbastanza grande.
			- Best fit: si inserisce il processo nella zona disponibile che sprechi il minor spazio possibile.
			- Worst fit: si inserisce il processo nella zona con la maggiore memoria lasciano 
	- Multiprogrammazione con swapping:
		- La memoria principale è divisa in partizioni chiamate "swapping area" che contiene più processi contemporaneamente e le scambia periodicamente salvando quelli non in esecuzione in memoria secondaria.
	- Gestione della memoria con una "mappa di bit" dove ogni bit si riferisce ad un blocco della memoria e descrive se è occupato o libero o una lista dei blocchi liberi e occupati (con l'informazione H/P, inizio dei blocchi e dimensione).
- Non contigua:
	- Il programma è diviso in segmenti che possono essere salvati in punti diversi della memoria
	- Overhead maggiore


31/10
Memoria virtuale
- Permette di avere l'illusione di avere più memoria di quella disponibile
- Utilizza un MMU (Memory management unit), una componente HW per tradurre indirizzi virtuali in indirizzi reale:
	- ![[Pasted image 20231031145131.png]]
- Concetti: 
	- Spazio di memoria virtuale V
	- Spazio di memoria reale R
	- Meccanismo di Traduzione Dinamica dei indirizzi (Address) DAT
- Le pagine virtuali hanno indirizzi collegati alla memoria reale, certi collegamenti sono in memoria principale e altri invece hanno riferimenti in memoria secondaria. Ciò che è salvato in memoria primaria si può usare subito mentre quello che è presente solo in memoria virtuale deve essere caricato in memoria primaria, liberando spazio in memoria principale se serve.
- Mapping dei blocchi 


Varianti della FIFO:
- Second-Chance:
	- Esamina il bit di riferimento:
		- Se è 0 viene tolta
		- Se è 1 viene settato a 0 e rimessa in coda
- Ad orologio:
	- Come la SS ma a ciclo.

Modello Working Set:
- I processi lavorano nel tempo spesso sugli stessi sottoinsiemi di pagine. Possiamo quindi cercare di mantenere in memoria il sottoinsieme favorito dal programma.
- I processi mostrano località. Ogni processo usa un certo numero di pagine, è importante capire quante pagine dare ad ogni processo. Si segue l'utilizzo delle pagine del processo e una volta che si vede una stabilizzazione si usa quelle pagine come soglia cercando di diminuire il page fault.
- Il working set delle pagine del processo in un determinato momento è $W(t,w)$ con t il tempo e w l'intervallo di tempo.
	- L'insieme di pagine durante l'intervallo di tempo è $[t-w,w]$ 

Dimensione delle pagine:
- Se abbiamo pagine più piccole:
	- Avere minor frammentazione interna (se le pagine più piccole lo spazio sprecato nella memoria usata per un certo processo sarà minore).
	- Può coprire il working set con meno pagine perché le pagine scelte hanno meno informazioni che non vengono in realtà usate.
	- Minor spreco di memoria.
	- Tabella delle pagine più grandi.
- Se abbiamo pagine più grandi:
	- Riduce la memoria sprecata dalla frammentazione della tabella.
	- Ogni riga della TLB mappa una memoria più grande con più prestazioni.
	- Riduce il numero di operazioni I/O (?).
- Se abbiamo pagine di memoria di diversa grandezza:
	- Si può avere frammentazione esterna (può rimanere memoria sprecata tra le pagine quando una pagina viene tolta della memoria e si inserisce al suo posto una pagina più piccola).

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