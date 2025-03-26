	
```cpp
void rimuovidoppie(string &s)
{
    if(s.size()<=0) return;
    int i = 0;
    while(i<s.length()-1){
        if(s.at(i) == s.at(i+1)){
            s.erase(s.begin()+i);
        }
        i++;
    }
}
```


```cpp
int minimumDivisor(vector<int> arr, int threshold) {
    double min = 1, max = threshold;
    int divisor;
    long trash = 0, i = 0;
    while(min != max){
        divisor = (min + max)/2;
        i = 0;
        trash = 0;
        while(trash < threshold && i < arr.size())
            trash += ceil((double)arr.at(i++)/divisor);
        if(trash <= threshold) max = divisor;
        else min = divisor+1;
    }
    return max;
}
```

```cpp
std::vector<double> moving_average(const std::vector<double> v, int k) {
    std::vector<double> ris;
    ris.resize(v.size());
    int ini = 0, fin = 0;
    double num = 0;
    for(int i = 0; i < v.size(); i++){
        num = 0;
        if(i-k <= 0) ini = 0;
        else ini = i-k;
        if(i+k >= v.size()) fin = v.size();
        else fin = i+k+1; 
        for(int j = ini; j < fin; j++){
            num = num + v.at(j);
        }
        ris.at(i) = num/(fin-ini);
    }
    return ris;
}
```