1. Vettore di primi
		Scrivere una funzione che riempie un vettore lungo n con altrettanti numeri primi (non ripetuti e consecutivi)
```cpp
#include<iostream>


struct Cella_circ{
  int info;
  struct Cella_circ* next;
};


typedef Cella_circ* Lista_circ;


void add(Lista_circ& lista, int x) {
  Lista_circ nuovo = new Cella_circ;
  nuovo->info = x;
  if (lista==nullptr) {
    nuovo->next = nuovo;
    lista = nuovo;
  }
  else {
    nuovo->next = lista->next;
    lista->next = nuovo;
  }
}

//stampa lista
void stampa_lista(Lista_circ l) {
  if (l) {
    Lista_circ pc{l};
    do {
      std::cout<<l->info << " ";
      l=l->next;
    } while (l!=pc);
  }
  std::cout<<std::endl;
}

//distruggi lista
void distruggi(Lista_circ& l) {
  if (l) {  
    Lista_circ supp, sentinella{l};
    do {
      supp = l;
      l=l->next;
      delete supp;
    } while (l!=sentinella);
    l = nullptr;
  }
}


//leggi lista
void leggi_lista(Lista_circ& l) {
  int elem, n;
  std::cin>>n;
  while (n>0) {
    std::cin>>elem;
    add(l, elem);
    n--;
  }
}





void rimuovi_occ(Lista_circ& l, int elem) {
    if(l == nullptr) return;
    Lista_circ punt = l->next;
    while (punt != l){
        if(punt->next->info == elem){
            if(punt->next == l){
                l = l->next;
            }
            Lista_circ punt_m = punt->next;
            punt->next = punt_m->next;
            delete punt_m;
        }
        if(punt->next->info != elem) punt = punt->next;
    }
    if(l->info == elem) l = nullptr;
}

```

2. Media mobile
		Dato in input un vettore (passato per copia come const) e un valore k, scrivere una funzione lunga come il vettore di input dove in ogni casella è calcolata la media del range dal k valore a sinistra al k valore a destra. non si considerino valori esterni al vettore.
		(dato un vettore {0, 1, 2} e k=1, il vettore risultante sarà {0.5, 1, 1.5})

```cpp
#include <iostream>

struct Cella{
  int info;
  struct Cella* next;
};


typedef struct Cella* Lista;


//aggiunta in testa alla lista
void prepend(Lista& lista, int x) {
  Lista nuovo = new Cella;
  nuovo->info = x;
  nuovo->next = lista;
  lista = nuovo;
}

//aggiunta in coda alla lista
void append(Lista& l, int data) {
  if (!l)            
    l = new Cella{data, nullptr};
  else append(l->next, data);
}

//stampa lista
void stampa_lista(Lista l) {
  if (l) {
    std::cout<<l->info<<std::endl;
    stampa_lista(l->next);
  }
}

//distruggi lista
void distruggi(Lista& l) {
  Lista supp;
  while(l) {
    supp = l;
    l = l->next;
    delete supp;
  }
}

void leggi(Lista& l) {
    distruggi(l);
    int elem;
    std::cin>>elem;
    
    while (elem > 0) {
        int e;
        std::cin >> e;
        append(l, e);
        elem--;
    }
}

void elimina_dup(Lista& l)
{
    Lista punt = l;
    while(punt != nullptr){
        if(punt->next != nullptr && punt->info == punt->next->info){
            Lista punt_m = punt->next;
            punt->next = punt_m->next;
            delete punt_m;
        }
        else punt = punt->next;
    }
}
```

3. Anagrammi
		Date due stringhe (passati per copia) scrivere una funzione che controlla se sono anagrammi. Bisogna ignorare gli spazi e nelle stringhe contengono solo caratteri alfabetici minuscoli.

```cpp
#include<string>
#include<iostream>
#include<stack>

using namespace std;

bool bilanciata(string&);

bool bilanciata(string& s){
    if(s.empty()) return true;
    stack<char> S;
    //cout << s;
    for(int i = 0; i < s.length(); i++){
        if(s[i] >= 'A' && s[i] <= 'Z') S.push(s[i]);
        else if(S.empty()) return false;
        else if(s[i] >= 'a' && s[i] <= 'z'){
            if(S.top() != s[i] - 32) return false;
            S.pop();
        }
    }
    
    if(S.empty()) return true;
    else return false;
}
```