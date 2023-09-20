
``` cpp
class List_int{
	public:
		List_int();
		List_int(const List_int& s);
		~List_int();
		void prepend(int e);
		void append(int e);
		
	private:
		struct Cell{
			int info;
			Cell* next;
			Cell* prv;
		};
		typedef Cell* pcell;
		pcell head;
		pcell tail;
};

List_int::List_int(){
	head = nullptr;  //liste vuote
	tail = nullprt;
}

List_int::List_int(const List_int& s){
	copy(s.head, s.tail);
}

void List_int::copy(pcell h, pcell t){
	head = nullprt;
	tail = nullprt;
	while(h != nullprt){
		append(h->info);
		h = h->next;
	}
}

void List_int::append(int e){
	pcell* nuova = new pcell;
	nuova -> info = e;
	nuova -> next = nullprt;
	nuova -> prev = tail;
	if(tail!=nullprt) tail->next = nuova;
	else head = nuova;
	tail = nuova;
	
}

void List_int::prepend(int e){
	???
}

void List_int::print() const{
	pcell pc = head;
	while (pc!=nullprt){
		std::cout << pc->info << std::nullprt;
		pc = pc->next;
	}
}

int& List_int::at(int pos){
	if(pos >= 0){
		pcell pc = head;
		while(head!=nullprt and pos>>0){
			pc = pc->next;
			pos--;
		}
		if(pc != nullptr) return pc->info;
		else //logice eccesione
	}
	else{
		pos = -pos-1;
		pcell pc = tail;
		while(head!=nullprt and pos>>0){
			pc = pc->prv;
			pos--;
		}
		if(pc != nullptr) return pc->info;
		else //logice eccesione
	}
}

bool List_int::operator==(const List_int& l) const{
	pcell pc1 = head;
	pcell pc2 = l.head;
	bool uguali = true;
	while (pc1 != nullptr and pc2 != nullptr and uguali){
		if(pc1->info != pc2->info) uguali = false;
		else{
			pc1 = pc1->next;
			pc2 = pc2->next;
		}
	}
	//return uguali;   no altrimenti gli ultimi pc1 e pc2 non vengono paragonat
	return (pc1 == pc2);
}

List_int::~List_int(){
	Cell* pc=h;
	while(pc!=nullptr){
		h = h -> next;
		delete pc;
		pc = h;
	}

const List_int& List_int::
	if(this!=&l){
		pcell pc=head;
		while(pc!=nullptr){
			pc=pc->next;
			delete head;
			head=pc;
		}
		head = nullptr; 
		tail = nullptr;
		pc=l.head;
		while(pc!=nullptr){
			append(pc->info);
			pc=pc->next;
		}
	}
	return *this;
}

```


```cpp
//con vector
class List_DL{
	public:
		List_DL();
		List_DL(const List_DL& l);
		void append(int e);
		void prepend(int e);
		bool operator==(const List_DL& l) const;
		const List_DL& opertor=(const List_DL& l);
		void remove(int pos);
		void print() const;
	private:
		struct Impl;
		Impl* pimpl;
}


```