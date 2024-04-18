```cpp
string carta(int n) {
    string carta;
    if(n >= 0 && n < 10){
        carta = "denari";
    }else if (n >= 10 && n < 20){
        carta = "coppe";
    }else if (n >= 20 && n < 30){
        carta = "bastoni";
    }else if (n >= 30 && n < 40){
        carta = "spade";
    }else return carta = "Errore di conversione\0";
    
    carta = " di " + carta;
    
    if(n == 0 or n == 10 or n == 20 or n == 30){
        carta = "Asso" + carta;
    }else if(n == 7 or n == 17 or n == 27 or n == 37){
        carta = "Donna" + carta;
    }else if(n == 8 or n == 18 or n == 28 or n == 38){
        carta = "Fante" + carta;
    }else if(n == 9 or n == 19 or n == 29 or n == 39){
        carta = "Re" + carta;
    }else carta = (char)(n%10 + 49) + carta;
    return carta;
}
```


```c++
void ordinamento_parziale(vector<int>& vect, const vector<int>& pos)
{
    for(int j = 0; j < pos.size()-1; j++){
        for(int i = 0; i < pos.size()-j-1; i++){
            if(vect.at(pos.at(i)) > vect.at(pos.at(i+1))){
                int temp = vect.at(pos.at(i));
                vect.at(pos.at(i)) = vect.at(pos.at(i+1));
                vect.at(pos.at(i+1)) = temp;
            }
        }
    }
}
```

```cpp
void ordinamento_parziale(vector<int>& vect, const vector<int>& pos)
{
    if(vect.size() != 0 && pos.size() != 0){
        for(int j = 0; j < pos.size()-1; j++){
            for(int i = 0; i < pos.size()-j-1; i++){
                if(vect.at(pos.at(i)) > vect.at(pos.at(i+1))){
                    int temp = vect.at(pos.at(i));
                    vect.at(pos.at(i)) = vect.at(pos.at(i+1));
                    vect.at(pos.at(i+1)) = temp;
                }
            }
        }    
    }
    else return;
}
```

```cpp
bool rotazione(const string& S, const string& T)
{
    if(S.size() != 0 and S.size() == T.size()){
        string S_double = S + S;
        if(S_double.find(T) != std::string::npos) return true;
        else return false;    
    }
    else return false;
}
```

```cpp
bool rotazione(const string& S, const string& T)
{
    if(S.size() != 0 and S.size() == T.size()){
        string S_double = S + S;
        if(S_double.find(T) != std::string::npos) return true;
        else return false;    
    }
    else return false;
}
```









```cpp
bool rotazione(const string& S, const string& T)
{
    if(S.size() == T.size() and S.size() != 0){
        int s_size = 0, t_size = 0;
        for(int i = 0; i < S.size(); i++){
            s_size += (int)S.at(i);
            t_size += (int)T.at(i);
        }
        if(s_size != t_size) return false;
        else return true;
    }
    else return false;
}
```