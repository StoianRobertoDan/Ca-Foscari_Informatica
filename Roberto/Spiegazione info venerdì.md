```cpp
//in file.hpp
class ListDL{
    public:
        ListDL();
        ListDL(const ListDL& s);
        ~ListDL();
        //ListDL(pimpl &head = nullptr, pimpl &tail = nullptr, int size =0){}
        void append(int e);
        void prepend(int e);
        void print() const;
        int size() const;
        const int& at(int pos) const;
    private:
        struct impl;
        impl* pimpl;
};


//in file .cpp
#include"ListDL.hpp"

struct cella{ // la firma é: tipo della struct oppure metodo, nome della classe, :: , infine il nome della struct implementata all'interno della classe
    int info;
    cella* next;
    cella* prev;
};
typedef cella* pcella;

struct ListDL::impl{
    pcella head;
    pcella tail;
    int size; // rappresenta i numeri nodi 
};
// typedef impl* people; //?????????????????????    Perché é sbagliato   ???????????????????????????????

ListDL::ListDL(){ // non posso scrivere con il metodo impl ListDL::ListDL():pimpl->head = nullptr; pimpl->tail = nullptr; pimpl->size = 0;{}
    pimpl = new impl;
    pimpl->head = nullptr;
    pimpl->tail = nullptr;
    pimpl->size = 0;
}
//ListDL::ListDL(pimpl &head = nullptr, pimpl &tail = nullptr, int size = 0){}

ListDL::ListDL(const ListDL& s){
    pimpl = new impl;
    pimpl->head = nullptr;
    pimpl->tail = nullptr;
    pcella h = s.pimpl->head;
    while(h != nullptr){
        append(h->info);
        h = h->next;
    }
}

ListDL::~ListDL(){
    pcella pc = pimpl->head;
    while(pc != nullptr){
        pimpl->head = pimpl->head->next;
        delete(pc);
        pc = pimpl->head;
    }
    delete(pimpl);
}

/* Seconda versione del distruttore che assolve alla sua funzione
ListDL::~ListDL(){
    pcella pc = pimpl->head;
    while(pc != nullptr){
        pc = pc->next;
        delete(pimpl->head);
        pimpl->head = pc;
    }
    delete(pimpl);
}
*/

void ListDL::append(int e){ // aggiungo alla fine della lista
    pimpl->size++;
    pcella nuova = new cella;
    nuova->next = nullptr;
    nuova->info = e;
    nuova->prev = pimpl->tail;
    if(pimpl->tail != nullptr) pimpl->tail ->next = nuova;
    else pimpl->head = nuova;
    pimpl->tail = nuova;
}

void ListDL::prepend(int e){ // aggiungo all'inizio della lista
    pimpl->size++;
    pcella nuova = new cella;
    nuova->prev = nullptr;
    nuova->info = e;
    nuova->next = pimpl->head;
    if(pimpl->head != nullptr) pimpl->head->prev = nuova;
    else pimpl->tail = nuova;
    pimpl->head = nuova;
}

int ListDL::size() const{
    return pimpl->size;
}

int& ListDL::at(int pos){
	if(pos < 0) pos = size() + pos;
	if(pos < 0) throw std::invalid.argument("invalid position");

	pcella pc = pimpl->head;
	while(pc != nullprt && pos > 0){
		pc = pc->next;
		pos--;
	}
	if(pc != nullprt) return pc->inf0;
	else throw std::invalid.argument("invalid position");
}

void ListDL::remove(int pos){
	if(pos < 0) pos = size() + pos;
	if(pos < 0) throw std::invalid.argument("invalid position");

	pcella pc = pimpl->head;
	while(pc != nullprt && pos > 0){
		pc = pc->next;
		pos--;
	}
	if(pc != nullprt) {
		if(pc->next ==  nullprt) pimpl->tail = pc-> prev;
		else pc->next->prev = pc->prev;
		if(pc->prev ==  nullprt) pimpl->head = pc-> next;
		else pc->prev->next = pc->next;
		delete pc;
		pimpl->size -1;
	}
}
```