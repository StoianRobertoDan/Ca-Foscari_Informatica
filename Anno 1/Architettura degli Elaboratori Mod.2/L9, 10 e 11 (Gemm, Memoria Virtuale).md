
Moltiplicazione tra matrici: 
![[Pasted image 20230808140307.png]]
- Moltiplicazione riga-colonna: ogni casella è il risultato della somma di tutti i prodotti tra la riga della prima matrice e la colonna della seconda matrice (la riga e la colonna che si intersecano nella casella di cui stiamo calcolando il valore).
- Il numero di righe della prima matrice deve essere uguale elle colonne della seconda matrice.
- La matrice risultante ha lo stesso numero di righe della prima matrice e numero di colonne uguale al numero di righe della seconda colonna.

Moltiplicazione tra matrici in c
```
for( i = 0; i < Ma; i++)
	for( j = 0; j < Nb; j++)
		for( k = 0; k < Na; k++)
			C[ i*Nb + j ] += A[ i * Na + k ] * B[ k * Nb + j ]
```
 ed equivale a: ![[Pasted image 20230808141020.png]]

Accedere ad A utilizza il principio di località spaziale e per accedere a C si utilizza il principio di località temporale però B non utilizza nessun principio di località. Possiamo quindi scrivere il codice della moltiplicazione in questo modo:
```
for( i = 0; i < Ma; i++)
	for( k = 0; k < Na; k++)
		for( j = 0; j < Nb; j++)
			C[ i*Nb + j ] += A[ i * Na + k ] * B[ k * Nb + j ]
```
Abbiamo quindi questa situazione:![[Pasted image 20230808141558.png]]

In questo modo A utilizza il principio di località temporale e B e C utilizzano il principio di località spaziale.
I due metodi utilizzano lo stesso numero di istruzioni e hanno lo stesso valore finale ma il secondo metodo ci impiega molto meno tempo.


Esempio degli effetti della cache sui programma (Radix Sort VS Quicksort).

Rapporto sul numero di istruzioni per item:![[Pasted image 20230808143120.png]]

Rapporto sulle Cache misses:![[Pasted image 20230808143216.png]]

Di conseguenza questo è il grafito del rapporto sul numero dei cicli speso per item:![[Pasted image 20230808143308.png]]

Si vede che, nonostante il Radix Sort utilizza meno istruzioni per memorie Cache grandi, il suo rateo di Miss lo porta ad essere complessivamente più lento del Quicksort.


**Memoria Virtuale**
La memoria virtuale è una tecnica in cui la memoria primaria (RAM) agisce da Cache per la memoria secondaria. I motivi sono:
- Realizzare un meccanismo **sicuro** affinché la RAM possa essere condivisa tra più programmi in esecuzione. Un programma non deve, senza permesso, allo spazio indirizzato ad un altro programma.
- Con questo meccanismo è possibile far utilizzare ad un programma più memoria di quanto in realtà disponibile, andando ad utilizzare la memoria fissa come RAM.
- I programmi possono essere riallocati nella memoria senza bisogno di ricompilazione, cosi il programma usa regioni anche non adiacenti della memoria.

I programmi sono compilati rispetto ad uno spazio di **indirizzamento virtuale** ed è la CPU e il SO che mappano gli indirizzi virtuali nella memoria fisica con gli indirizzi fisici.
In questo modo ogni programma ha la sua memoria dedicata e lo stesso indirizzo di memoria utilizzato da 2 programmi viene mappato in 2 posizioni di memoria fisica diversa.
![[Pasted image 20230808145721.png]]

Questi blocchi di memoria chiamati **pagine** possono essere mappati anche su memoria fisica invece che sulla RAM. 
Pagine fisiche possono essere condivise tra più indirizzi virtuali se diversi programmi devono accedere agli stessi dati.

Gli indirizzi sono divisi tra:
- Virtual page number e page offset nella memoria virtuale.
- Physical page number e page offset (uguale al page offset virtuale) nella memoria fisica
Un meccanismo traduce i virtual page number in physical page number.

![[Pasted image 20230808150726.png]]
In questo esempio la Page Table contiene 2^20 elementi, ciascuno da 18 bit (che corrisponde al Physical Page Numbert) e un bit di validità per sapere se l'indirizzo è in memoria.

Mapping:
- I page Offset determina la dimensione della page (Page offset = log2 (page size)).
- La traduzione avviene mediante una page table, un array di indirizzi.
- Ciascun programma in esecuzione ha la propria page table.
- La page table risiede nella memoria RAM.
- Tutte le page tables sono salvate in una page table register.
- Ad ogni pagina virtuale può essere associata qualsiasi pagina fisica, completa associatività.

Page Fault
- Se una pagina non è presente in RAM ma solo su disco si verifica un Page Fault (come la cache miss ma per la RAM),
- Il miss penalty delle pagine è enorme quindi è molto importante ridurre il più possibile il numero di Page Faults:
	- Mapping completamente associativo tra pagine virtuali e fisiche.
	- Politica di rimpiazzo delle pagine di tipo LRU.
	- I page Fault sono gestiti via software con l'intervento del SO (algoritmi sofisticati di mapping e rimpiazzamento).
	- Si usa solo politica Write-back perché è troppo costoso scrivere in memoria secondaria.

Bit di stato:
- Valid bit: per determinare se la pagina seguente è valido e in memoria.
- Dirty bit: per sapere se sulla pagina seguente è stato scritto e se deve quindi essere copiata in memoria con il Write-back.
- Reference bit: per indicare se la pagina è stata riferita in un certo lasso di tempo. Il bit viene periodicamente azzerato e settato a 1 quando viene riferita la page (importante per la politica LRU).

Ad ogni accesso alla Page Table ci sono 2 passaggi:
- Prima accedere all'area di memoria RAM dove è salvata la Page Table per leggerla e tradurre l'indirizzo virtuale.
- Seconda accedere all'area di memoria RAM all'indirizzo che abbiamo tradotto.
Si utilizza quindi una Cache per gli elementi della Page Table chiamata **TLB** (Translation Lookaside Buffer) o Translation Cache.
- La TLB contiene le ultime pagine riferite dalla Page Table.
- La TLB alcune volte è implementata (separatamente dalla Cache) in hardware creando un overhead minimo in caso di hit.
- Ogni volta che un Page Fault avviene, viene copiata anche nella TLB per velocizzare gli accessi futuri.
![[Pasted image 20230809160753.png]]
In questo esempio la TLB (tabella superiore) è completamente associativa cioè per ogni Tag c'è una virtual page number.
Se una Page viene eliminata dalla Page Table essa viene dissociata anche dal TLB. Il TLB contiene solo tag validi.

Un TLB Miss produce:
- Un eccezione che può essere risolta se la pagina è presente nella Page Table. 
	- Penalty simile alla Cache Miss cioè RAM Lookup.
	- L'istruzione che ha causato l'eccezione (lw, sw) deve essere rieseguita dopo aver caricato l'entry nella Page Table.
- Una Page Fault nel caso la Page non sia presente nella Page Table.
	- Recuperare la pagina dalla memoria secondaria è molto lento ed è impensabile tenere in stallo la CPU. Si effettua un Context Switch:
		- Il SO salva lo stato del programma (processo) in esecuzione.
		- Carica lo stato di un altro processo.
		- Riprende l'esecuzione del nuovo processo.
	- Se si cambia Page Table durante un Context Switch bisogna anche cambiare la TLB che è unica per ogni processo e bisogna riempirlo da capo, provocando molte miss.

Come lavora la Cache sulla memoria virtuale e sulla TLB?
- Physically addressed Cache: la cache lavora dopo la TLB e Page Table, su indirizzi fisici.
	- Ogni accesso passa prima per TLB (e Page Table in caso di TLB miss).
	- Relativamente facile da implementare.
	- Non è soggetta ad Aliasing tra programmi che usano gli stessi indirizzi virtuali in un dato istante.
- Virtually addressed Cache: la cache lavora prima della TLB e Page Table, su indirizzi virtuali.
	- Una hit della Cache non richiede l'accesso alla TLB (non provoca ne TLB miss ne Page Fault).
	- Soggetta ad Aliasing e se diversi programmi usano lo stesso indirizzo virtuale (ma di Page Tables diverse) ci possono essere letture e sovrascrizioni da parte di tutti i programmi. 
- Virtually indexed but physically tagged: approcio ibrido in cui la cache usa il tag fisico (per evitare aliasing) ma indice virtuale.
	- Comportamento simile alla Cache Physically Tagged.
	- Evita il Aliasing.
	- Possono essere più vantaggiose in termini di prestazioni.

Tipologie di Miss:
- Compulsory (Certi) Miss: si verificano all'accensione di un programma quando la sua Cache è ancora vuota.
- Capacity (Capacità) Miss: si verificano quando la Cache non è in grado di contenere i blocchi necessari ed espelle e riammette blocchi nella Chace.
- Collisions (conflitti) Miss: si verifica quando 2 blocchi sono in conflitto per la stessa posizione. 
	- Possono verificarsi anche se la Cache non è piena
	- Solo se la Cache non è completamente associativa, altrimenti viene usato il primo blocco libero.


**SO e Memoria Virtuale**

Il sistema operativo viene invocato per gestire TLB Miss e Page Fault.
In risposta alle eccezioni/interruzioni:
- La CPU salta alla routine di gestione del SO.
- Cambio modalità esecuzione da **User Mode** a **Supervisor (Kernel) Mode**.
	- La Supervisor Mode è una modalità esecutiva (Execution Mode).
	- Durante il programma in User Mode:
		- Non può modificare il Page Table Register.
		- Non può modificare le entry della TLB.
		- Non può cambiare l'Execution mode.
	- La User Mode permette la protezione dei programmi in esecuzione.
	- Un programma in esecuzione può passare da User Mode a Supervisor Mode solo con eccezioni o invocando il System Call.

Certe CPU hanno concatenate al TLB anche un ID del processo. Ogni hit ha così bisogno di un match tra Page number e Process ID.
Durante il Context Switch quindi non serve svuotare la Cache.
Processi diversi hanno memorie diverse ma Threads dello stesso processo condividono la stessa memoria. Uno Context Switch è più facile switchando tra threads.

Address Space di ARM:
![[Pasted image 20230809224429.png]]
ARM ha indirizzi virtuali da 48 bit, abbastanza da coprire 256TB di memoria e ha indirizzi fisici da 40 bit, abbastanza per 1TB di memoria. Visto che solo una piccola parte dello spazio di indirizzamento è davvero usato, ARM usa un approccio gerarchico a 4 livelli per Page Table:![[Pasted image 20230809225024.png]]

