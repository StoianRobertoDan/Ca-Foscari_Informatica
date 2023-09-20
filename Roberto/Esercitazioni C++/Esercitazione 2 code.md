1. Radice k-esima ricorsiva
		Scrivere una funzione ricorsiva calcola con una precisione di 5 cifre decimali la radice k-esima di un numero tramite la riduzione dell'intervallo di ricerca
```cpp
double radice(double n, unsigned int k, double min, double max) {
    float p_med =1, p_med_pow = 1;
    if(max - min > 0.00001){
        p_med = (max+min)/2;
        for(int i = 0; i < k; i++) p_med_pow = p_med_pow * p_med;
        if(p_med_pow >= n) max = p_med;
        else min = p_med;
        return radice(n, k, min, max);
    }
    else return min;
}
```

2. Carta di un mazzo come stringa
		Dato un mazzo di 40 carte (10 per seme e con asso (1), donna (8), fante (9) e re(10)) scrivere in stringa la carta specificando seme e numero. Se la variabile in input non è nel range delle carte (0-->39) dare un messaggio di errore
```cpp
string GetNumero(int n){
    n = n%10;
    if(n == 0) return "Asso di ";
    else if(n == 7) return "Donna di ";
    else if(n == 8) return "Fante di ";
    else if(n == 9) return "Re di ";
    else return std::to_string(n+1) + " di ";
}

string GetSeme(int n){
    if(n < 10) return "denari";
    else if(n < 20) return "coppe";
    else if(n < 30) return "bastoni";
    else return "spade";
}


string carta(int n) {
    if(n > 39 or n < 0) return "Errore di conversione";
    else{
        return GetNumero(n) + GetSeme(n);
    }
    
}
```

3. Miglior guadagno ricorsiva
		Dato un grattacielo in cui si possono dipingere di nero i piani (ma non in modo consecutivo) bisogna capire qual è il massimo guadagno possibile. V è l'array con le offerte di ogni piano per dipingerle di nero, piano è il piano corrente e c è il colore del piano precedente.

```cpp
int grattacielo(const std::vector<int>& v, int piano, colore c) {
    int b = 0, n = 0;
    if(v.empty()) return 0;
    
    if (piano == v.size()-1 && c == Bianco) return v.at(piano);
    else if (piano == v.size()-1 && c == Nero) return 0;
    else if(c == Bianco){
        n = grattacielo(v, piano +1, Nero);
        b = grattacielo(v, piano +1, Bianco);
        if(n >= b) return n + v.at(piano);
        else return b;
    }
    else{
        return grattacielo(v, piano+1, Bianco);
    }
}

```

il mio metodo ma corretto:
```cpp
int grattacielo(const std::vector<int>& v, int piano, colore c) {
	if(piano == v.size()) return 0;
	if(c==Nero) return grattacielo(v, piano+1, Bianco);
	else{
		int bianco = grattacielo(v, piano+1, Bianco);
		int nero = grattacielo(v, piano+1, Nero) + v.at(piano);
		if(bianco > nero) return bianco;
		else return nero;
	}
}
```

metodo alternativo in cui il piano indica il piano successivo:
```cpp
int grattacielo(const std::vector<int>& v, int piano, colore c) {
	if(piano > v.size()) return 0;
	if(c==Nero) return v.at(priano-1) + grattacielo(v, piano+1, Bianco);
	else{
		int bianco = grattacielo(v, piano+1, Bianco);
		int nero = grattacielo(v, piano+1, Nero);
		if(bianco > nero) return bianco;
		else return nero;
	}
}
```

