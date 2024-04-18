1. Scrivere una funzione che dato un vettore ritorna la somma dei 2 valori più alti.
```cpp
int trova_somma_massima(const std::vector<int> & v) {
    int max1 = v[0], max2 = v[1];
    for(int i = 2; i < v.size(); i++){
        if(v.at(i) > max1 || v.at(i) > max2){
            if(max1 >= max2) max2 = v.at(i);
            else max1 = v.at(i);
        }
    }
  return max1+max2;
}
```

2. Scrivere una funzione che dato un vettore ritorna il valore ripetuto più volte. Se 2 valori sono ripetuti lo stesso numero di volte ritornare il minore.
```cpp
int search(const std::vector<int>& val, int pr){
    for(int i = 0;i < val.size(); i++){
        if(pr == val.at(i)){
            return i;
        }
    }
    return -1;
}

int max(const std::vector<int>& quan, const std::vector<int>& val){
    int max = 0, maxPos = 0;
    for(int i = 0; i < quan.size(); i++){
        if(quan.at(i) > max) {
            max = quan.at(i);
            maxPos = i;
        }
        else if(quan.at(i) == max){
            if((quan.at(i) < val.at(maxPos))){
                max = quan.at(i);
                maxPos = i;
            }
        }
    }
    return maxPos;
}

int trova_max_freq(const std::vector<int>& v) {
    std::vector<int> val;
    std::vector<int> quan;
    if(v.size() > 0){
        for(int i = 0; i < v.size(); i++){
            int tr = search(val, v.at(i));
            if(tr == -1){
                val.push_back(v.at(i));
                quan.push_back(1);
            }
            else{
                quan.at(tr)++;
            }
        }
        return val.at(max(quan, val));
    }
    return 0;
}
```

3. Scrivere una funzione che dato un intero ritorna un vettore di quella dimensione riempito da numeri primi.
```cpp
std::vector<int> fill_with_primes(int size) {
    std::vector<int> vec;
    if(size > 0){
        vec.push_back(2);
        int i = 1;
        int prime = 3;
        while(i < size){
            int j = 0;
            while(j<vec.size()){
                if(prime % vec.at(j) == 0){
                    prime = prime + 2;
                    j = 1;
                }
                else j++;
            }
            vec.push_back(prime);
            prime = prime +2;
            i++;
        }
    }
    return vec;
}
```
