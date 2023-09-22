
Il left value può essere usato in ogni caso come un right value ma non viceversa.

``` cpp
int k;
int& foo(int b){
k=b;
return k;
}

foo(7) = 15; //scrive 15 nella variabile globale k

cout << foo(24); //stampa 24 che adesso è il valore di k
```
ritorna l'oggetto che dentro la funzione si chiama k, non il valore ma l'oggetto stesso (è come se, se le variabili fossero scatole, ritormassi la scatola intera quando si passa con &)

```c
int *foo(int a){
	return &a;
}
```
in c questo potrebbe partire.

classi container (es lista di interi)

``` cpp
class List_int{
	public:
		List_int();
		List_int(const List_int& s);
		void prepend();
		void append()
		bool is_empty() const;
		int& head();  //restituisce l'ggetto della head che può essere modificato
		const int& head() const; 
		void print() const;
		
	private:
		struct Cell{
			int info;
			Cell* next;
		};
		Cell* h;
};

List_int::List_int(){
	h = nullptr;  //liste vuote
}

void List_int::prepend(int e){
	Cell* nuova = new Cell;
	nuova -> info = e;
	nuova -> next = h;
	h = nuova;
}

List_int::~List_int(){
	Cell* pc=h;
	while(pc!=nullptr){
		h = h -> next;
		delete pc;
		pc = h;
	}
}

const int& List_int::head() const{
	return h->info;
}

List_int(const List_int& s){
	
	pc = pc.h;
}
```



``` cpp
class List_int{
	public:
		List_int();
		List_int(int el);
		List_int(const List_int& source);
		void prepend(int el);
		void append(int el)
		
		std::string convert_to_string();
		void tail(List_int& res);
		void& first();
		const int& first() const; 
		bool is_empty() const;
		
		bool equal(const List_int& l) const;
		
		void concat(List_int& l);
		void print() const;

		void remove_first();
		~List_int();
	
	private:
		struct Cella{
			int info;
			Cella* next;
		};
		Cella* l;
		Cella* last;
};

bool List_int::equal(const List_int& comp) const{
	Cella* cp1 = l;
	Cella* cp2 = comp.l;
	
	while(pc1!=nulref and pc2!=){
	}
	return (cp1 == cp2);
}



List_int::List_int(){
	h = nullptr;  //liste vuote
}

void List_int::prepend(int e){
	Cell* nuova = new Cell;
	nuova -> info = e;
	nuova -> next = h;
	h = nuova;
}

List_int::~List_int(){
	Cell* pc=h;
	while(pc!=nullptr){
		h = h -> next;
		delete pc;
		pc = h;
	}
}

const int& List_int::head() const{
	return h->info;
}

List_int(const List_int& s){
	
	pc = pc.h;
}
```


``` cpp
class List_int{
	public:
		List_int();
		//List_int(int el);
		List_int(const List_int& l);
		void prepend(int el);
		void append(int el)
		
		void stampa();
	
	private:
		struct Impl;
		Impl* Impl;
};


//IN UN ALTRO FILE

struct List_int::Impl(){
	std::vector<int> v;
	double a;
};

List_int::List_int(){
	pimpl = new Impl;
	pimpl->a = 3.14;
}

List_int::List_int(const List_int& l){
	pimmpl = new Impl;
	pimpl->v = l.pimpl->;
}

List_int::~List_int(){
	delete pimpl;
}

void List_int::prepend(int el){
	piml->v.resize(pimpl->v.size()+1);
	for(int i = pimpl.size()-1; i>0 ; i--){
		pimpl->v.at
	}
}

void List_int::append(){
	pimpl->
}


//IN UN ALTRO FILE
```


```cpp
class List_int{
public:
	...
	int elimina_fondo(int n);
	
private:
	struct Cella{
		int info;
		Cella* next;
	}
	Cella* l;
	typedef Cella* Pcella;
	int elimina_fondo_ric(Pcella& list, int n);
};

int List_int::elimina_fondo(int n){
	elimina_fondo_ric(l, n);
}

int List_int::elimina_fondo_ric(Pcella& list, int n){
	if(list==nullptr) return 0;
	else{
		int canc = elimina_fondo_ric(list->next, n);
		if(canc < n){
			delete list;
			list =  nullptr;
			return canc+1;
		}
		return n;
	}
}

```