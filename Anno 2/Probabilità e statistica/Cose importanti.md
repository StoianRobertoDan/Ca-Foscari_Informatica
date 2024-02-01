
Disposizioni semplici: 
- Contano i gruppi di k elementi, di un insieme di cardinalità n, che differiscono tra loro per almeno un elemento oppure per l'ordine con il quale gli elementi sono disposti.
- $$D_{n,k} = \frac{n!}{(n − k)!}$$
Disposizioni con ripetizione: 
- Contano i gruppi di k elementi, di un insieme di cardinalità n, che differiscono tra loro per almeno un elemento oppure per l'ordine con il quale gli elementi sono disposti ed uno stesso elemento può comparire nello stesso gruppo fino a k volte.
- $$D'_{n,k} = n^k$$
Permutazioni semplici: 
- Disposizioni semplici, con k = n.
- $$P_n = n!$$
Permutazioni con ripetizione: 
- Permutazioni in cui un elemento può comparire fino a $\alpha$ volte.
- $$P^{(α)}_n = \frac{n!}{\alpha!}$$
Combinazioni semplici: 
- Contano i gruppi di k elementi, di un insieme di cardinalità n, che differiscono tra loro per almeno un elemento, ma non importa l'ordine con il quale gli elementi sono disposti.
- $$C_{n,k} = \binom{n}{k} =  \frac{n!}{k!(n − k)!}$$
Combinazioni con ripetizione:
- Contano i gruppi di k elementi, di un insieme di cardinalità n, che differiscono tra loro per almeno un elemento, ma non importa l'ordine con il quale gli elementi sono disposti ed uno stesso elemento può comparire nello stesso gruppo fino a k volte.
- $$C'_{n,k} = \binom{n+k-1}{k}$$

![[Pasted image 20240123183217.png]]
![[Pasted image 20240123183231.png]]

![[Pasted image 20240123183457.png]]

Due eventi A e B si dicono incompatibili, o disgiunti, se non è possibile che siano entrambi veri, cioè se A ∩ B = ∅:
![[Pasted image 20240123183742.png]]

Una famiglia di eventi si dice una partizione dello spazio campionario se ogni coppia di insiemi della famiglia ha intersezione vuota e l’unione di tutti i componenti della famiglia è Ω stesso.
![[Pasted image 20240123183803.png]]

Probabilità del complementare: dato un evento A, $$\mathbb{P}[\bar{A}]= 1 − \mathbb{P}[A]$$
![[Pasted image 20240123183842.png]]

Probabilità dell’unione: dati due eventi A e B, $$\mathbb{P}[A\cup B] = \mathbb{P} [A] + \mathbb{P} [B] - \mathbb{P} [A\cap B]$$
![[Pasted image 20240123184218.png]]

Sia B un evento di probabilità positiva. La probabilità condizionata dell’evento A dato l’evento B è $$\mathbb{P}[A|B] = \frac{\mathbb{P}[A\cup B]}{\mathbb{P}[B]} ,\space\space\mathbb{P}[B] > 0$$
![[Pasted image 20240123184807.png]]

![[Pasted image 20240123185120.png]]

Si dice che A e B sono indipendenti nel caso particolare in cui $$\mathbb{P}[A|B] = \mathbb{P}[A]$$ In questo caso, vale anche $\mathbb{P}[A|\bar B] = \mathbb{P}[A]$
![[Pasted image 20240123185230.png]]

Se A e B sono indipendenti, si ha allora $$\mathbb{P}[A\cap B] = \mathbb{P}[A]\mathbb{P}[B]$$
![[Pasted image 20240123185440.png]]

![[Pasted image 20240123190047.png]]
![[Pasted image 20240123190209.png]]

![[Pasted image 20240123190925.png]]


BAYES
1. La definizione di probabilità condizionata: $$\mathbb{P}[C_m|A] =\frac{\mathbb{P}[C_m\cap A]}{\mathbb{P}[A]}$$
2. La formula delle probabilità composte (per il numeratore): $$\mathbb{P}[C_m\cap A] = \mathbb{P}[C_m]\mathbb{P}[A|C_m]$$
3. La legge della probabilità totale (per il denominatore): $$\mathbb{P}[A] = \sum_i \mathbb{P}[A|C_i]\mathbb{P}[C_i]$$
![[Pasted image 20240123191430.png]]
Sia data la partizione C1, C2, . . . e tutti i suoi elementi abbiano probabilità positiva. Sia A un ulteriore evento, anch’esso con probabilità positiva. Fissiamo l’attenzione su uno specifico elemento Cm della partizione. Abbiamo allora $$\mathbb{P}[C_{m}|A] == \frac{\mathbb{P}[A|C_m] \mathbb{P}[C_m]}{\sum\limits_{i} \mathbb{P}[A|C_i] \mathbb{P}[C_i]}$$
![[Pasted image 20240123204231.png]]
ES: ![[Pasted image 20240123204602.png]]


Una variabile aleatoria o casuale X è una funzione che assume valori numerici determinati dall’esito di un certo fenomeno aleatorio. Formalmente, se Ω è lo spazio campionario relativo al fenomeno di interesse, X è una particolare funzione X : Ω → R .
![[Pasted image 20240123211039.png]]
![[Pasted image 20240123211054.png]]

![[Pasted image 20240123211314.png]]
![[Pasted image 20240123213005.png]]


![[Pasted image 20240123213045.png]]

![[Pasted image 20240124175537.png]]

Se X è una v.a. discreta con valori {x1, x2, . . .} e funzione di probabilità $P(x_i) = p_i$ , allora il valore atteso o media di X è $$\mathbb{E}[X] =\sum\limits_i x_ip_i = x_1p_1 + x_2p_2 + ...$$![[Pasted image 20240124175914.png]]

Sia X una v.a. continua con densità f(x). Allora il valore atteso o media di X è: $$E [X] =\int_R xf(x)dx$$![[Pasted image 20240124181031.png]]
![[Pasted image 20240124181720.png]]

Se X è una v.a. discreta con valori {x1, x2, . . .} e funzione di probabilità $P(x_i) = p_i$ , allora la varianza di X è $$Var[X] =\sum\limits_i (x_i − \mathbb{E} [X])^2 p_i$$ $$Var[X] =\sum\limits_i x^2_i p_i − [E [X]]^2$$
![[Pasted image 20240124182009.png]]![[Pasted image 20240124182124.png]]
Sia X una v.a. continua con densità f(x). Allora la varianza di X è: $$Var[X] =\int_R(x − \mathbb{E} [X])^2 f(x) dx$$ $$Var[X] =\int_R x^2 f(x) dx − [E [X]]^2$$
![[Pasted image 20240124182743.png]]![[Pasted image 20240124182836.png]]
![[Pasted image 20240124183214.png]]

La mediana di una variabile aleatoria X è il minimo valore m per cui $$F(m) = P [X ≤ m] ≥ 1 /2$$
Per una v.a. continua (cioè con f.r. F continua) la mediana è l’unico punto m in cui $$F(m) = P [X ≤ m] = P [X ≥ m] = 1/2$$
![[Pasted image 20240124191128.png]]


![[Pasted image 20240124191425.png]]
![[Pasted image 20240124200054.png]]

![[Pasted image 20240124200627.png]]
![[Pasted image 20240124200914.png]]
- Il valore atteso di X ∼ Bin (n, p) è $\mathbb{E}[X] = np$
- La varianza di X si calcola tenendo conto che $Var[X] = \mathbb{E}[X^{2] -}[\mathbb{E} [X]]^2 = np(1 − p)$

![[Pasted image 20240125142849.png]]
Il valore atteso di X ∼ P(λ) è $$\mathbb{E}[X] =\sum\limits^{+\infty}_{i=0} i\frac{\lambda^i}{i!}e^{−\lambda} =\lambda\sum\limits^{+\infty}_{i=1} \frac{\lambda^{i-1}}{(i-1)!}e^{−\lambda}= λ$$
Allo stesso modo si dimostra che $$Var[X] = λ$$
![[Pasted image 20240125143211.png]]![[Pasted image 20240125143908.png]]

![[Pasted image 20240125144716.png]]
![[Pasted image 20240125144748.png]]
![[Pasted image 20240125145531.png]]