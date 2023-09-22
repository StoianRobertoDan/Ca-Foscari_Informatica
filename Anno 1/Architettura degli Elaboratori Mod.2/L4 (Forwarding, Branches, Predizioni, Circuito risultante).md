
Negli Hazard RAW non sempre serve aspettare che un valore venga salvato, infatti già dopo che è stato calcolato il valore esso viene salvato nei registro intermedio EXE/MEM.
Sapendo questo si può salvare tempo andando a prendere il valore direttamente dal registro intermedio invece che dopo il Write Back (che è invece 2 stadi successi, cosi si risparmiano 2 nop).
![[Pasted image 20230803183431.png]]


Guardiamo questo esempio:![[Pasted image 20230803183822.png]]

Possiamo facilmente vedere che la *and* e la *or* creano hazard in quanto, se il registro usasse il valore di $2 in quel momento non sarebbe aggiornato al valore dopo la *sub*, dovremmo quindi mettere in pausa tutte le istruzioni successive alla sub.
Si nota inoltre che la *and* accede per leggere dal registro nello stesso ciclo di clock in cui la *sub* iniziale scrive nel registro (Write Back). Questo può avvenire solo se il Register File è ottimizzato per poter scrivere (prima) e leggere (dopo) nello stesso ciclo di clock.
Infine la *sw* non crea nessun hazard nonostante sia dipendente dalla *sub*, questo perché la lettura del registro avviene nel ciclo di clock successivo alla scrittura.
Vediamo come questo viene risolto dal *Forwarding*:
![[Pasted image 20230803190936.png]]
![[Pasted image 20230803191147.png]]

Le load word invece può creare comunque un hazard in quanto il valore è disponibile solo dopo lo stage MEM (non dopo lo stage EXE come prima) e il nop è, a volte, neccessario.
![[Pasted image 20230803191502.png]]

Nel caso dei branch (come beq-or) si sa il risultato solo dopo lo stadio EXE ed è solo dopo il registro intermedio EXE/MEM che il program counter sa cosa deve eseguire.
Il modo più semplice è di inserire 3 nop.

Un altro modo però sarebbe assumere che i branch siano sempre not taken e questo ci produce 2 casi:
- Il branch è not taken (falso e quindi non si fa il salto) allora le 3 istruzioni successive sono già entrate nella pipeline e possono semplicemente continuare l'esecuzione.
- Il branch è taken (vero e quindi si deve fare il salto) comunque le 3 istruzioni successive sono entrate nella pipeline ma non hanno ancora modificato ne la memoria (che avviene nello stadio MEM) ne i registri (che avviene nello stadio WB) e basta quindi solo forzare quelle istruzioni in nop.
In entrambi i casi non portano errori ma nel caso del branch taken abbiamo perso 3 cicli di clock.
Possiamo ridurre il delay del branch anticipando il confronto dei registri inserendo un'unità specializzata formata XOR bit a bit e un OR finale nello stadio ID.
![[Pasted image 20230803195608.png]] 
In questo modo anticipiamo di 2 cicli di clock il controllo e solo una istruzione sarà entrata nella pipeline prima di sapere il risultato del controllo.

Nelle CPU MIPS si utilizza la tecnica del **delayed branch** secondo cui non solo si riduce il delay grazie all'unita specializzata ma l'istruzione successiva entrata nella pipeline viene sempre eseguita. E' compito del compilatore/assemblatore inserire dopo il branch una nop esplicita oppure un'istruzione che non modifica la semantica del programma.
Questa tecnica non è utilizzata dalle CPU più moderne perché avendo delle pipeline più lunghe servirebbero più **delay shot** (istruzioni da riempire dopo un branch) e non è ottimale.

Questa tecnica inoltre produce un problema nel forwarding in quanto i valori possono essere recuperati dopo lo stadio EXE ma essendo il delay branch eseguito nello stadio ID (dell'istruzione successiva) bisogna comunque inserire una nop perché i 2 stadi avvengono nello stesso ciclo di clock:![[Pasted image 20230803200008.png]]

Nel caso della lw invece ne vanno inseriti 2 di nop in quanto il valore è disponibile solo dopo lo stadio MEM:![[Pasted image 20230803200108.png]]

Assumere che il branch sia sempre not taken (**previsione semplice**) può essere comodo per per pipeline semplici mentre per pipeline profonde il numero di istruzioni da annullare in caso di predizione errata può essere significativo.
L'utilizzo di previsioni dinamiche e algoritmi di previsioni avanzati sono quindi importanti per CPU più complesse.

Per le previsioni dinamiche si una una History Table, una lista degli indirizzi salvati delle istruzioni branch. Essa contiene, per ogni indirizzo di branch, l'indirizzo dell'istruzione successiva al salto se taken e uno o più bit di stato riguardo il risultato della branch:
![[Pasted image 20230803215013.png]]

In questo modo ogni volta che si esegue un branch si può controllare se è già avvenuto di recente e si utilizza lo stato della branch precedente per prevedere lo stato della branch corrente. Questo è molto utile in quanto i cicli non sono altro che salti (branch) alla stessa istruzione e, avvenendo più volte, è più facile da prevedere.

Ci possono essere predittore a uno o più bit. Ecco 2 esempi (stati a 1 bit e a 2 bit):
![[Pasted image 20230803220349.png]]
![[Pasted image 20230803220405.png]]

Le predizioni possono comunque produrre errori quindi serve avere un'unità di individuazione delle criticità sul controllo (un Hazard detection unit). L'unità è inserita nello stadio ID e potrà inserire delle nop nel caso di predizioni errate e istruzioni già entrate nella IF:![[Pasted image 20230803221157.png]]


**==RIASSUNTO (CON FORWARDING E DELAY BRANCH)==**
![[Pasted image 20230803200457.png]]
![[Pasted image 20230803200557.png]]


