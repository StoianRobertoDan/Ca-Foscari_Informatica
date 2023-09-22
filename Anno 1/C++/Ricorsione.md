Caso base: il caso finale che farà finire il ciclo di ricorsione e farà il return finale.

funzione ricorsiva esponenziale matematico:
```cpp
int power_recursive(int x, int y){
	assert(y >= 0);
	if (y==0) return 1;
	return x * power_recursive(x, y-1);
}
```

funzione palindroma:
```cpp
bool is_palindrome(std::string cost& s){
	uint64_t n = s.length();
	for(uint64_t i = 0; i < n; i++){
		if(s[i] == s[n-i-1]) return false;
	}
	return true;
}
```
modo ricorsivo:
```cpp
bool is_palindrome_recursive(std::string cost& s, int i, int j){  //si può passare per coppia ma verrà copiata per il numero di caratteri /2 che ha
	if(i >= j) return true;  //caso base (quando si arriva a metà stringa, con 1 o 0 elementi)
	if(s[i] != s[j]) return false;
	return is_palindrome_recursive(s, i+1, j-1);
}
```

Coefficiente binomiale:
```cpp
uint64_t binmomial(int n, int k){
	if(n == k) return 1;
	if(k == 0) return 1;
	return (n * binomial(n-1, k-1))/k
}
```

ricerca binaria:
per ricercare un valore in un vettore ordinato si può dividere a metà il vettore e cercare nella prima metà. In caso il valore non fosse presente si divide il resto di nuovo in metà e si ricerca nella prima metà. 
è il metodo di ricerca molto veloce ed fa log2(n) passi nel peggiore dei casi con n il numero di elementi.

Depth-first search
```cpp
#include<stdio.h>
#include<iostream>
#include<vector>
using namespace std;

void all_words(vector<char>& const alphabet, string& prefix, int k){
	cout << prefix << endl;
	if(prefix.length == k)
		return;
	
	for(auto c:alphabet){
		prefix.push_back(c);
		all_words(alphabet, prefix, k);
		prefix.pop_back(c);
	}
	
}

int main(){
	string prefix {};
	vector<char> alphabet {"a", "b", "c"};
	int k = 3;
	
	all_words(alphabet, prefix, k);
}
```