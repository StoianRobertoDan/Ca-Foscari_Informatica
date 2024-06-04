
```cpp
#include<iostream>
#include<string>

using namespace std;

class Dict{
  public:
    Dict();
    ~Dict();

    int& at(string pos);
    void print() const;
    bool operator<=(const Dict& d) const;
    bool operator==(const Dict& d) const;
    Dict& operator+=(const Dict& d);

  private:
    struct Cella{
      string key;
      int val;
      Cella* next;
    };

    typedef Cella* pCella;

    pCella head;



};

//Costruttore di default. Non cambiare
Dict::Dict() {
  head = nullptr;
}

//Distruttore: Non cambiare
Dict::~Dict() {
  pCella pc;
  while (head) {
    pc = head;
    head = head->next;
    delete pc;
  }
}

//Stampa gli elementi. Non cambare
void Dict:: print() const {
  cout<<"OUTPUT"<<endl;
  pCella pc = head;

  while (pc) {
    cout<<pc->key<<":"<<pc->val<<endl;
    pc = pc->next;
  }
  cout<<"---"<<endl;
}

//Esercizio 1
//Implementare: il metodo at ritorna una reference al
//campo value del nodo con la key uguale a pos se questa esiste
//altrimenti crea un nuovo nodo in coda alla lista che contiene
//come key pos e come valore 0, e ritorna la reference al campo
//value di questo nuovo nodo
int& Dict::at(string pos) {
    if(!head)
        head = new Cella{pos, 0, nullptr};
    pCella current = head;
    while(current->next){
        if(pos == current->key) return current->val;
        current = current->next;
    }
    if(pos == current->key) return current->val;
    current->next = new Cella{pos, 0, nullptr};
    return current->next->val;
}

//Esercizio 2
//Ritorna true se *this ha un sottoinsieme degli elementi
//di d, cioe' tutte le coppie key,value di *this sono anche
//in Dict (anche in ordine diverso) 
bool Dict::operator<=(const Dict& d) const {
    pCella  punt = head;
    bool found;
    while(punt){
        pCella dhead = d.head;
        found = false;
        while(dhead and !found){
            if(dhead->key == punt->key and dhead->val == punt->val) found = true;
            dhead = dhead->next;
        }
        if(!found) return false;
        punt = punt->next;
    }
    return true;
}

//Esercizio 2
//Ritorna true se *this ha gli stessi elementi
//di d anche in ordine diverso
bool Dict::operator==(const Dict& d) const {
    pCella  punt = d.head;
    bool found;
    while(punt){
        pCella thead = head;
        found = false;
        while(thead and !found){
            if(thead->key == punt->key and thead->val == punt->val) found = true;
            thead = thead->next;
        }
        if(!found) return false;
        punt = punt->next;
    }
    if(*this <= d) return true;
    else return false;
}


//Esercizio 3
//Aggiunge tutti gli elementi del parametro formale la cui chiave
//non e' gia' presente in *this. 
//In altre parole, per ogni elemento di d, se la sua key e' gia'
//presente in *this, allora viene ignorato, se invece non e'
//presente, va aggiunto in coda. Al termine si ritorna *this

Dict& Dict::operator+=(const Dict& d) {
    pCella punt = d.head;
    while(punt){
        if(this->at(punt->key) == 0) this->at(punt->key) = punt->val; 
        punt = punt->next;
    }
  return *this;
}
```