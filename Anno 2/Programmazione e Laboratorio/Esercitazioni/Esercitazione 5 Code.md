
```cpp
void merge_ric(List const l1, List const l2, List& l){
    if(l1 == nullptr && l2 == nullptr)
        return;
    else{
        if(l2 == nullptr){
            append(l, l1->info);
            merge_ric(l1->next, l2, l);
        }
        else if(l1 == nullptr){
            append(l, l2->info);
            merge_ric(l1, l2->next, l);
        }
        else if(l2->info >= l1->info){
            append(l, l1->info);
            merge_ric(l1->next, l2, l);
        }
        else if(l1->info > l2->info){
            append(l, l2->info);
            merge_ric(l1, l2->next, l);
        }
        return;
    }
}

List merge(List l1, List l2) {
    if(l1 == nullptr && l2 == nullptr)
        return nullptr;
    else{
        List l{nullptr};
        merge_ric(l1, l2, l);
        return l;
    }
}
```
Metodo migliore:
```cpp
List merge(List l1, List l2) {
    if(l1 == nullptr && l2 == nullptr)
        return nullptr;
    List l = new List;
    if(l1 && l2){
	    if(l1->info < l2->info){
		    l->info = l1->info;
		    l->next = merge(l1->next, l2);
	    }else{
		    l->info = l1->info;
		    l->next = merge(l1->next, l2);
	    }
    }
    else if(!l1){
		l->info = l2->info;
		l->next = merge(l1, l2->next);
	}
	else{
		l->info = l1->info;
		l->next = merge(l1->next, l2);
	}
	return l;
}
```

```cpp
void concat_ric(Lista l, int pos, int len, string& s){
    if(len == 0 || l == nullptr) return;
    if(pos != 0)
        concat_ric(l->next, --pos, len, s);
    else{
        s += l->info;
        concat_ric(l->next, pos, --len, s);
    }
}

/*void print_all(Lista l){
    if(l==nullptr) return;
    std::cout << l->info << " ";
    print_all(l->next); 
}
no need*/

string concat(Lista l, int pos, int len) {
    std::string s = "";
    concat_ric(l, pos, len, s);
    return s;
}
```
Metodo migliore:
```cpp
string concat(Lista l, int pos, int len) {
    if(len == 0 || !l) return "";
    else{
	    if(pos>0) return concat(l->next, pos-1,len);
	    else return l->info + concat(l_next, pos, len-1);
    }
}
```

```cpp
int conta_mattoncini(int n)
{
    if(n == 1) return 1;
    if(n%2 == 0) return n + conta_mattoncini(n/2);
    else return n + conta_mattoncini(n-1);
}
```