
**MIPS**:
L'architettura **MIPS** (Microprocessor without Interlocked Pipeline Stages) è una nota architettura di set di istruzioni (ISA) utilizzata in numerosi processori e sistemi embedded. È stata originariamente sviluppata da MIPS Computer Systems Inc. negli anni '80 ed è nota per la sua semplicità ed efficienza. Di seguito, ti fornirò una panoramica delle principali caratteristiche dell'ISA dell'architettura MIPS:

1. **Tipo di architettura**: MIPS è un'architettura RISC (Reduced Instruction Set Computer), il che significa che si basa su un set di istruzioni relativamente piccolo, ma altamente ottimizzato, per eseguire le operazioni di base. Questa scelta consente una maggiore velocità e una progettazione del processore più semplice rispetto alle architetture CISC (Complex Instruction Set Computer).

2. **Registri**: MIPS utilizza un set di 32 registri generali a 32 bit, numerati da $0 a $31. I registri $0 a $31 hanno ruoli specifici e alcune convenzioni particolari, ad esempio, $0 viene sempre impostato a zero e non può essere modificato, $31 è spesso utilizzato come link return address per le chiamate alle funzioni, ecc.

3. **Formato delle istruzioni**: Le istruzioni MIPS sono tutte di lunghezza fissa di 32 bit. Esistono tre formati principali di istruzioni: R (register), I (immediate), e J (jump).

   - Le istruzioni di formato R coinvolgono tre registri e vengono utilizzate per operazioni aritmetiche e logiche.
   - Le istruzioni di formato I coinvolgono due registri e un valore immediato e sono utilizzate per operazioni di carico/store e alcune operazioni aritmetiche.
   - Le istruzioni di formato J sono utilizzate per salti (jump) e il loro indirizzo di destinazione è specificato nei bit dell'istruzione.

4. **Accesso alla memoria**: L'architettura MIPS ha un modello di memoria load/store, il che significa che le operazioni di accesso alla memoria devono passare attraverso i registri. Ciò consente un maggiore controllo e predicibilità delle operazioni di memoria.

5. **Pipeline**: MIPS è noto per il suo approccio pipeline efficace che divide l'esecuzione delle istruzioni in diverse fasi, permettendo al processore di eseguire più istruzioni contemporaneamente e migliorando la velocità complessiva del processore.

6. **Convenzioni di chiamata**: MIPS ha convenzioni di chiamata standard per le funzioni, ad esempio, specifica quali registri devono essere utilizzati per passare argomenti e restituire valori di ritorno.

L'architettura MIPS è stata utilizzata in vari contesti, dai processori per computer a uso generale ai microcontrollori per dispositivi embedded. La sua eleganza e semplicità l'hanno resa una scelta popolare in molti ambiti di applicazione. È importante notare che ci sono diverse varianti dell'architettura MIPS, come MIPS32 e MIPS64, che differiscono per la dimensione dei registri e altre caratteristiche specifiche.


**ISA**:
La **ISA** (Instruction Set Architecture), tradotta in italiano come "Architettura del Set di Istruzioni", è un insieme di istruzioni che definiscono le operazioni che un processore o un'architettura di computer può eseguire. In altre parole, la ISA specifica l'insieme di comandi che un processore può comprendere e interpretare per eseguire varie operazioni, come operazioni aritmetiche, logiche, di controllo e di gestione della memoria.

La ISA svolge un ruolo cruciale nella progettazione dei processori e degli altri componenti hardware che compongono un sistema informatico. Essa crea l'interfaccia tra il software e l'hardware, consentendo ai programmatori di scrivere codice in linguaggi di programmazione ad alto livello, come C o Python, che poi viene tradotto in istruzioni specifiche del processore dalla fase di compilazione o interpretazione.

L'ISA può variare notevolmente da un'architettura a un'altra. Le diverse famiglie di processori, come x86, ARM, MIPS, PowerPC, ecc., hanno ISA diverse. Ogni ISA ha il suo set unico di istruzioni con formati specifici e regole per l'esecuzione delle operazioni. Ciò significa che un programma scritto per una ISA particolare non può essere eseguito direttamente su una CPU con un'ISA diversa senza alcuna forma di traduzione o interpretazione.

Le scelte fatte nella progettazione di un'ISA possono influenzare le prestazioni, l'efficienza energetica, la complessità del processore e altre caratteristiche cruciali del sistema informatico. Pertanto, la progettazione dell'ISA è una delle fasi fondamentali nello sviluppo di un nuovo processore o di un nuovo sistema embedded.


**Registri**:
Nell'informatica, ISA (Instruction Set Architecture) si riferisce all'insieme di istruzioni che un processore o un'architettura di computer può eseguire. Un registro del ISA (o registro dell'architettura) è una piccola memoria interna al processore che viene utilizzata per archiviare dati temporanei e per eseguire operazioni. I registri sono elementi chiave di un'architettura di computer e svolgono un ruolo cruciale nell'esecuzione delle istruzioni del programma.

I registri del ISA sono in genere molto veloci da accedere rispetto alla memoria principale, quindi vengono utilizzati per conservare dati che devono essere utilizzati frequentemente o per effettuare operazioni aritmetiche e logiche. Di seguito, sono elencate alcune tipiche caratteristiche dei registri del ISA:

1. **Registri generali**: Questi sono registri utilizzati per immagazzinare dati temporanei e indirizzi di memoria. Sono spesso utilizzati nelle operazioni aritmetiche e logiche di base e per memorizzare i risultati intermedi delle istruzioni.

2. **Contatori di programma**: Un registro speciale utilizzato per memorizzare l'indirizzo di memoria dell'istruzione successiva da eseguire. Viene aggiornato automaticamente dal processore man mano che vengono eseguite le istruzioni.

3. **Registri di stato**: Questi registri tengono traccia dello stato del processore e delle condizioni risultanti dalle istruzioni precedenti, ad esempio, il flag di zero (Z), il flag di carry (C), etc.

4. **Puntatori**: Registri utilizzati per tenere traccia di indirizzi di memoria specifici o di puntatori a dati o funzioni.

5. **Registri di controllo**: Registri utilizzati per configurare il comportamento del processore o per abilitare/disabilitare determinate funzionalità.

6. **Registri a uso specifico**: A seconda dell'architettura, potrebbero essere presenti registri specializzati per scopi particolari, come registri di gestione delle eccezioni, registri per operazioni in virgola mobile, ecc.

L'insieme, il numero e la dimensione dei registri del ISA variano a seconda dell'architettura del processore. I registri svolgono un ruolo fondamentale nella velocità e nell'efficienza delle operazioni di un processore, poiché riducono la necessità di accedere frequentemente alla memoria principale, che è significativamente più lenta rispetto all'accesso ai registri interni.


**Linguaggio Assembly**:
Il linguaggio Assembly è un linguaggio di programmazione a basso livello che fornisce un'interfaccia diretta con l'architettura hardware di un computer o di un processore. Esso utilizza un set di istruzioni mnemoniche simboliche per rappresentare le operazioni eseguite dal processore. Ogni istruzione Assembly corrisponde a un'istruzione di livello macchina che il processore può eseguire direttamente.

Le caratteristiche principali del linguaggio Assembly includono:

1. **Mnemoniche**: Le istruzioni Assembly sono rappresentate da nemotechnie, cioè abbreviazioni di parole chiave che rendono le istruzioni più leggibili rispetto al codice binario. Ad esempio, invece di utilizzare codici binari complessi, come "0101001100100010", è possibile utilizzare una nemotecnia come "ADD" per rappresentare un'operazione di somma.

2. **Operazioni elementari**: Il linguaggio Assembly fornisce istruzioni per operazioni di base supportate direttamente dal processore, come operazioni aritmetiche (somma, sottrazione, moltiplicazione, divisione), operazioni logiche (AND, OR, XOR, NOT), e operazioni di movimento dei dati tra registri e memoria.

3. **Registro-centrico**: Le istruzioni Assembly coinvolgono spesso l'uso di registri della CPU. I registri sono piccole memorie veloci che possono essere utilizzate per memorizzare dati temporanei. Le istruzioni Assembly spesso specificano quali registri devono essere coinvolti in un'operazione.

4. **Struttura sequenziale**: Il codice Assembly è scritto come una sequenza di istruzioni che vengono eseguite una dopo l'altra. La capacità di realizzare strutture di controllo (come cicli e condizioni) è fornita attraverso istruzioni di salto condizionato o incondizionato.

5. **Accesso diretto alla memoria**: Il linguaggio Assembly consente un accesso diretto alla memoria, permettendo di caricare e salvare dati dalla RAM o da altri dispositivi di memoria.

Tuttavia, scrivere programmi in linguaggio Assembly può risultare complesso e richiedere una conoscenza dettagliata dell'architettura hardware specifica del processore target. Inoltre, il codice Assembly è spesso meno portabile rispetto ad altri linguaggi di programmazione ad alto livello, poiché deve essere adattato alle caratteristiche specifiche del processore su cui verrà eseguito.

Oggi, l'uso del linguaggio Assembly è meno comune nelle applicazioni quotidiane e viene spesso utilizzato solo in contesti particolari, come nell'ottimizzazione di codice, nella programmazione embedded o nei sistemi operativi dove la precisione e il controllo a livello di hardware sono critici. La maggior parte dello sviluppo software viene svolto utilizzando linguaggi di programmazione ad alto livello, che offrono una maggiore astrazione e portabilità.


**Registri del MIPS**:
Nell'architettura MIPS (Microprocessor without Interlocked Pipeline Stages), ci sono 32 registri a 32 bit disponibili per l'utilizzo del processore. I registri vengono indicati con il prefisso "$", seguito dal numero del registro. Di seguito sono elencati i registri MIPS:

1. **Registri generali (R0 - R31)**:
   - $0 ($zero): Questo registro ha sempre il valore zero. Non può essere modificato e viene utilizzato per rappresentare il valore costante zero.
   - $1 ($at): Registro riservato all'assembler (assembler temporary). È utilizzato dall'assemblatore per temporanei.
   - $2 ($v0), $3 ($v1): Registri di valore di ritorno. I valori di ritorno delle funzioni vengono memorizzati in questi registri.
   - $4 ($a0) - $7 ($a3): Registri degli argomenti. Utilizzati per passare i primi quattro argomenti alle funzioni.
   - $8 ($t0) - $15 ($t7): Registri temporanei. Possono essere utilizzati per immagazzinare dati temporanei.
   - $16 ($s0) - $23 ($s7): Registri di salvataggio. Possono essere utilizzati per memorizzare dati importanti durante l'esecuzione delle funzioni.
   - $24 ($t8), $25 ($t9): Altri registri temporanei.
   - $26 ($k0), $27 ($k1): Registri riservati al kernel del sistema operativo.
   - $28 ($gp): Puntatore globale. Utilizzato per puntare alla sezione dei dati globali.
   - $29 ($sp): Puntatore dello stack. Puntatore all'ultimo elemento dello stack.
   - $30 ($fp): Puntatore del frame. Utilizzato come frame pointer per accedere alle variabili locali delle funzioni.
   - $31 ($ra): Return address. Contiene l'indirizzo di ritorno delle chiamate di funzione.

2. **Registri di stato**:
   - LO ($lo): Parte inferiore del risultato di una moltiplicazione o divisione.
   - HI ($hi): Parte superiore del risultato di una moltiplicazione o divisione.
   
3. **Registri di controllo**:
   - PC ($pc): Contatore di programma. Contiene l'indirizzo dell'istruzione in esecuzione.
   - HI ($hi) e LO ($lo): Registri di stato utilizzati per operazioni aritmetiche speciali, come la moltiplicazione e la divisione.

Questi 32 registri costituiscono l'insieme di registri generali disponibili nel processore MIPS e vengono utilizzati per eseguire le operazioni del programma.
![[Pasted image 20230727155708.png]]


**Le 8 idee alla base del progetto dei calcolatori**

1. Considerare la legge di Moore
	- Bisogna prevedere dove sarà arrivata la tecnologia al **termine** della progettazione di un calcolatore e non al momento in cui si inizia.
2. Usare l'astrazione
	- L'astrazione permette la creazione di diversi livelli su cui la macchina funziona in modo da offrire un livello superiore (su cui si lavora normalmente) semplificato. Lavorare in linguaggio macchina sarebbe molto difficile e per questo si utilizzano compilatori che, in base all'ISA specifico della macchina su cui viene usato, traduce il linguaggio ad alto livello (HLL) in linguaggio macchina.
3. Common case fast
	- Velocizzare anche di poco un processo che capita frequentemente tende a dare risultati migliori che velocizzare anche di molto un processo che avviene raramente. (per questo abbiamo bisogno del calcolo delle performance)
4. Parallelismo
	- Svolgere più operazioni contemporaneamente premette di aumentare il volume di lavoro.
5. Pipelining
	- La quantità di lavoro può essere migliorata se si opera in serie, come una catena di montaggio.
6. Predizione
	- Certe volte conviene cercare di predire il prossimo processo e farlo, col rischio di sbagliare, che aspettare la conferma di quello che serve fare davvero. Con metodi di predizione migliori si possono aumentare di molto la velocità.
7. Gerarchia di memoria
	- Quantità, prezzo e velocità della memoria non sono compatibili ma possiamo avere un compromesso ottimale organizzando la memoria in modo gerarchico (memoria più veloce ma costosa più vicina alla CPU e per dati momentanei e memoria più economica e in abbondanza più lontana dalla CPU e per dati da salvare a lungo termine).
8. Dependability via redundancy
	- I computer devono essere anche dependable (tolleranti ai guasti) e aumentare la rindondanza (il numero) di alcuni componenti permette di rivelare anomalie e avere componenti di backup per quelli malfunzionanti.