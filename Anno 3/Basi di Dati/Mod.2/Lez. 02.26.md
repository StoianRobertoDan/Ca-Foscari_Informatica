Ottimizazzione della verifica.
- Non ci serve calcolarci tutta la chiusura 


Es:
R(ABC) F{A->B,B->C,C->A}
Partizionamento p{$R_{1}$(AB),$R_{2}$(BC)}
Considero A->B
- $A^{+}_{G}$ = 
	- $A\cup((A\cap AB)^{+}_{F}\cap AB)=AB$
	- $AB\cup((AB\cap BC)^{+}_{F}\cap BC)=ABC$
- $B^{+}_{G}$ =  
	- $B\cup((B\cap AB)^{+}_{F}\cap AB)=AB$
	- $AB\cup((AB\cap BC)^{+}_{F}\cap BC)=ABC$


BCNF
Uno schema relazionale è in BCNF sse per ogni dipendenza funzionale non banale $X\rightarrow Y$, si ha che X è superchiave
Costo polinomiale.
