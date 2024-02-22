
Che cos'è la normalizzazione e a cosa serve?



Dipendenze funzionali:
- Dipendenze tra gli attributi. Per esempio tra gli attributi normali e le chiavi principali.

Che cos'è la chiusura di F ($F^+$)?
Che cos'è il problema dell'implicazione? è la dimostrazione che X->Y (dipendenza funzionale tra X e Y) faccia parte di $F^+$ (chiusura di F) oppure no.
Che cos'è la chiusura di X ($X^+_F$)?
In che modo il teorema della chiusura di X è bivalente? (slide 21)

Esempio del calcolo di $X^+_F$:
- X = AB e F = {A → C, AC → D, E → F}
	- C dipende da A, D dipende da A e C, F dipende da E.

- function Closure(X, F)
	- $X^+_{old}$ ← ∅ 
	- $X^+_{new}$ ← X
	- while $X^+_{new} \neq X^+_{old}$  
		- 
	X + new ← X while X + new ̸= X + old do X + old ← X + new for all Y → Z ∈ F do if Y ⊆ X + new then X + new ← X + new ∪ Z return X + new
- Passaggi:
	- $X^+_0$ = AB 
		- Il primo passo di X chiuso ha solo la X che nel nostro caso è AB
	- $X^+_1$ = AB ∪ C = ABC
		- Siccome A fa parte di X chiuso e C ne è dipendente lo si aggiunge.
	- $X^+_2$ = ABC ∪ D = ABCD
		- Siccome A o C fanno parte di X chiuso e D ne è dipendente lo si aggiunge.
	- Siccome E non fa parte di X chiuso non si può aggiungere F.


Cos'è una superchiave? é l'insieme di attributi cui chiusura comprende tutti i suoi attributi
Cos'è una chiave? è una superchiave minimale cioè nessuno dei suoi sottoinsiemi sono a loro volta superchiavi.
Come si può dimostrare che X$\subseteq$T è una superchiave? X è una superchiave se con la chiusura si comprendono tutti gli altri attributi. Si può dimostrare che X è una superchiave se calcolando la chiusura $X^+_F$ si ha che $X^+_{F}=T$
Esempio:
- Si consideri la relazione R(T, G), con T = ABCDEF e G = {AB → C, E → A, A → E, B → F}. 
- ABD è superchiave:
	- $ABD^+_{0}$ = ABD (per dimostrazione)
	- $ABD^+_{1}$ = ABCD (per AB → C)
	- $ABD^+_{2}$ = ABCDE (per  E → A)
	- $ABD^+_{3}$ = ABCDEF (per B → F)
- Se un attributo non dipende da niente (non è mai a destra) fa parte necessariamente della chiave

Che cos'è la forma canonica?
Che cos'è una copertura canonica?
Ci possono essere più coperture canoniche?

Esercizio:
Sia $$F = \{A \rightarrow BC, B \rightarrow C, A \rightarrow B, AB \rightarrow C\}$$
1. Decomponiamo: $G = \{A \rightarrow B, A \rightarrow C, B \rightarrow C, A \rightarrow B, AB \rightarrow C\}$
2. $G = \{A \rightarrow B, A \rightarrow C, B \rightarrow C, A \rightarrow B, AB \rightarrow C\}$ (le doppie possono essere tolte: $G = \{A \rightarrow B, A \rightarrow C, B \rightarrow C\}$)
3. $AB\rightarrow C$ entro nel forall e cerco di togliergli un attributo a sinistra $(AB\backslash {A}$ oppure $AB\backslash {B})$
4. $\{AB\}\backslash\{A\}^+_F = B^+_{F}= BC$ oppure $\{AB\}\backslash\{B\}^+_F = A^+_{F}= ABC$


Esercizio: 
- Usando **gli assiomi di Armstrong** si dimostri che $F = \{X \rightarrow Y, YW \rightarrow Z\}$ allora $XW \rightarrow Z$
	- Arrichimento $\frac{F\vdash X\rightarrow Y}{F\vdash XW \rightarrow YW}$
	- Transitivo $$\frac{\frac{F\vdash X\rightarrow Y}{F\vdash XW \rightarrow YW} F\vdash YW \rightarrow Z}{F\vdash XW \rightarrow Z}$$

