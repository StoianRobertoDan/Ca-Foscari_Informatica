
Classificazioni:
- disposizioni dei dati:
	- Lineari:
		- Quando gli agglomerati sono formati da dati disposti in sequenza.
		- Es: array, liste, pile.
	- Non lineari:
		- Quando non è individuata una sequenza.
		- Es: alberi, grafi.
- Numero:
	- Statiche:
		- In cui il numero degli elementi dell'aglomerato non cambia.
		- Es: array.
	- Dinamica: 
		- In cui il numero di elementi può aumentare o diminuire nel tempo.
		- Es: liste, pile.
- Tipo:
	- Omogenei:
		- In cui i dati sono tutti dello stesso tipo.
	- Non omogenei:
		- In cui i dati possono anche essere di diversi tipi.

Dizionario (map): rappresenta il concetto matematico di relazione univoca
- R: D --> C. Fra gli elementi di un insieme D (dominio) e gli elementi di un insieme C (codominio). Gli elementi del dominio sono detti **Chiavi** e gli elementi del codominio sono detti **Valori**.
- Associazioni chiave-valore.
- Tipo di dizionario:
	- Dati: un insieme S di coppie (chiave-valore).
	- Operazioni:
		- Search(Dizionario S, Chiave K) --> Elemento U {NIL}
			- Post: restituisce il valore associato alla chiave K se presente in S, altrimenti restituisce NIL.
		- Insert(Dizionario S, Elemento V, Chiave K) 
			- Post: Associa il valore V alla chiave K.
			- Se la chiave è nuova allora la aggiunge insieme al suo valore, altrimenti deve fare l'update del valore a quello nuovo.
		- Delete(Dizionario S, Chiave K)
			- Pre: la chiave K è presente nel dizionario S.
			- Post: cancella la coppia (chiave-valore) con chiave K dal dizionario S.

Realizzazione attraverso array ordinati.
- Dati: un array A di dimensioni w contenenti record con due campi (Key, Info).
	- **Ordinati** in base al campo Key.
- A.length contiene la dimensione dell'array.
- Search(Dizionario A, Chiave K)
	- i = search_index (A, K, 1, A.length)
``` C
if(i == -1){
	return NIL
}else return A[i].info
```

``` C
search_index(Dizionario A, Chiave K, int p, int r){
	if (p>r) return -1;
}
``` 



Si mantiene un array di dimensione h, dove per ogni n>0 h soddisfa la seguente invariante:
- n<= h <= 4n
Le prime n celle dell'array contengono gli elementi della collezione, mentre il contenuto delle altre è indefinito:
- Inizialmente quando h=0, proviamo h=1.
- Ogni qualvolta n supera h, l'array viene riallocato raddoppiando la dimensione $(h = 2*h)$.
- Ogni qualvolta n scende ad h/4, l'array viene riallocato dimezzando la dimensione (h = h/2).
Lo spazio $$S(n) = \theta(h) = \theta(n) $$
L'analisi ammortizzata è l'analisi del costo medio dell'esecuzione di n operazioni su una struttura dati.

Assumiamo che il vettore abbia inizialmente dimensione $h=1 \space e \space n=0$ e voglio fare h inserimenti.
Sia Ci il costo dell'i-esimo inserimento: $$ C_i \leftbracket(i \space se \esiste k \taleche i=2^k+1 \acapo 1 \space altrimenti$$
$$C(n) = \sum_{i=1}^nC_i \lessorequal n+ \sum_{k=0}^{\log_2n}2^k = n+ (2^{\log_2n+1}-1)/(2-1) \lessorequal n+2*n = 3n$$
$C(n) \lessorequal 3n$
costo ammortizzato: $C(n)/n \lessorequal 3n/n = 3 = \theta(1)$

Realizzazione tramite strutture collegate: record e puntatori.
Dati:
- una collezione L di n record contenuti (key, info, next, prev) dove next e prev sono puntatori al successivo e al precedente elemento nel record
- Un attributo L.head punta al primo elemento della lista. Se L.head == NULL la lista è vuota

``` C
insert (Dizionario L, Elem v, Chiave k){
	p.next = L.head;
	if(L.head != NULL) L.head.prev = p;
	L.head = p;
	p.prev = NULL:
}

search (Dizionario L, Chiave k){
	x = L.head;
	while(x != NIL and x.key != k) x = x.next;
	if(x != NIL) return x.info;
	else return NIL;
}
``` 

Funzione di terminazione è una funzione a valori naturali che decresce strettamente ad ogni iterazione del ciclo.



24/10
``` c
delete(Dizionario L, Chiave K){
	x = l.head;
	while(x!=NIL)
		if(x.key == k)
			if(x.next != NIL)
				x.next.prev = x.prev;
			if(x.prev != NIL)
				x.prev.next = x.next;
			else l.head = x.next;
			temp = x;
			x = x.next;
			***(temp);
		else x = x.next;
}
``` 
Il tempo di esecuzione è t(n) = $\theta(n)$


``` c
a(int n){
	s = 0;
	for(int i = 1; i < n; i++) s = s + b(i);
	return s;
}

b(int n){
	s = 0;
	for(int j = 1; j < n; j++) s = s + 1;
	return s;
}
``` 



```C
struct Node{
	int key;
	Node* left;
	Node* right;
	Node* prev;
}
typedef Node* PNode;

int intermedi(PNode r){
	int sumSottoalbero;
	return intermediAux(r, 0, sumSottoalbero);
}

int intermediAux(PNode u, int sump, int& sumSottoalbero){
	if(u == nullptr){
		sumSottoalbero = 0;
		return 0;
	}
	
	int numsx, numdx, sumsx, sumdx;
	numsx = intermediAux(u->left, sump+u->key, sumsx);
	numdx = intermediAux(u->right, sump+u->key, sumdx);
	sumSottoalbero = sumsx + sumdx + u->key;
	if(sumSottoalbero == sump) return 1 + numsx + numdx;
	return numsx + numdx;
}
```
Complessità? vedi Onenote