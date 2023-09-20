
```cpp
#include<iostream>
#include<string>

class Number{
  public:
    Number();
    Number(unsigned int m);
    Number(const Number& l);
    Number(std::string s);
    ~Number();

    void print() const;

    Number operator+(const Number& x) const;
    Number operator*(const Number& x) const;
    bool operator==(const Number& x) const;
    bool operator!=(const Number& x) const;
    Number& operator=(const Number& x);


  private:
    //Non modificare
    struct Cell{
      char info;
      Cell* next;
    };

    typedef Cell* List;

    List n;
    List sum(List l1, List l2, char carry) const;
    List convert(unsigned int m);
    void print_rec(List l) const;

    
    //Parte modificabile (ma attenzione: ora è progettata per guidarvi)
   
    void destroy(List h);
    List copy(const List pc);
    bool equal(List l1, List l2) const;


};

//Costruttore di default, 0 e' codificato con la lista vuota
Number::Number() {
  n=nullptr;
}

//converte un unsigned int nella lista richiesta
Number::Number(unsigned int m) {
  n = convert(m);
}

//studia questa funzione per comprendere completamente la rappresentazione nel numero
//e' un bell'esempio di ricorsione
Number::List Number::convert(unsigned int m) {
  if (m==0)
    return nullptr;
  else {
    List pc = new Cell;
    pc->info = m%10;
    pc->next = convert(m/10);
    return pc;
  }
}

//stampa la lista: siccome le cifre meno significative sono in testa, devo stampare al contrario
void Number::print() const {
  if (n==nullptr) 
    std::cout<<"0";
  else
    print_rec(n);
}

//parte ricorsiva della stampa
void Number::print_rec(List l) const {
  if (l) {
    print_rec(l->next);
    std::cout<<static_cast<char>(l->info+'0'); //Ecco il type casting explicito in C++
  }
}

//distruttore
Number::~Number() {
  destroy(n);
}

//funzione di disruzione ricorsiva
void Number::destroy(List h) {
  if (h) {
    destroy(h->next);
    delete(h);
  }
}

//primo metodo da implementare: dato un numero codificato con una stringa
//scritto in modo che la cifra piu' significativa e' nella prima posizione
//generare un Number. Attenzione non fare la conversione string->int->list
//perche' potresti avere errori di overflow
Number::Number(std::string s) {
    n = nullptr;
    for(int i = s.size(); i > 0; --i){
        List pc = new Cell;
        pc->info = s[s.size() - i] - '0';
        pc->next = n;
        n = pc;
    }
}

//secondo metodo da implementare: copy constructor
//consigliato far uso della funzione privata ricorsiva copy
//potrebbe esserti utile anche per l'assegnamento!
Number::Number(const Number&x) {
    n = copy(x.n);
}


Number::List Number::copy(const List pc) {
    //List head = n;
    if(pc == nullptr) return nullptr;
    else{
        //List rev = copy(pc->next);
        List nuova = new Cell;
        nuova->info = pc->info;
        nuova->next = copy(pc->next);
        n = nuova;
    }
    return n;
}


//l'operatore + non va modificato. Deve utilizzare il meotodo sum come indicato
Number Number::operator+(const Number& x) const {
  Number res;
  res.n = sum(x.n, n, 0);
  return res;
}

//Questa funzione deve essere ricorsiva. Implementala con cura. Ricorda
//che l'ultimo carry potrebbe essere diverso da 0
Number::List Number::sum(List l1, List l2, char carry) const {
    if((l1 == nullptr and l2 == nullptr) and carry == 0) return nullptr;
    else{
        char ris = carry;
        if(l1 != nullptr) ris += (l1->info);
        if(l2 != nullptr) ris += (l2->info);
        
        if(ris >9) carry = 1;
        else carry = 0;
        
        List pc = new Cell;
        pc->info = ris%10;
        /*if(l1 == nullptr and l2 != nullptr) pc->next = sum(nullptr, l2->next, carry);
        else if( l2 == nullptr and l1 != nullptr) pc->next = sum(l1->next, nullptr, carry);
        else pc->next = sum(l1->next, l2->next, carry);*/
        pc->next = sum(l1 ? l1->next : nullptr, l2 ? l2->next : nullptr, carry);
        return pc;
    }
}


//operatore di assegnamento. Segui la traccia
Number& Number::operator=(const Number& x) {
  if (this!=&x) {
    destroy(n);
    n = copy(x.n);
  }
  return *this;
}


//La seguente funzione puo' essere modificata, ma e'
//consigliato usare la equal sviluppata ricorsivamente
bool Number::operator==(const Number& x) const{
  return equal(x.n, n);
}

//Da sviluppare
bool Number::equal(List l1, List l2) const {
    if(l1 == nullptr && l2 == nullptr) return true;
    else if(l1 == nullptr && l2 != nullptr || l1 != nullptr && l2 == nullptr) return false;
    else if(l1->info != l2->info) return false;
    return equal(l1->next, l2->next);
}

//Metodo velore per implementare il != 
bool Number::operator!=(const Number& x) const{
  return !(*this==x);
}

int pow(int base, int exp){
    if(exp == 0) return 1;
    else return base * pow(base, exp-1);
}

//Fare il prodotto x*y significa sommare x+x+x+..+x (y volte...)
//non il modo piu' efficiente, ma il piu' facile
//Ricorda che tutte le operazioni vanno fatte coi numbers!
Number Number::operator*(const Number& x) const{
    Number res;
    List pc = x.n;
    int numb = 0, cont = 0;
    while(pc != nullptr){
        numb += pc->info*pow(10, cont);
        cont++;
        pc = pc->next;
    }
    //std::cout<< numb << std::endl;
    for(int i = 0; i < numb; i++){
        res = res + *this;
    }
  
    return res;
}

Number opera(Number x, Number y) {
  return x*y;
}


int main() {
  std::string s1, s2;
  std::cin>>s1;
  std::cin>>s2;
  Number n1(s1), n2(s2); 
  Number n3=24593;

  n3 = opera(n1, n2);

  n1.print(); 
  std::cout<<std::endl;
  n2.print();
  std::cout<<std::endl;
  n3.print();
  std::cout<<std::endl;
  if (n1==n2) 
    std::cout<<"Numeri uguali inseriti"<<std::endl;
 

  return 0;
}
```

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

		bool set_zero_neg();

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

		bool set_zero_neg_rec(Pcell l);

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


bool ListInt::set_zero_neg(){
    return set_zero_neg_rec(head);
}

bool ListInt::set_zero_neg_rec(Pcell l) {
    if(l == nullptr) return false;
    bool neg = set_zero_neg_rec(l->next); 
    if(l->info < 0 and !neg) return true;
    else if(l->info < 0 and neg) l->info = 0;
    return neg;
}

```