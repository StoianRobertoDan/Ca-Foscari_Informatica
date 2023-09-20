
**Eccezioni e interruzioni**
Il flusso delle istruzioni può cambiare anche per altre cause oltre che i salti, come:
- Eccezioni: salto a causa della CPU. Sono eventi sincroni, generati internamente al processore e provocati da problemi nell'esecuzione delle istruzioni.
- Interruzioni: salto a causa è esterna (I/O). Sono eventi asincroni, generati esternamente al processore e provocati dalle periferiche.

Per gestire le eccezioni e le interruzioni:
- Si interrompe l'esecuzione del programma corrente.
- Si salva lo stato di esecuzione del programma corrente (il PC viene salvato nel Exception Program Counter EPC)
- Si trasferisce il controllo al sistema operativo (con un salto) modificando il PC ad un valore specifico e una volta risolto si riprende l'esecuzione del programma dal PC precedentemente salvato). Se non può tornare all'esecuzione del programma precedente lo termina.

Ci sono 2 approcci per capire i tipi di eccezioni e interruzioni:
- Si utilizza un registro speciale che contiene i codici per i vari tipi di eccezioni. Ha un singolo entry point nel sistema operativo. Il MIPS usa questo approccio grazie al CAUSE register.
- Si utilizzano salti diversi per eccezioni diverse. Questo metodo si chiama **Vectorized interrupts** e ha diversi entry points nel sistema operativo.

Il MIPS ha un approccio minimale e salva solo il PC mentre il resto, se serve, deve essere gestito dal Sistema Operativo. Altre CPU (come CISC) effettuano un salvataggio esteso.

Nella pipeline c'è bisogno di un control hazard specifico.
- Occorre annullare le istruzioni già entrate nella pipeline inserendo delle nop.
- Le eccezioni aritmetiche vengono rilevate nello stadio EXE di conseguenza anche quello stadio ha bisogno di poter immettere stalli nella CPU.
- Nella pipeline più istruzioni possono generare eccezioni nello stesso ciclo di clock e per tale motivo ci deve essere un sistema di priorità delle istruzioni.
- Le interruzioni, essendo asincrone e non associate ad un'istruzione specifica, possono essere gestite con più flessibilità.
- Eccezioni possono essere generate anche dal sistema operativo. Ha la possibilità di disabilitare le eccezioni/interruzioni per brevi periodi.


Esercizio di ottimizzazione del codice:
![[Pasted image 20230803224411.png]]

Assumiamo che sono implementati forwarding e register file ottimizzato.
Individuiamo un'istruzione da usare nel delay shot e riduciamo gli stalli.

Dipendenze RAW:
- lw -> addi $t0 -> sw
	- La lw scrive t0 alla fine del 4° ciclo mentre addi ha bisogno di leggerlo all'inizio del 3°. addi è successivo nella pipeline e il 4° ciclo della lw coincide con il 3° ciclo della addi ma sottolineiamo che lw scrive t0 alla **FINE** del ciclo mentre addi ne ha bisogno all'**INIZIO**.
	- addi scrive t0 alla fine del 3° ciclo e sw ne ha bisogno all'inizio del 4° quindi non ci sono stalli.
- addi $s1 -> bne
	- addi scrive s1 alla fine del 3° ciclo e bne deve leggerlo al 2° (perché il register file è ottimizzato). bne è 2 istruzioni più avanti per cui il suo 2° ciclo equivale al 4° della addi quindi non ci sono stalli.
Dipendenze WAR (no stalli ma non si possono scambiare di posto):
- lw -> addi $s0
- sw -> assi $s1

Primo punto: possiamo spostare la addi $s1 sotto la bne per riempire il delay shot.
![[Pasted image 20230803230816.png]]

una volta riempita il delay shot però abbiamo uno stallo tra addi $s0 e bne, essi infatti sono successivi uno all'altro e si pone il problema che inizialmente non c'era.

Inseriamo quindi i nop necessari per non creare stalli:![[Pasted image 20230803232813.png]]

Si possono spostare istruzione al posto delle nop?
Spostare addi $s0 al posto della prima nop è possibile perché la dipendenza con lw è di tipo WAR e non crea stalli e allo stesso tempo si allontana addi dalla bne con cui aveva creato uno stallo, risolvendo entrambe le nop in un solo spostamento.
![[Pasted image 20230803233723.png]]

Questi sono i seguenti diagrammi di esecuzione pre-ottimizzazione e post-ottimizzazione: 
![[Pasted image 20230803233854.png]]
![[Pasted image 20230803233908.png]]


**Processori superscalari**
Abbiamo visto che attraverso la pipeline possiamo usare il parallelismo per:
- Ridurre il tempo di clock (al tempo dello stage più lento) 
- Ottenere una CPI (cicli per istruzione) pari a 1 (per ogni ciclo finisce un'istruzione) e uno speedup maggiore (speedup teorico pari al numero di stage).

Per aumentare ancora di più il parallelismo ci sono 2 possibilità:
- Aumentare la profondità della pipeline (più stadi) per eseguire più istruzioni in parallelo. Bisogna in ogni caso bilanciare equamente il lavoro tra stadi.
- Replicare i componenti in modo da poter immettere più istruzioni alla volta nella pipeline (**multiple issue**).

Multiple issue ha 2 approci:
- Static: sfrutta il compilatore per raggruppare istruzioni da inserire contemporaneamente in un issue packet. Il compilatore deve evitare possibili hazard tra le istruzioni. Un esempio potrebbe essere inserire 3 *add* non dipendenti se si hanno 3 ALU. 
	- Vantaggi:
		- Il compilatore è colui che impiega più tempo nel analizzare le istruzioni ma dà anche la possibilità di ottimizzarlo in modo più sofisticato.
		- Una volta ottimizzato il compilatore le migliorie verranno sempre applicate invece nella CPU l'ottimizzazione dovrebbe avvenire ad ogni esecuzione.
		- Il Branch prediction (e anche parte del hazard detector) sono gestite dal compilatore e non dalla CPU, risparmiando transistor che potranno essere usati per altro (come altri stadi).
	- Svantaggi:
		- Non tutti gli stalli sono predicibili in compile time.
		- Il compilatore non può speculare in modo efficace sul risultato delle branch (no Dynamic Branch Prediction).
		- Il codice prodotto dipende sia dalla ISA che dalla specifica CPU perché profondità di pipeline diverse richiede compilazioni diverse del codice.
- Dynamic: decide quali e quante istruzioni immettere nella pipeline (CPU **Superscalare**):
	- Invio **in-order**: la CPU decide solo quante istruzioni inviare ad ogni ciclo di clock, ma l'ordine rimane lo stesso.
	- Invio out-of-order: la CPU decide l'ordine delle istruzioni prima di raggrupparle e immetterle nella pipeline per massimizzare il parallelismo.
	- Divisione in 3 macro unità:
		- Fetch & issue unit: unià che legge diverse istruzioni e le distribuisce dinamicamente.
		- Functional units: unità in parallelo che eseguono le istruzioni.
		- Commit unit: unità finale che si occupa di salvare i dati (WB) in modo che la semantica non venga alterata (questo risolve tutte le dipendenze WAW e WAR).