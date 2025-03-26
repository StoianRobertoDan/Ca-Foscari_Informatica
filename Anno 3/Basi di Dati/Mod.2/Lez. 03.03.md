1)
F(AB->C, AC->B, AD->E, B->D, BC->A, E->G) 
$\Pi_{ABC}(F):$
- $A\rightarrow A^{+}_{F}\cap ABC\Rightarrow A\cap ABC \Rightarrow A\rightarrow A$
- $B\rightarrow B^{+}_{F}\cap ABC\Rightarrow BD\cap ABC \Rightarrow B\rightarrow B$
- $C\rightarrow C^{+}_{F}\cap ABC\Rightarrow C\cap ABC \Rightarrow C\rightarrow C$
- $AB\rightarrow AB^{+}_{F}\cap ABC\Rightarrow ABC\cap ABC \Rightarrow AB\rightarrow C$
- $BC\rightarrow BC^{+}_{F}\cap ABC\Rightarrow BCA\cap ABC \Rightarrow BC\rightarrow A$
- $AC\rightarrow AC^{+}_{F}\cap ABC\Rightarrow ACB\cap ABC \Rightarrow AC\rightarrow B$
È già in BCNF.

2)
R=(ABCDE), F={B->C,B->D,B->E,C->B}
Dimostrate che non è 3NF (né BCNF altrimenti sarebbe anche 3NF in automatico) e convertirlo.
- Verificare BCNF: $B^{+}_{F} = BCDE \neq ABCDE$
- Troviamo tutte le chiavi:

| [X::Y] | X   | Y   | $X^+$ | Key |
| ------ | --- | --- | ----- | --- |
| A::BC  | A   | BC  | A     | ~   |
| AB::C  | AB  | C   | ABCDE | AB  |
| AC     | AC  | ~   | ACBDE | AC  |
- Verifichiamo 3FN:
	- $B\rightarrow C \Rightarrow B^{+}_{F}\neq ABCDE$
	- $B\rightarrow D \Rightarrow B^{+}_{F}\neq ABCDE$   no

- Convertire in 3FN:
	- Portare in forma canonica:
		- 1. fatto
		- 2. fatto
		-  $B^{+}_{F\backslash B\rightarrow C} = BDE \neq C$
		- $B^{+}_{F\backslash B\rightarrow D} = BCE \neq D$
		- $B^{+}_{F\backslash B\rightarrow E} = BCD \neq E$
		- $C^{+}_{F\backslash C\rightarrow B} = C \neq B$
	- Raggruppo $F'={B\rightarrow CDE, C\rightarrow B}$
	- $\{R_{1}(BCDE), R_{2}(CB)\}$
	- Rimuoviamo $R_{2}$
	- $\{R_{1}(BCDE), R_{3}(AB)\}$

Es 5 e 6 come all'esame
