
Es2:
- A -> B
- B -> C
- AE -> D
- Find AE -> C
Sappiamo per transitività che se A -> B e B -> C allora A -> C. 
For AUGM rule A -> C is equal to AW -> CW so equal to AE -> C.

Es3:
- R(A,B,C,D)
- F{AB -> C, C-> D, D -> A}
Chiave? 
- If it's never on the left it doesn't need to be in the key.
- If it's not on the right is should/must be in the key.
Never on left: none
Never on right: B
Candidate: B::(ACD)

| Cand{}   | X   | Y   | $X^+$ | Key |
| -------- | --- | --- | ----- | --- |
| B::(ACD) | B   | ACD | B     | ~   |
| BA::(CD) | BA  | CD  | ABCD  | AB  |
| BC::(D)  | BC  | D   | BCDA  | BC  |
| BD::()   | BD  |     | BDAC  | BD  |

Es4:
- R(ABCD) 
- F{A->B,C->B,D->ABC,AC->D}
Find the canonic cover.
Steps:
1. F' = {A->B,C->B,D->A,D->B,D->C,AC->D}
2. AC->D:
	- $D\notin C^{+}_{F'}= CB$
	- $D\notin A^{+}_{F'}= AB$
3. Enclosures:
	- $B\notin A^{+}_{F''\backslash A->B}= A$
	- $B\notin C^{+}_{F''\backslash C->B}= C$
	- $A\notin D^{+}_{F''\backslash D->A}= DBC$
	- $B\in D^{+}_{F''\backslash D->B}= ABCD$
	- $C\notin D^{+}_{F''\backslash D->C}= ABD$
	- $D\notin AC^{+}_{F''\backslash AC->D}= ABC$
Canonical closure $F_{can}$ = {A->B,C->B,D->A,D->C,AC->D}

(Remember: having XY->Z, X is external if $Y^{+}_{F} not\ni A$)