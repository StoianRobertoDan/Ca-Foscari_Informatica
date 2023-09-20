1. Somma dato il numero di  addendi
		Ritorno true se è possibile sommare `add` addendi per formare la somme `sum`
```cpp
#include<iostream>

struct Cella{
  int info;
  Cella* next;
};

typedef Cella* Lista;

void append(Lista& l, int elem) {
  if (l==nullptr) {
    l = new Cella{elem, nullptr};
  }
  else 
    append(l->next, elem);
}

void readlist(Lista& l) {
  int q, e;

  std::cin>>q;

  while (q>0) {
    std::cin>>e;
    append(l, e);
    q--;
  }
}

bool findsum(Lista l, int sum, int add) {
    if(add==0 and sum==0) return true;
    else if(add==0 and sum!=0) return false;
    if(l==nullptr) return false;
    return findsum(l->next, sum-l->info, add-1) or findsum(l->next, sum, add);
}
```

Metodo della prof
```cpp
bool findsum(Lista l, int sum, int add) {
	if(add==0 and sum==0) return true;
	if(l==nullptr) return false;
	int val = l->info;
	bool res1 = findsum(l->next, sum-val, add-1);
	bool res2 = findsum(l->next, sum, add);
	return res1 or res2;
}
```

2. Elimina le doppie
		Implementare un metodo ricorsivo che elimini tutte le ricorrenze di elementi identici consecutivi, lasciandone uno
```cpp
#include<iostream>

class ListInt{
	public:
		ListInt();  //Deafult Constructor
		~ListInt();  //Destructor
		ListInt(const ListInt& s); //Copy constructor

		void prepend(int el);
		void append(int el);
		void print() const;
		void read();

		void remove_consec();

		int& at(unsigned int pos);
		const int& at(unsigned int pos) const;
	private:
		struct Cell {
			int info;
			Cell* next;
		};
		typedef Cell* Pcell;
		Pcell head;
		int dummy;

		void destroy(Pcell pc);
		Pcell copy(Pcell source);

		void remove_consec_rec(Pcell& l); 
};

ListInt::ListInt() {
	head = nullptr;
}

ListInt::~ListInt() {
	destroy(head);
}
			
void ListInt::destroy(Pcell pc) {

	if (pc!=nullptr) {
		destroy(pc->next);
		delete pc;
	}
}

void ListInt::read() {
	destroy(head);
	head=nullptr;
	int elem;
	std::cin>>elem;

	for (int i=0; i<elem; i++) {
		int e;
		std::cin>>e;
		append(e);
	}
}


void ListInt::append(int el) {
	if (head==nullptr) 
		prepend(el);
	else {
		Pcell pc = head;
		while (pc->next!=nullptr)
			pc = pc->next;
		pc->next = new Cell;
		pc->next->info = el;
		pc->next->next = nullptr;
	}
}

void ListInt::prepend(int el) {
	Pcell newone = new Cell;
	newone->info = el;
	newone->next = head;
	head = newone;
}

void ListInt::print() const {
	Pcell pc = head;
	while (pc) {
		std::cout<<pc->info<<std::endl;
		pc = pc->next;
	}
}


ListInt::ListInt(const ListInt& s) {
	head = copy(s.head);
}

ListInt::Pcell ListInt::copy(Cell* source) {
	if (source == nullptr)
		return nullptr;
	else {
		Pcell dest = new Cell;
		dest->info = source->info;
		dest->next = copy(source->next);
		return dest;
	}
}


int& ListInt::at(unsigned int pos) {
	Pcell pc = head;
	while (pc!=nullptr && pos>0) {
		pc = pc->next;
		pos--;
	}

	if (pc) 
		return pc->info;
	else
		return dummy;
}

const int& ListInt::at(unsigned int pos) const {
	Pcell pc = head;
	while (pc!=nullptr && pos>0) {
		pc = pc->next;
		pos--;
	}

	if (pc) 
		return pc->info;
	else
		return dummy;
}

void ListInt::remove_consec() {
    remove_consec_rec(head);
}

void ListInt::remove_consec_rec(Pcell& p) {
    if(p==nullptr or p->next == nullptr) return;
    if(p->info == p->next->info){
        Pcell punt = p->next;
        p->next = punt->next;
        delete punt;
        remove_consec_rec(p);
    }
    remove_consec_rec(p->next);
}
```

alternativa:
```cpp
void ListInt::remove_consec_rec(Pcell& p) {
    if(p==nullptr or p->next == nullptr) return;
    if(p->info == p->next->info){
        Pcell temp = p;
        p= p->next;
        delete punt;
        remove_consec_rec(p);
    }
    remove_consec_rec(p->next);
}
```


3. Carello oggetti
		Creare i metodi per aggiungere oggetti nel carrello, mettere il output una stringa con i componenti del carrello e calcolare il costo totale.

```cpp
#include <iostream>
#include <vector>
#include <string>

using namespace std;
    
class Carrello{
public:
    Carrello(){
        head = nullptr;
    }
    
    ~Carrello() {
    }

    void add(string  desc, int qnt, double cost) {
        append(head, desc, qnt, cost);
    }

    string print_carrello() {
        if(head==nullptr){
            return "Carrello vuoto";
        }
        Obj copy = head;
        string carello = copy->ogg;
        while(copy->next!=nullptr){
            carello += ", " + copy->next->ogg;
            copy = copy->next;
        }
        return carello;
    }

    double total() {
        if(head==nullptr){
            return 0;
        }
        double tot = 0;
        Obj copy = head;
        while(copy!=nullptr){
            tot += (copy->num * copy->cost);
            copy = copy->next;
        }
        return tot;
    }

private:
    struct Oggetti{
        string ogg;
        int num;
        double cost;
        Oggetti* next;
    };
    typedef Oggetti* Obj;
    Obj head;
    
    void append(Obj& l, string  desc, int qnt, double cost){
        if(l==nullptr){
            l = new Oggetti{desc, qnt, cost, nullptr};
        } else append(l->next, desc, qnt, cost);
    }
};

```

alternativa:
```cpp
public:
    Carrello(){
        head = nullptr;
    }
    
    ~Carrello() {
    }

    void add(string  desc, int qnt, double cost) {
        Oggetti nuovo = {desc, qnt, cost};
        /*nuovo.ogg = desc;
	        nuovo.num = qnt;
	        nuovo.cost = cost;
        */
        items.pushback(nuovo);
    }

    string print_carrello() {
        if(items.size()) return "Carrello vuoto";
        string out_str = item.desc;
        for(auto el:items){
            out_str += el.desc + ", ";
        }
        return out_str.substr(0, out_str.length()-2);
    }

    double total() {
        if(head==nullptr){
            return 0;
        }
        double tot = 0;
        Obj copy = head;
        while(copy!=nullptr){
            tot += (copy->num * copy->cost);
            copy = copy->next;
        }
        return tot;
    }
private:
    struct Oggetti{
        string ogg;
        int num;
        double cost;
    };
	vector<Oggeti> items;
```