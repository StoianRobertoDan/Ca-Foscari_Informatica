
```cpp
#include<iostream>
#include<string>

using namespace std;

/*Classe lista di stringhe ordinate alfabeticamente in modo
 * crescente. La lista e' doppiamente concatenata*/

class ListStrings{
public:
  ListStrings();
  ListStrings(ListStrings&& ls);
  ~ListStrings();
  void print_forward() const;
  void print_reversed() const;
  void add(const string& s);
  ListStrings& operator=(const ListStrings& ls);
  ListStrings operator+(const ListStrings& ls) const;
private:
  struct Cell{
    string info;
    Cell* next;
    Cell* prev;
  };
  Cell* head; //puntatore alla prima cella
  Cell* tail; //puntatore all'ultima cella
};


//Default constructor
ListStrings::ListStrings() {
  head = nullptr;
  tail = nullptr;
}


//Move constructor
ListStrings::ListStrings(ListStrings&& ls) {
  head = ls.head;
  tail = ls.tail;
  ls.head = nullptr;
  ls.tail = nullptr;
}

//stampa da head a tail
void ListStrings::print_forward() const{
  Cell* ptr=head;
  while (ptr) {
    cout<<ptr->info<<endl;
    ptr = ptr->next;
  }
}

//stampa da tail a head
void ListStrings::print_reversed() const{
  Cell* ptr=tail;
  while(ptr) {
    cout<<ptr->info<<endl;
    ptr=ptr->prev;
  }
}


//Destructor: 
ListStrings::~ListStrings() {
    Cell* temp = head;
    Cell* temp_next = temp->next;
    while(temp!=nullptr){
        temp_next = temp->next;
        delete temp;
        temp = temp_next;
    }
}


void ListStrings::add(const string& s) {
    if(head == nullptr){
        head = new Cell{s, nullptr, nullptr};
        tail = head;
    }
    else if(s < head->info) {
        Cell* temp = new Cell{s, head, nullptr};
        head->prev = temp;
        head = temp;
    }
    else if(s > tail->info) {
        Cell* temp = new Cell{s, nullptr, tail};
        tail->next = temp;
        tail = temp;
    }
    else{
        Cell* temp = head;
        while (s > temp->info && temp->next!=nullptr){
            temp = temp->next;
        }
        Cell* nuova = new Cell{s, temp, temp->prev};
        temp->prev->next = nuova;
        temp->prev = nuova;
    }
}
       
ListStrings& ListStrings::operator=(const ListStrings& ls) {
    Cell* temp = head;
    while(temp != nullptr){
        Cell* temp_other = temp->next;
        delete temp;
        temp = temp_other;
    }
    head = nullptr;
    tail = nullptr;
    temp = ls.head;
    while(temp != nullptr){
        add(temp->info);
        temp = temp->next;
    }
  return *this;
}

ListStrings ListStrings::operator+(const ListStrings& ls) const {
   //Scrivi qui il tuo codice Esercizio 3
  ListStrings res;
  if(head == nullptr) res = ls; 
  else if(ls.head == nullptr) res = *this;
  else{
      Cell* temp = ls.head;
      res = *this; 
      while(temp != nullptr){
          res.add(temp->info);
          temp = temp->next;
      }
  }
  return res;
}
```
