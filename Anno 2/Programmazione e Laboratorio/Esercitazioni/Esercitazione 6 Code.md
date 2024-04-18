
```cpp
#include<iostream>

class List_uguali{
  public:
    List_uguali();
    List_uguali(const List_uguali& l);

    void aggiungi(int elem);
    void rimuovi(int elem);
    void stampa() const; 

    List_uguali operator+(const List_uguali& l) const;
    List_uguali& operator=(const List_uguali& l);

    ~List_uguali();

  private:
    struct Cella;
    typedef Cella* pCella;

    pCella list;

};

struct List_uguali::Cella{
  int info;
  pCella next;
};

//Costruttore di default: non modificare il metodo
List_uguali::List_uguali() {
  list = nullptr;
}

//Distruttore: non modificare il metodo
List_uguali::~List_uguali() {
  pCella p=list;
  while(p) {
    p=p->next;
    delete list;
    list=p;
  }
}

//Implementare: Esercizio 1
//Aggiungi un elemento alla lista
void List_uguali::aggiungi(int elem) {
    if(!list) list = new Cella{elem, nullptr};
    else{
        pCella head = list;
        while(head->info != elem and head->next) 
            head = head->next;
        pCella punt = nullptr;
        if(head->info == elem) punt = head->next;
        pCella cell = new Cella{elem, punt};
        head->next = cell;
    }
}

//Implementare: Esercizio 1
//Stampa gli elementi della lista
void List_uguali::stampa() const {
    pCella head = list;
    while(head) {
        std::cout<< head->info << std::endl;
        head = head->next;
    }
}

//Implementare: Esercizio 1
//Rimuovi un elemento dalla lista
void List_uguali::rimuovi(int elem) {
    if(!list) return;
    if(list->info == elem){
        pCella app = list;
        list = list->next;
        delete app;
    }
    else{
        pCella head = list;
        while(head->next->info != elem && head->next->next){
            head = head->next;
        }
        if(head->next->info == elem){
            pCella app = head->next;
            head->next = head->next->next; 
            delete app;
        }
    }   
}

//Implementare: Esercizio 2
//Ridefinizione del copy constructor
List_uguali::List_uguali(const List_uguali& l) {
    list = nullptr;
    if(!l.list) return;
    pCella lh = l.list;
    while(lh){
       aggiungi(lh->info);
       lh = lh->next;
    }
}

//Implementare: Esercizio 3
List_uguali& List_uguali::List_uguali::operator=(const List_uguali& l) {
    pCella p = list;
    while(p) {
        rimuovi(p->info);
        p = list;
    }
    pCella lh = l.list;
    if(!lh) return *this;
    while(lh){
       aggiungi(lh->info);
       lh = lh->next;
    }
    return *this;
}


//Implementare: Esercizio 3
List_uguali List_uguali::List_uguali::operator+(const List_uguali& l) const{
    List_uguali res(*this);
    pCella lh = l.list;
    while(lh){
        res.aggiungi(lh->info);
        lh = lh->next;
    }
    return res;
}
```