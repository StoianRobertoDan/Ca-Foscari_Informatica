class stringPascal parte da 1 e non da 0 perchè il primo spazio è dedicato ad un numero (di caselle successive?).

```cpp
class StringPascal{
public:
	stringPascal()
	stringPascal(const StringPascal& s) //copyconstructor
	void stampa();
	void set(const string s);
	void setsize(int dim);
	void setchar(int pos, char c);
	char getchar(int pos);
private:
	char buff[256];
};

void StringPascal::set(const string& s){
	if(s.length() <= 255) 
		buff[0] = s.length();
	else buff[0] = 255;
	
	for(int i = 0; i <= buff[0]; i++){
		buff[i] = s.at(i-1);
	}
}

void stringPascal::stampa(){
	for(int i = 0; i <= buff[0]; i++){
		std::cout<< buff[i];
	}
}

StringPascal::StringPascal(){
	buff[0] = 0;
}

StringPascal::StringPascal(const string son){
	set(son);
}

StringPascal::StringPascal(const stringPascal& copy){
	buff = new char[256];  //buff senza niente è il buff di quello che si sta creando. <nome>.buff è di quello specificato
	for(int i = 1; i <= s.buff[0]; i++){
		buff[i] = s.buff[i];
	}
}

int main(){
	stringPascal p;
	p.set("hello");
	p.setchar(1, "h");
	p.print();

	stringPascal* p = new stringpPascal; //crea 2 oggetti: un puntato p e una stringPascall
	string cpps = "hi";
	stringPascal z(cpps);
	
}



```


```
StrPascal s(cstring);
StrPascal t = s;
```
shallow copy: quando ci sono puntatori li copia ma senza duplicare la cosa puntata, cosi due puntatori puntano alla stessa cosa e se uno fa la free del puntatore l'altra può dare errore. esempio se si chiama il distruttore di s e t, t viene eliminato per primo, fa la free di quell'area di memoria, quando cerca di farlo anche s si ritrova a fare la free di un'area di memoria già liberata e da errore.

attenzione perchè succede anche chiamando una funzione per copia (copy constructor) perchè una volta finita la funzione essa elimina la copia ma così libera anche l'area di memoria allocata. non succede con il passaggio per reference perchè a fine funzione non viene chiamato il distruttore.