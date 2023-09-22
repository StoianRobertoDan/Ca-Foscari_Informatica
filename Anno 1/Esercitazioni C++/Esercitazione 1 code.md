1. Vettore di primi
		Scrivere una funzione che riempie un vettore lungo n con altrettanti numeri primi (non ripetuti e consecutivi)
```cpp
bool is_prime(int n){
    if(n == 2) return true;
    if(n == 0 || n == 1) return false;
    for(int i = 2; i <= n/2; i++) if(n%i == 0) return false;
    return true;
}


std::vector<int> fill_with_primes(int size) {
    std::vector<int> primes;
    int j=2;
    bool full = false;
    while(full == false){
        if(primes.size() == size) full = true;
        else{
            if(is_prime(j)) primes.push_back(j);
            j++;
        }
    }
    return primes;
}
```
es 1 fatto ancora meglio:


```cpp
std::vector<int> fill_with_primes(int size){
    std::vector<int> v_primes;
    if(size > 0){
        int prime = 3;
        v_primes.push_back(2);
        for(int i = 0; i < size-1; i++){
            int k = 1;
            while(k < v_primes.size())
                if(prime%v_primes.at(k) == 0){
                    prime = prime + 2;
                    k = 1;
                }
                else k++;
            v_primes.push_back(prime);
            prime = prime + 2;
        }
    }
    return v_primes;
}
```

2. Media mobile
		Dato in input un vettore (passato per copia come const) e un valore k, scrivere una funzione lunga come il vettore di input dove in ogni casella è calcolata la media del range dal k valore a sinistra al k valore a destra. non si considerino valori esterni al vettore.
		(dato un vettore {0, 1, 2} e k=1, il vettore risultante sarà {0.5, 1, 1.5})

```cpp
std::vector<double> moving_average(const std::vector<double> v, int k) {
    std::vector<double> mo_avg;
    double sum, div;
    int min = 0, max = 0;
    
    for(int i = 0; i < v.size(); i++){
        sum = 0;
        div = 0;
        if(i - k <0) min = 0;
        else min = i - k;
        
        if(i + k >= v.size()) max = v.size();
        else max = i + k +1;
        
        do{
            sum = sum + v.at(min);
            div++;
            min++;
        }while(min < max);
        mo_avg.push_back(sum/div);
    }
    return mo_avg;
}
```

```cpp

for(int i = 0; i < v.size(); i++){
	for(int j = i-k; i < j+k; j++){
		if(j>=0 && j<v.size()){
			sum = sum + v[j];
			count++;
		}
	}
	v.at(i) = sum/count;
}
return v;
```

3. Anagrammi
		Date due stringhe (passati per copia) scrivere una funzione che controlla se sono anagrammi. Bisogna ignorare gli spazi e nelle stringhe contengono solo caratteri alfabetici minuscoli.

```cpp
bool is_empty(string& s){
    
    for(int i = 0; i < s.size(); i++){
        if(s[i] != ' ') return false;
    }
    return true;
}

bool anagramma(string s1, string s2)
{
    int count = 0, j, i = 0;
    bool found;
    
    for(int i = 0; i < s1.size(); i++){
        if(s1[i] == ' ') count++;
        else{
            found = false;
            j = 0;
            while(found == false && j < s2.size()){
                if(s2[j] == s1[i]){
                    count++;
                    s2[j] = ' ';
                    found = true;
                }
                else j++;
            }
        }
    }
    if(count == s1.size() && is_empty(s2)) return true;
    else return false;
}
```