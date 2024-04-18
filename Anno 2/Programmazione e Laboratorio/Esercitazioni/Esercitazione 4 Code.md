
```cpp
class Primes{
private:
    std::vector<int> prime;
    void find_primes(int first, int last);
public:
  Primes(int size) {
      if(size > 0){
        find_primes(0, size);    
      }
      else prime.resize(0);
  }

  int get_prime(int n) {
      if(n >= prime.size()) find_primes(prime.size(), n+1);
      return prime.at(n);
  }
};

void Primes::find_primes(int first, int last){
    prime.resize(last);
    int prim;
    if(first == 0){
        prime.at(0) = 2;
        first++;
        prim = prime.at(first-1)+1;
    }
    else prim = prime.at(first-1);
    while(first < last){
        int j = 1;
        while(j<first){
            if(prim % prime.at(j) == 0){
                prim = prim + 2;
                j = 1;
            }
            else j++;
        }
        prime.at(first++) = prim;
        prim = prim +2;
    }
}
```


```cpp
class Carrello{
public:
    Carrello() {
        product.resize(0);
        quantity.resize(0);
        price.resize(0);
    }
    
    ~Carrello() {
        
    }

    void add(string  desc, int qnt, double cost) {
        product.push_back(desc);
        quantity.push_back(qnt);
        price.push_back(cost);
    }

    string print_carrello() {
        if(product.size() == 0) return "Carrello vuoto";
        string lista = product.at(0);
        for(int i = 1; i < product.size(); i++) lista += ", " + product.at(i);
        return lista;
    }

    double total() {
        double sum = 0;
        for(int i = 0; i < price.size(); i++){
            sum += price.at(i)*quantity.at(i);
        }
        return sum;
    }

private:
    vector<string> product;
    vector<int> quantity;
    vector<double> price;
};
```


```cpp
class Rubrica{
private:
  struct cont{
    string nome;
    string numero;
  };
  vector<cont> contatti;
  void add(string str);
  string get_numero(const string& str, int i, int j);
  string get_nome(const string& str, int i, int j);
  void ordina();
public:
  Rubrica(const string& str) {
    contatti.resize(0);
    add(str);
  }

  void stampa_contatti_ordinati() {
      ordina();
      for(auto a:contatti) cout << a.nome << ": " << a.numero << endl;
  }
};

void Rubrica::add(string str){
    int i = 0, j = 0;
    bool nom = true, upper = true;
    string nome, numero;
    while(i < str.length()){
        if(str.compare(i, 1, ",") == 0){ 
            if(nom) nom = false;
            else {
                nom = true;
                contatti.push_back({nome, numero});
                i++;
            }
            i++;
        }
        else{
            j = str.find(",", i+1);
            if(nom)
                nome = get_nome(str, i, j);
            else
                numero = get_numero(str, i, j);
            i = j;
        }
    }
}

string Rubrica::get_nome(const string& str, int i, int j){
    bool upper = true;
    if(str.compare(j-1, 1, " ") == 0) j--;
    string nome = "";
    while(i < j){
        if(str.compare(i, 1, " ") == 0) {
            if(str.compare(i+1, 1, " ") != 0){
                nome += str.at(i);
            }
            upper = true;
        }
        else if(upper){
            nome += (str.at(i) | ' ') - ' ';
            upper = false;  
        } 
        else nome += str.at(i) | ' ';
        i++;
    }
    return nome;
}

string Rubrica::get_numero(const string& str, int i, int j){
    string num_app = "";
    string numero = "";
    for(int k = i; k < j; k++)
        if(str.compare(k, 1, " ") != 0) num_app += str.at(k);
    int length = num_app.length();
    if(length >= 10){
        int k = 0;
        numero += "+";
        while(length > 10){
            numero += num_app.at(k);
            k++;
            length--;
        }
        length = num_app.length();
        while(k < length){
            if(k == length-10 || k == length-7 || k == length-4) numero += " "; //si poteva usare .instert
            numero += num_app.at(k);
            k++;
        }
    }
    else numero = "numero non valido";
    return numero;
}

void Rubrica::ordina(){
    if(contatti.size() != 0){
        for(int j = 0; j < contatti.size()-1; j++){
            for(int i = 0; i < contatti.size()-j-1; i++){
                if(contatti.at(i).nome > contatti.at(i+1).nome)
                    swap(contatti.at(i), contatti.at(i+1));
            }
        }    
    }
    else return;
}
```

```cpp
for(int i = 0; i < l.length(); i++){
	sum += l.at(i); //l[i]
}

for(auto a:l){
	sum += a;
}

for(auto a:l){
	a = a*2;


for(auto a:l){
	sum = a + (a+1);
}
```