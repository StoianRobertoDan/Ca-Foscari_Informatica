1. Vettore di primi
		Scrivere una funzione che riempie un vettore lungo n con altrettanti numeri primi (non ripetuti e consecutivi)
```cpp
#include<iostream>

struct Cell{
  int info;
  Cell* next;
};

typedef Cell* List;

void append(List& l, int elem) {
  if (l==nullptr) {
    l = new Cell{elem, nullptr};
  }
  else 
    append(l->next, elem);
}


void readlist(List& l) {
  int q, e;

  std::cin>>q;

  while (q>0) {
    std::cin>>e;
    append(l, e);
    q--;
  }
}

void destroy(List& l) {
  if (l) {
    destroy(l->next);
    delete l;
    l=nullptr;
  }
}


void printlist(List l) {
  if (l) {
    std::cout<<l->info<<std::endl;
    printlist(l->next);
  }
}


List merge(List l1, List l2) {
    List l = nullptr, l1_c = l1, l2_c = l2;
    while(l1_c != nullptr || l2_c != nullptr){
        if(l1_c == nullptr) {
            append(l, l2_c->info);
            l2_c = l2_c->next;
        }
        else if(l2_c == nullptr || l1_c->info < l2_c->info ){
            append(l, l1_c->info);
            l1_c = l1_c->next;
        }
        else {
            append(l, l2_c->info);
            l2_c = l2_c->next;
        }
    }
    return l;
}

```

2. Media mobile
		Dato in input un vettore (passato per copia come const) e un valore k, scrivere una funzione lunga come il vettore di input dove in ogni casella è calcolata la media del range dal k valore a sinistra al k valore a destra. non si considerino valori esterni al vettore.
		(dato un vettore {0, 1, 2} e k=1, il vettore risultante sarà {0.5, 1, 1.5})

```cpp
#include<iostream>

struct Cell{
  int info;
  Cell* next;
};

typedef Cell* List;

void addcircular(List& l, int elem) {
  if (l==nullptr) {
    l = new Cell;
    l->info = elem;
    l->next = l;
  }
  else {
    List nuova = new Cell{elem, l->next};
    l->next = nuova;
  }
}



List read_input() {
  int q;
  int el;

  List res = nullptr;

  std::cin >> q;

  while (q>0) {
    std::cin >> el;
    addcircular(res, el);
    q--;
  }

  return res;
}



void print(List l) {
  if (l) {
    std::cout<<l->info << " ";
    print(l->next);
  }
  else 
    std::cout<<std::endl;
}


void destroy(List& l) {
  if (l) {
    destroy(l->next);
    delete l;
    l=nullptr;
  }
}


void linearize(List& l) {
    List l_c = l;
    if(l != nullptr){
        while (l_c->next != l) l_c = l_c->next;
        l_c->next = nullptr;
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