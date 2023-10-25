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
	-Gestito in tempo di esecuzione dal sistema e mantiene la lista dei thread bloccati e la lista di quelli pronti.
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


24/10
