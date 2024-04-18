def: in numero di elementi di una base finita di V è chiamata la dimensione della base.
	Theor. Due qualsiasi basi finite di  uno spazio vettoriale V hanno lo stesso numero di elementi.
Es: 
- $V = \mathbb{R}^n$ n è la sua dimensione ($dim(V) = n$)
- $\mathbb{R}_{n}[x]= V \rightarrow dim(V) = n+1$
- $V = \{f:\mathbb{R}\rightarrow \mathbb{R}\}$

Esercizio:
- $V=\mathbb{R}^{4};S=\{v_{1}, v_{2}\}$. 
	- $v_{1}= (1, 0, 1, 0)$
	- $v_{2}= (1, 2, 3, 4)$
- Completare S in modo che sia una base.
	- Per farlo devo aggiungere 2 vettori (per arrivare a 4 come la base) e che siano linearmente indipendenti.
1. Controllare che i $v_{1} \mbox{~e~} v_{2}$ siano linearmente indipendenti
	- $v_{2}=\lambda v_{1}$ ma $(1, 2, 3, 4) = \lambda(1, 0, 1, 0) = (\lambda, 0, \lambda, 0)$. Non c'è lambda che soddisfi quindi sono indipendenti.
2. Cercare le altre v:
	- Prendo una base canonica $B = \{e_{1}, e_{2}, e_{3}, e_{4}\}$
	- $v_{1}= (1, 0, 1, 0) = e_{1}+e_{3}$
	- $B' = \{e_{1}, e_{2}, v_{1}, e_{4}\}$
	- $v_{2}=(1, 2, 3, 4) = \alpha_{1} e_{1}+ \alpha_{2} e_{2}+ \alpha_{3} e_{3}+ \alpha_{4} e_{4}$
	- $\left\{ \begin{array}{rcl} \end{array}\right.$

Dimensione dei sottospazi vettoriali (s.s.vet.)
- dim(V) = n. W s.s.vet di V:
	- $dim(W) \leq n$
	- $dim(W) = n \Leftrightarrow W = V$ 
	- $dim(W) = 0 \Leftrightarrow W=\{0\}$
- U, W s.s.vet di V
	- $U\cap W$ s.s.vet di V:
		- $dim(U\cap W) \leq min\{dim(U), dim(W)\}$
	- $U\cup W$ s.s.vet di V: Non può essere
	- $U+V$ s.s.vet di v:
		- $dim(U+W) \geq max\{dim(U), dim(W)\}$
		-   