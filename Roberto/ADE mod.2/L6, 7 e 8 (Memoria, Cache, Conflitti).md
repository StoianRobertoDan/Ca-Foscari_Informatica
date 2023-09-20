
Tipologie di memorie:
- **SRAM** (Static Random Access Memory):
	- Memoria molto veloce.
	- Difficile da renderle capienti (6 transistor per ogni bit).
	- Consumo di energia elevate.
	- Non richiedono refresh, memorizzazione molto stabile ma solo finché riceve corrente.
	- La memoria che si usa dentro la CPU per i registri (va alla stessa velocità della CPU).
- **DRAM** (Dynamic Random Access Memory):
	- Memoria più lenta della SRAM.
	- Occupano meno spazio (1 condensatore e 1 transistor per ogni bit) e quindi più capienti.
	- Consumo di energia minore.
	- Possono dimenticare i dati nel tempo e perciò hanno bisogno di refresh a intervalli regolari (per dare comunque tempo per la lettura e la scrittura normale).
	- Hanno una struttura a griglia che permette il refresh di una intera riga alla volta (un ciclo di lettura e uno di scrittura).
	- **SDRAM** (Syncronized DRAM) che utilizza un clock sincronizzato con la CPU.
		- **DDR** (Double Data Rate) SDRAM possono trasferire sia durante la salita del clock che la discesa (raddoppio della banda).
- **NAND** (SSD memory): fanno parte delle memorie EEPROM (Electrically Erasable Programmable Read-only Memory) e usano i *floating-gate transistors*.
	- Significativamente più lente delle DRAM
	- Non richiedono il refresh.
	- I dati rimangono memorizzati anche in assenza di corrente.
	- 5 tipi diversi di memorie con velocità, costo e capacità diverse, differiscono per il numero di bit per cella (NAND SLC memorizza 1 bit per cella ed è la più veloce e costosa).
	- Problema di usura, riscrivere una cella di memoria molte volte la porta inevitabilmente a rompersi. Wear leveling è un controller che distribuisce le scritture in modo uniforme su tutta la memoria per evitare che alcune parti si consumino prima di altre.
- **Hard Disk**: 
	- Scrittura fisica su dischi magnetici in movimento, non adatti a dispositivi soggetti a vibrazioni.
	- Memoria molto lenta.
	- Estremamente capienti.
	- Molto economici.

![[main-qimg-1814b02d79a90243ac5050584618a5e9-lq.jpeg]]
**IOPS: Input / Output Operations Per Second**

**Gerarchia e località**
Non si può avere velocità, capacità e costo moderato contemporaneamente quindi la cosa migliore è usare diverse memorie per diversi scopi: gerarchia di memoria. L'importante è avere la memoria più veloce più vicina alla CPU.

Principio di località: un programma non accede a tutta la memoria con la stessa probabilità ma anzi accede ad una porzione relativamente piccola dello spazio di indirizzamento in un certo istante. I tipi di località sono:
- **Località temporale**: quando si fa riferimento ad un dato c'è più probabilità di far riferimento a quello stesso dato di nuovo in un certo periodo di tempo.
- **Località spaziale**: quando si fa riferimento ad un dato c'è più probabilità di far riferimento a dati che hanno un indirizzo vicino a quello corrente.

Il principio di località può essere utilizzato per rendere più efficiente l'accesso alla memoria.
I livelli più vicini alla CPU infatti è formato da sottoinsieme dei livelli sottostanti (copiati tra livelli adiacenti). Grazie al principio di località, copiando dalla memoria più lontana a quella più vicina alla CPU l'intera sezione di memoria che comprende il dato di cui abbiamo bisogno, c'è una certa probabilità che i prossimi dati a cui dovremmo accedere siano già stati copiati nella memoria più vicina. In questo modo sarà più veloce accedervi. Quando i dati richiesti dalla CPU sono già stati copiati ad un livello superiore parliamo di **hit**, altrimenti si parla di **miss**.
- La frazione di accessi alla memoria in cui ottengo una hit si chiama **hit rate** e vale:
	- Numero delle hit / numero degli accessi
- La frazione degli accessi alla memoria in cui ottengo una miss si chiama **miss rate** e vale:
	- Numero delle miss / numero degli accessi
	- 1 - hit rate
Dato che la memoria più vicina alla CPU è più veloce, hit e miss non vengono gestiti nello stesso tempo ma:
- **Hit time**: è il tempo di accesso al livello superiore della gerarchia insieme al tempo necessario per stabilire se l'accesso avrà un hit oppure un miss.
- **Miss penalty**: è il tempo necessario per recuperare il dato dalla memoria al livello inferiore insieme al tempo per copiare quel blocco (e in caso capire quale blocco sovrascrivere):


**CACHE**
Viene chiamato cosi ogni sistema di storage che sfrutta il principio di località degli accessi. Si usa il termine per la memoria che si trova tra CPU e memoria RAM.
Esse sono utilizzate per minimizzare il tempo di accesso alla memoria per carichi tipici e aumentare il hit rate.
Scelte nella progettazione di una cache:
- Dimensionamento e numero dei blocchi utilizzati.
- Metodo per determinare se un blocco è presente e come si individua.
- Metodo per recuperare un blocco dal livello inferiore e decidere dove scriverlo nella cache.
Si crea quindi una funzione mapping tra indirizzi di memoria e identificatori del blocco.

**Cache ad accesso diretto (Direct-mapped cache)**
La funzione di mapping è: *address % # blocchi cache* dove il numero di blocchi è una potenza di 2, infatti moltiplicare per una potenza di 2 equivale a effettuare uno shift a sinistra e la divisione equivale ad uno shift a destra.

Nel caso di 8 blocchi, ognuno da 1B, gli indirizzi con gli stessi 3 bit significativi finiscono nello stesso blocco:
![[Pasted image 20230804215714.png]]

Abbiamo istruzione da 4B quindi avere blocchi da 1B non è una buona ottimizzazione. Avere blocchi da più Byte però introduce un nuovo indirizzamento al blocco e non al Byte:
- Calcolo l'indirizzo del blocco = indirizzo / dimensione del blocco.
- Calcolo l'indice del blocco della cache = indirizzo del blocco % numero dei blocchi.

Nel caso di 8 blocchi da 2B ciascuno:
- Calcolo l'indirizzo del blocco dividendo l'indirizzo della memoria per la dimensione del blocco, in questo caso 2. Sappiamo che dividere per 2 equivale a shiftare a destra gli indirizzi prendendo dunque in considerazione i bit più significativi (quelli a sinistra, ignorando il bit più a destra):
![[Pasted image 20230804221410.png]]
- Calcolo l'indice del blocco facendo il modulo dell'indirizzo del blocco per il numero dei blocchi della cache, in questo case 8. Fare il modulo di una potenza di 2 significa prendere i n bit meno significativi (a destra) dove n è il logaritmo in base 2 della potenza di 2 prima citata. Siccome *log2(8) = 3*, prendiamo i 3 bit meno significativi:
![[Pasted image 20230804221424.png]]

**TAG**
Serve capire però quale dei blocchi di memoria che possono essere salvati nella stessa cache è attualmente salvato dentro. Dobbiamo quindi salvare anche l'indirizzo di memoria di tale blocco di memoria, ma non serve l'intero indirizzo in quanto già sappiamo quali sono i bit più significativi (perché sono gli stessi bit del blocco della cache). Ci servono i bit più significativi che chiamiamo **tag** ed è definito come *indirizzo del blocco della memoria /  # blocchi della cache*.

![[Pasted image 20230804225027.png]] ![[Pasted image 20230804225118.png]]
Per riuscire a capire quale dato dalla memoria è salvato nella cache si fa così:
- I bit più significativi sono nella cache, insieme al blocco, è salvato come **tag**.
- I bit successivi al tag sono i bit del blocco della cache, il **Index** (in questo caso corrisponde a soli 3 bit).
- Il bit meno significativo corrisponde al Byte del blocco della cache, il **Byte Offset** (in questo caso uno solo).

L'ultimo valore importante è il **valid bit**, un bit che definisce se i dati in quella parte di memoria sono validi per essere usati o no (per esempio nel caso quella memoria abbia bit che non appartengono a nessun dato).

Esempio di Cache del vecchio MIPS con word da 4 Byte:![[Pasted image 20230807151344.png]]

Esempio di Cache con blocchi da 4 word (16 Byte):![[Pasted image 20230807151733.png]]

Esercizio:
Assumiamo una cache con 64 blocchi, ognuna da 16 Byte.
1. Se l'indirizzo è di 27 bit, com'è composto?
2. Qual è l'indice del blocco che contiene il byte all'indirizzo 1201?

L'indice (**index**) deve essere in grado di puntare a tutti i 64 blocchi, abbiamo quindi che la misura dell'indice è: log2 (64) = 6 (bit).
Il **offset** deve essere in grado di indirizzare ognuno dei 16 Byte del blocco, abbiamo quindi che la misura dell'offset (block offset e byte offset insieme) è: log2 (16) = 4 (bit).
Il **tag** corrisponde ai bit rimanenti: 27 - 6 (index) - 4 (index) = 17.
![[Pasted image 20230807165829.png]]

Indice dell'indirizzo 1201:
- Posso scrivere l'indirizzo in binario e inserirlo nel tag, index e offset.
- Posso calcolare i blocchi tramite operazioni:
	- Indirizzo del blocco = 1201 (indirizzo del Byte) / 16 (Byte di ogni blocco) = 75
	- Offset all'interno del blocco = 1201 % 16 (Byte per ogni blocco) = 1 (primo Byte nel suo blocco)
	- Index = 75 % 64 (numero dei blocchi) = 11 (dodicesimo blocco)
	- Tag = 75 / 64 = 1
![[Pasted image 20230807173209.png]]


Dimensioni ottimali?
Aumentando il Block Size:
- Sfrutto la località spaziale e si può diminuire il miss rate.
- Si aumenta il miss penalty (che equivale al numero di cicli spesi per accedere alla DRAM e i cicli spesi per copiare i dati) perché più dati vengono copiati da DRAM a Cache.
- Aumentare troppo il block size ci porta a sprecare memoria della cache per dati che non servono.

C'è un rapporto tra miss rate e block size:![[Pasted image 20230807210343.png]]


**CONFLITTI**
Copiare nella cache un nuovo blocco dove già ne è stato salvato uno ci porta a doverlo sovrascrivere:
- Se il vecchio blocco è stato solo letto, non c'è nessun conflitto e si può sovrascrivere.
- Se il vecchio blocco è stato letto e scritto, non possiamo semplicemente sovrascrivere e perdere i dati scritti ma bisogna creare una **politica di coerenza** tra i livelli di memoria.

Politiche di coerenza:
- Scrittura diretta: ad ogni istruzione di scrittura la CPU aspetta che essa venga anche scritto ai livelli inferiori, rendendo tutto molto lento.
- Write through: una scrittura nella cache implica una scrittura automatica nei livelli sottostanti
	- Non è più presente nessun conflitto e si può sovrascrivere senza problemi.
	- Le scritture sono molto lente e accedere alla memoria inferiore ad ogni scrittura in cache.
	- Possibile usare un **write buffer**. una memoria tampone veloce tra cache e memoria.
		- I blocchi sono scritti temporaneamente nel write buffer e vengono scritti a loro tempo in modo asincrono.
		- Il processore può proseguire senza attendere la scrittura finché il write buffer non è pieno.
		- Il problema maggiore è che scrivere in memoria è tanto lento che non è difficile per la CPU riempire il write buffer e una volta pieno la CPU dovrà aspettare per ogni inserimento prima di continuare, come nella scrittura diretta.
- Write back: le scritture avvengono normalmente nella cache e la scrittura a livello superiore avviene sono quando abbiamo la presenza di un conflitto.
	- In assenza di confitti non vi è overhead dovuto alla politica della coerenza.
	- La sostituzione di un blocco è più complessa e lenta.


**HITS & MISS**
- Read-hit:
	- Conseguente a lw e instruction fetch.
	- Accesso alla memoria con massima velocità.
- Read-miss:
	- Si mette in stallo la CPU finché non viene completata la lettura dalla memoria.
	- In caso di Instruction cache miss: si ripete il fetch dell'istruzione.
	- In caso di Data cache miss: si completa l'accesso al dato (lw).
- Write-hit:
	- Conseguente a sw.
	- Dipende dalla politica di coerenza:
		- Write through: i dati sono scritti in cache e in memoria.
		- Write back: i dati sono scritti in cache e viene salvato un bit "dirty" per segnalare la modifica per quando verrà sovrascritta.
- Write-miss:
	- Conseguente a sw.
	- Dipende dalla politica di coerenza:
		- Write through:
			- Il controllo mette in stallo la CPU.
			- La scrittura avviene in cache e poi in memoria.
		- Write back:
			- Il controllo mette in stallo la CPU.
			- Lettura del blocco della memoria cache (write allocate).
			- Completamento dell'istruzione di store in cache.


**Cache Associativa**
Nella Cache diretta abbiamo visto che ogni blocco di memoria è associato ad un preciso blocco di Cache. 
Nella Cache completamente associativa ogni blocco di memoria può essere associato con un qualsiasi blocco libero della Cache.
- L'accesso non dipende dall'indirizzo.
- La ricerca della Cache viene effettuata scorrendo tutti i possibili blocchi (HW comparator).

![[Pasted image 20230809194507.png]]
I blocchi della Cache sono disposti come una lista e ogni blocco di memoria viene inserito nel primo blocco libero.