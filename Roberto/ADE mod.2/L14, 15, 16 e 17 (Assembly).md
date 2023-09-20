
![[Pasted image 20230813185631.png]]

L'object file è il risultato della compilazione e contiene le istruzioni i diti e le informazioni aggiuntive (metadati) necessarie per produrre il programma eseguibile.
- L'object file è compost da:
	- **Header**: descrive il contenuto dell'object file.
	- **Text segment**: contiene il codice macchina prodotto dall'assemblatore.
	- **Data segment**: contiene i dati "globali" utili.
	- **Relocation information**: identifica le istruzioni e i dati con indirizzi assoluti.
	- **Symbol table**: contiene i simboli (label) locali e globali (da esportare).
	- **Debug information**: informazioni aggiuntive come mapping.

Programmi complessi possono aver bisogno di essere composti da più file detti moduli che sono scritti, compilati e assemblati in modo indipendente.
Un programma può usare moduli scritti e compilati da terze parti dette librerie.

Un programma chiamato **Linker** combina i diversi Object Files compilati dai moduli per combinarli in un unico file eseguibile:![[Pasted image 20230813190726.png]]
- Il programma eseguibile è un file oggetto in cui:
	- Tutti i riferimenti a funzioni esterne sono risolti.
	- Non ci sono informazioni di rilocazione (l'indirizzo di caricamento virtuale è conosciuto).
- Il linker effettua le seguenti operazioni:
	- Prende i text segment di ciascun object file e li concatena in un unico segmento.
	- Prende i data segment di ciascun object file e li concatena in un unico segmento.
	- Concatena il segmento dati generato al segmento text generato.
		- La concatenazione rispetto ad un indirizzo virtuale comporta la potenziale modifica degli indirizzi assoluti. 
	- Risolve i riferimenti sulla base della rilocazione dei vari segmenti.

Quando eseguiamo un programma il Loader:
- Legge l'header dell'eseguibile per determinare la dimensione dei segmenti text e data.
- Crea uno spazio di indirizzamento per il programma con la necessaria memoria (per text, data, stack e heap).
- Copia i text e data segment nel nuovo spazio di indirizzamento.
- Copia i parametri passati da riga di comando nello stack.
- Inizializza i registri (a 0) e inizializza lo stack pointer SP.
- Salta all'indirizzo definito nell'entry-point specificato dall'header dell'eseguibile.


Variabili:
- **Char**: 1 byte.
- **Int**: 4 byte.
- **Short**: 2 byte.
- **Float**: 4 byte.
In assembly serve sapere/specificare la dimensione di ogni tipo di dato per allocarlo correttamente in memoria.

Esempio di programma in assembly:
![[Pasted image 20230814150955.png]]
Solitamente però non si programma in questo modo perché non sappiamo quale sia l'indirizzo esatto delle variabili. Si usano allora etichette (labels) associati a specifici punti del programma o dati. L'assemblatore può convertire le etichette nel loro corrispettivo valore.

.word 10, 20, 30: alloca una sequenza di 3 numeri di 4 byte ciascuno inizializzati con i valori 10, 20, 30 (in base 10).
Altre direttive sono:
![[Pasted image 20230814151436.png]]

Possiamo programmare quindi in questo modo:
![[Pasted image 20230814151709.png]] ![[Pasted image 20230814151726.png]]

Come tradurre espressioni complesse in assembly:
- In modo modulare, traducendo ogni accesso alla variabile come una load e ogni scrittura come una store.
- In modo ottimizzato, massimizzando il numero di variabili utili salvate nei registri e minimizzando gli accessi alla memoria/cache.
	- Evitare di copiare dati dai registri alla memoria se non strettamente necessario.
	- Usare più registri variabili.


Costrutto **IF**:
![[Pasted image 20230814153543.png]]
Esempio di programma che stampa a schermo quale tra a e b è maggiore (04-ifthenelse):![[Pasted image 20230817160208.png]]

Costrutto **Do-While**:
![[Pasted image 20230814153625.png]]

Costrutto **While**:
![[Pasted image 20230814153715.png]]
Costrutto ottimizzato:
![[Pasted image 20230814153811.png]]
Esempio di programma che calcola il fattoriale (05-while):
![[Pasted image 20230817160111.png]]

Costrutto **For**:
![[Pasted image 20230814153935.png]]


Arrays
Gli array non sono altro che un modo per dichiarare e allocare n variabili.
Dichiarare un array di interi la memoria salva 4 Byte di indirizzi di memoria per ogni casella dell'array:
![[Pasted image 20230817161410.png]]
In questo caso abbiamo un array di 10 interi.
Per accedere ad ogni casella ci basta utilizzare l'indirizzo della prima casella (es: x0) e l'indice dell'array (es: x1). Per ottenere x3 = &(A\[x1]) possiamo scrivere:
![[Pasted image 20230817161723.png]]
O si può usare direttamente l'addressing mode offset se abbiamo l'offset piccolo e noto:
![[Pasted image 20230817161841.png]]

Word, dword e Bytes.
Abbiamo visto come caricare Words da 4 o 8 Bytes ma si possono caricare anche singoli Byte.
- STRB w0, \[\<addr>]
	- Memorizza il Byte meno significativo di w0 all'indirizzo *addr*.
- LDRB w4, \[\<addr>]
	- Carica il Byte all'indirizzo *addr* nel byte meno significativo di w4 e padda il resto a 0.

ASCII (American Standard Code for Information Interchange).
![[Pasted image 20230818165050.png]]
- Ogni Byte rappresenta un carattere.
- 128 caratteri disponibili.
	- Da 0 a 31: caratteri di controllo.
	- Da 32 a 126: caratteri stampabili.
	- 127: carattere di controllo DEL.
- Caratteri alfabetici e numerici sono consecutivi:
	- Da 48 a 57: '0' ... '9'.
		- Si possono facilmente tradurre i numeri da cifra a ASCII, Basta sottrarre 48 al codice ASCII o aggiungere 48 alla cifra.
	- Da 65 a 90: 'A' ... 'Z'.
		- Si può passare da maiuscole a minuscole aggiungendo 32.
	- Da 97 a 122: 'a' ... 'z'.
		- Si può passare da minuscole a maiuscole sottraendo 32.
- Solo le lettere inglesi sono rappresentate.
	- Si potrebbero usare anche il resto dei 128 simboli rimanenti (usando l'ottavo bit a 1).
	- Nascono altre codifiche come ISO Latin-1 e Latin-9 e Mac OS Roman:
	- ![[Pasted image 20230818173704.png]]
- Per risolvere questi problemi viene creato UNICODE, un altro set di caratteri con 1.114.112 e comprende tutti i caratteri in tutte le lingue, caratteri matematici e scientifici e anche emoji.
	- Per tutti questi caratteri serve usare 3 Byte, rendendo la dimensione dei testi 3 volte più pesante.
	- Nasce la tecnica **Multi-Byte Character Encoding** che va a dare ai simboli più usati solo un Byte (o 2 Byte) e per quelli meno usati 3 Byte. Nasce cosi **UTF-8**, un encoding che si basa su UNICODE.
		- I primi 128 caratteri richiedono un solo Byte e sono codificati in ASCII.
		- I seccessivi 1920 caratteri richiedono 2 Bytes e comprendono molte delle lingue comuni.
		- I caratteri con 3 Bytes comprendono i caratteri asiatici.
		- I caratteri restanti vengono codificati con 4 Bytes e comprendono emoji, simboli matematici, storici ecc.
		- Codifica UTF-8:![[Pasted image 20230818174707.png]]


Stack e Funzioni.

Procedure e funzioni:
- Sono porzioni di codice che possono essere chiamate più volte per un compito.
- Le funzioni ritornano un valore.
- Le procedure (o subroutine) non producono un valore di ritorno.
- Per chiamare una procedura/fuunzione la CPU ha bisogno di interrompere il flusso e dare controllo al codice della procedura Per poi riprendere da dove aveva interrotto. Serve quindi:
	- Salvare il PC corrente.
	- Modificare il PC con l'indirizzo della procedura.
	- Ripristinare il PC salvato +4 (per andare all'istruzione successiva) al termine della procedura.
- Per chiamare le procedure/funzione si usano le istruzioni **RET** o **BR LR**. **RET** è consigliabile perché:
	- Indica in modo esplicito che si sta per usare una procedura/funzione.
	- Viene modellata in modo esplicito dal branch predictor della CPU ARM Cortex e ha più probabilità di eseguire le scelte migliori.
- Per i parametri delle funzioni e i valori di ritorno esistono delle regole chiamate **Procedure Call Standard (PCS)**. Nella PCS dell'ARM:
	- I parametri della funzione sono passati nei registri x0, ..., x7 (o w0, ..., w7 per interi a 32Bit e d0, ..., d7 per parametri floating point). Se servono più parametri serve usare lo Stack.
		- In C++ x0 è usato per passare il puntatore **this**.
	- Il valore di ritorno è passato nel registro x0.
	- L'indirizzo alla prossima istruzione del codice chiamante è salvata in x30, chiamata LR.
	- La funzione chiamata può usare i registri x0, ..., x15 senza preoccuparsi di conservare il loro valore poiché è responsabilità del codice chiamante salvarle.
	- La funzione chiamata deve preservare i valori dei registri x16, ..., x27. La funzione può modificarli ma deve anche ripristinarli prima di ritornare.
	- Generalmente i registri x8, x16, x17, x18 sono riservati.
- I registri che dobbiamo preservare possiamo salvarli in uno **Stack** di tipo **LIFO** (Last In First Out).
	- Lo Stack è allocato in un indirizzo specifico in base al SO e puntato dal registro SP.
	- Si salva nello Stack usando STR e per ripristinare un valore si usa LDR:![[Pasted image 20230819190519.png]]![[Pasted image 20230819190536.png]]![[Pasted image 20230819190548.png]]
	- In AArch64 tutti gli accessi alla memoria mediante registro SP deve essere allineati a 16Bytes (16 o multipli). Per risolvere questo vincolo hardware si può:
		- Accettare la limitazione e sprecare spazio usando 16Bytes per registro.![[Pasted image 20230819191059.png]]
		- Riservare lo spazio necessario (sempre 16 o multiplo) per salvare più registri.![[Pasted image 20230819191208.png]]
- E' importante che al termine di una funzione si ripristini lo Stack Pointer al valore che aveva prima.
- Quando invochiamo una funzione bl dobbiamo assumere che i registri X0…X15 saranno sovrascritti. Se contenevano informazioni importanti vanno salvati prima di invocare la funzione.
	- Possiamo copiare i valori sui registri x19, ..., x27.
	- Possiamo salvarle nello stack.
- Bisogna salvare il LR se viene chiamata un'altra funzione.