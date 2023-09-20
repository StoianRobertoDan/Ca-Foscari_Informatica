
Algoritmo di ordinamento "sul posto"

Il mio tentativo (da migliorare)
```cpp
for(int i = 0; i < v.size(); i++){
	
	for(int j = i+1; j < v.size(); j++){
		el = v.at(j);
		if(v.at(i) < v.at(j) && v.at(j) < el){
			el=v.at(j);
			pos_el = j;
	}
	
	sup = v.at(pos_el);
	v.at(pos_el) = v.at(i);
	v.at(i) = sup;
}
```


Del prof:
```cpp
for(int i = 0; i < v.size(); i++){
	
	for(int j = v.size()-1; j > i; j--){
		if(v.at(j) < v.at(j-1) {
			sup = v.at(pos_el);
			v.at(pos_el) = v.at(i);
			v.at(i) = sup;
		}
	}
}
```