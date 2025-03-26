Es 1.
F={P->CLA, CL->AP, A->C}, R={P,C,L,A}
Copertura canonica:
- F'={P->C, P->L, CL->A, CL->P, A->C}
- $C^{+}_{F'} = C$  e $L^{+}_{F'} = L$ non contengono A e P, le dipendenze con CL vanno mantenute
- $P^{+}_{F'\backslash{P\rightarrow C}} = PLAC$ ; C è già presente, P->C non serve
- $P^{+}_{F'\backslash\{P\rightarrow C, P\rightarrow L\}} = PAC$ ; L non è presente, si tiene P->L
- $P^{+}_{F'\backslash\{P\rightarrow C,P\rightarrow A\}} = PL$ ; A non è presente, si tiene P->A 
- $CL^{+}_{F'\backslash\{P\rightarrow C,CL\rightarrow A\}} = CLPA$
- $CL^{+}_{F'\backslash\{P\rightarrow C,CL\rightarrow A, CL\rightarrow P\}} = CL$
- $A^{+}_{F'\backslash\{P\rightarrow C,CL\rightarrow A, A\rightarrow C\}} = A$
$F_{can}=\{P\rightarrow L,P\rightarrow A,CL\rightarrow P,A\rightarrow C\}$


| [X::Y]              | X           | Y           | $X^+$       | K   |
| ------------------- | ----------- | ----------- | ----------- | --- |
| $\emptyset$::PCLA   | $\emptyset$ | PCLA        | $\emptyset$ | ~   |
| P::CLA,C::LA,L::A,A | P           | CLA         | PCLA        | P   |
| C::LA,L::A,A        | C           | LA          | C           | ~   |
| L::A,A,CL::A,CA     | L           | A           | L           | ~   |
| A, CL::A,CA,LA      | A           | $\emptyset$ | AC          | ~   |
| CL::A,CA,LA         | CL          | A           | CLPA        | CL  |
| CA,LA               | CA          | $\emptyset$ | CA          | ~   |
| LA                  | LA          | $\emptyset$ | LACP        | LA  |

A->C viola BCNF, $A^{+}_{F}\neq PCLA$
$T_{1}=A^{+}_{F}=AC$ --> $F_{1}=\{A\rightarrow C\}$
$T_{2}=P\in LA\backslash AC\cup A=PLA$ --> $F_{2}=\{P\rightarrow LA,LA\rightarrow P\}$
