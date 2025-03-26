Uno dei metodi per diminuire errori non campionari è un campionamento causale (si prendono i dati in maniera casuale).Ci permette di evitare di introdurre distorsioni date da aspetti della popolazione che non sappiamo.
Il campionamento casuale semplice estrae unità:
- indipendentemente l'una dall'altra.
- tutte con la stessa probabilità di essere estratte.

Statistiche che misurano la posizione: 
- media campionaria 
- mediana campionaria 
- quantili, percentili, quartili 
Statistiche che misurano la variabilita:` 
- varianza campionaria e deviazione standard 
- scarto interquartile


Media campionaria:
- Supponiamo che le osservazioni $X_i$ siano variabili i.i.d. con valore atteso $E(X) = µ$ e varianza $Var(X) = σ^2$
- La media campionaria è: $\overline{X} = \frac{1}{n}\sum\limits_{i=1}^{n}X_{i}$
	- $\overline{X}$ è la variabile casuale media campionaria.
		- è un **stimatore**.
	- $\overline{x}$ e il particolare valore (numero) osservato della ` media campionaria nel campione
		- è una **stima**.

**





La media campionaria per via della legge ** è asintoticamente normale.
nella formula ![[Pasted image 20250218105536.png]]
avendo n al denominatore, al crescere di n la distribuzione è più schiacciata.

La media è sensibile alle osservazioni estreme, cioè pochi dati ma molto estremi dagli altri modifica di molto il valore atteso.
La mediana campionaria stima la mediana di popolazione e non è cosi sensibile alle osservazioni estreme.
La mediana di popolazione divide la distribuzione della variabile casuale in 2 parti uguali.
La mediana campionaria è inferiore e superiore al più a metà dei dati campionari.
Per calcolare la mediana campionaria si ordinano le osservazioni in ordine crescente, se **n è dispari** allora $\widehat{M}$ è l'osservazione del campione in posizione $(n+1)/2$, se **n è pari** allora $\widehat{M}$ è un qualsiasi valore tra l'osservazione in posizione $n/2$ e $(n+2)/2$.


I singoli scarti mostrano quanto i dati si discostano dalla media ($X_{n}-\overline{X}$).
Se facciamo la media degli scarti ($\frac{1}{n} \sum\limits_{i=1}^{n}X_{i}$) il risultato sarà sempre 0. (vedi foto lezione)
Possiamo invece usare $S^{2}=\frac{1}{n-1}\sum\limits_{i=1}^{n}R_{i}^{2}$ e si chiama varianza campionaria.
Perchè $n-1$? senza sarebbe uno stimatore distorto. vedi pag 220-221 del libro.
Esso è uno stimatore della varianza della popolazione $\sigma^{2}= Var(x)$.
La deviazione standard campionaria è la radice quadrata della varianza campionaria.

DA RICORDARE PER L'ESAME!
- il valore atteso di una trasformazione non è uguale alla trasformazione del valore atteso (tranne quando è lineare es:).
	- $g(x) = a+bx$ , $E(g(x))=f(E(x))$ 
- Convergenza di probabilità: se $g(x)$ è continua e $X\to \Theta$ allora 