
Al giorno d'oggi nessuna macchina è a singolo ciclo perché la velocità del clock è in base all'istruzione più lunga altrimenti ci possono essere errori. Perciò viola il principio di "common case fast".

![[Pasted image 20230801201159.png]]

Stadi del datapath:
1. Instruction Fetch (**IF**): l'istruzione viene letta dalla memoria e il program counter viene incrementato.
2. Instruction Decode & register file read (**ID**): l'istruzione viene decodificata nelle sue parti e vengono letti i registri coinvolti.
3. Execute (**EX**): calcolo delle operazioni aritmetiche o calcolo dell'indirizzo di memoria (lw/sw) o calcolo dei indirizzi branch (salti).
4. Accesso alla memoria (**MEM**): accesso alla memoria dati per leggere o scrivere un valore (lw/sw).
5. Write back (**WB**): scrittura nei registri (lw).

**Pipeline**: tutte le singole operazioni impiegano lo stesso tempo ma eseguirle contemporaneamente (su istruzioni successive) crea un **throughput** (numero di istruzioni per lasso di tempo) maggiore e un **CPI** (cicli per istruzione) minore.

Esempio con la PCU:
![[Pasted image 20230801211420.png]]

Le istruzioni impiegheranno i seguenti tempi:
![[Pasted image 20230801211509.png]]

Nella versione a **singolo ciclo** il tempo del clock sarà impostata all'**istruzione** più lunga (800 ps).
Nella versione a **pipeline** il tempo del clock sarà Impostata allo **stadio** più lunga (200 ps).

- La Load Word in singolo ciclo durerà 800 ps, nella versione pipeline durerà invece 1000 ps (anche gli stadi che impiegano solo 100 ps comunque dureranno 200 ps).
- 3 Load Word in singolo ciclo dureranno 2400 ps (800 * 3) mentre nella versione pipeline durerà solo 1400 ps perché: 
![[Pasted image 20230801212304.png]]

Lo speed up in questo caso è di 1.7 ma incrementa con l'incremento del numero di istruzioni consecutive, rendendo la versione pipeline sempre più conveniente al maggior numero di istruzioni (come nei normali programmi che il computer esegue), con un throughput maggiore.


Le prestazioni di una pipeline:
- sia IC il numero di istruzioni
- sia T il periodo di clock del processore a singolo ciclo
- sia T' = T/n il periodo di clock del processore con pipeline dove n è il numero di stadi

Nella CPU a ciclo singolo (sequenziale) il tempo totale è IC * T.
Nella CPU con la pipeline abbiamo:
- Il tempo necessario per riempire la pipeline:
	- Per riempire la pipeline ci vogliono (n-1) cicli, perché il n-esimo ciclo concluderà già la prima istruzione. Il tempo necessario per riempire la pipeline è quindi (n-1) * T'
- Il tempo necessario per completare lo stream di istruzioni:
	- Dopo il riempimento della pipeline, per ogni ciclo di clock verrà completata un'istruzione. Il tempo necessario per completare lo stream di istruzioni è quindi IC * T'
- Il tempo totale della CPU a singolo ciclo è: $$(n-1) * T' + IC * T' = (n-1) * T/n + IC * T/n$$
Lo SpeedUp tra la versione a singolo ciclo e la versione con la pipeline è il seguente: ![[Pasted image 20230801215923.png]]

Se il numero di istruzioni è molto grande si ha che lo speedup tende a n, cioè il numero di stadi della pipeline. Più lunga la pipeline, migliore lo speedup, nel caso migliore. ![[Pasted image 20230801220859.png]]

Nella vita reale però:
- Il numero di istruzioni non è mai davvero infinito.
- Gli stadi sono a volte sbilanciati, come nell'esempio della load word di prima in cui il tempo su pipeline è superiore rispetto al tempo sequenziale per la singola istruzione. In questo caso lo speedup tende a $T/T'$.
- C'è una **dipendenza** tra istruzioni che causano **stalli**. Spesso infatti si ha bisogno per una istruzione il risultato della istruzione precedente.

 Ciascuna istruzione ha bisogno dei valori calcolati dallo stage precedente e per questo serve implementare registri intermedi:
![[Pasted image 20230802163406.png]]

In questo modo si possono salvare le istruzioni successive. questo però crea un problema con la load word perché quando il valore sarà preso dalla memoria per essere salvata dei registrers file, la write register sarà cambiata. Per ovviare a questo si può portare avanti il write register e riportarla indietro insieme al write data. Solitamente si può scrivere e leggere nello stesso ciclo di clock quindi non sarà un problema tornare indietro e scrivere. Possiamo fare così quindi:![[Pasted image 20230802204258.png]]


IF e ID vengono eseguiti ad ogni ciclo di clock e non dipendono dai segnali di controllo mentre i successivi stadi si. In corrispondenza di ID quindi vengono calcolati i segnali di controllo e vanno salvati nei registri intermedi per controllare le ALU e i MUX:![[Pasted image 20230802205728.png]]


**Criticità** o **Hazard** è il nome del terzo problema, la dipendenza tra istruzioni che crea stalli. Lo stadio che rivela la criticità (ID) rimane in stallo rieseguendo la stessa istruzione (e facendola rieseguire anche al IF successivo) mentre negli stadi successivi introducono delle nop (bolle d'aria) ovvero istruzioni vuote.

**Hazard**:
- Structural hazards: quando l'istruzione ha bisogno di unità funzionali che sono occupate da istruzioni precedenti. La CPU MIPS è progettata per non avere criticità strutturali.
- Data hazards: dipendenze (l'ordine di esecuzione non è modificabile perchè cambia il risultato finale) sui dati tra coppie di istruzioni. Ci sono 3 tipi (RAW, WAW, WAR)
- Per gestire le criticità serve un Hazard Detection Unit contenuta nello stadio ID che confronta i registri dell'istruzione corrente con quelli delle precedenti istruzioni.

**RAW** (Read After Write): quando un'istruzione ha bisogno di leggere un registro scritto da un'istruzione precedente (quindi bisogna aspettare che il registro finisca di essere scritto).
**WAW** (Write after Write): quando un'istruzione scrive un registro che è scritto da un'istruzione precedente (quindi bisogna aspettare che il registro finisca di essere scritto).
**WAR** (Write After Read): quando un'istruzione scrive un registro che è letta da un'istruzione precedente.

In CPU che seguono passo per passo l'ordine le WAW e le WAR non producono hazard, a differenza delle RAW perché la scrittura avviene allo stage 5 (WB) mentre la lettura avviene nello stage 2 (ID).

**RAW**:![[Pasted image 20230802213825.png]]
![[Pasted image 20230802214224.png]]

L'esempio corrente assume un register file non ottimizzato che non può leggere e scrivere nello stesso ciclo di clock quindi lo stage ID della seconda istruzione avviene al sesto ciclo di clock invece che al quinto.
Si può vedere come gli stadi ID e IF ripetono la loro istruzione fino alla fine del hazard mentre EXE, MEM e WB producono nop. I nop vengono prodotti dal ID (grazie alla Hazard Detection Unit) e portati avanti dai segnali di controllo.

Non tutte le CPU devono per forza avere il Hazard detection Unit (anche se la maggior parte delle CPU odierne ce l'hanno) ma possono dare tale compito di controllo ai livelli successivi (al compilatore o al programmatore) che devono inserire nop manualmente per evitare stalli. In questo modo si può però, se ottimizzato bene, riempire le nod con istruzioni che non sono soggette a criticità per continuare a usare tutti gli stadi durante una criticità. 

