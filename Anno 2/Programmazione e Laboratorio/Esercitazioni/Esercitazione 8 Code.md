```cpp
void linearize(List& l) {
    if(l == nullptr) return;
    List head = l, moving = l->next;
    while(moving->next != head) moving = moving->next;
    moving->next = nullptr;
}
```


```cpp
void rimuovi_occ(Lista_circ& l, int elem) {
    if(l == nullptr) return; // if(!l) return;
    Lista_circ head = l, move = l->next; //non serviva usare head, avevo gia l che stava fermo
    while(move != head){
        if(move->next->info == elem ){
            if(move->next == head){
                l = l->next;
                head = l;
            } 
            Lista_circ tmp = move->next;
            move->next = move->next->next;
            delete tmp;
        }
        else move = move->next;
    }
    if(head->next == head && head->info == elem){
        l = nullptr;
        delete head;
    }
}
 ```
```cpp //metodo del prof
void rimuovi_ooc(List_circ& l, int elem){
	if(!l) return;
	List_circ current = l;
	while(current->next != l){
		if(current->next->info == elem){
			//delete current->next
		}
		else current = current->next;
	}
	if(l->info == elem){
		if(l->next == l){
			delete l;
			l = nullptr;
		}
		else{
			current->next = l->next;
			delete l;
			l = current->next;
		}
	}
}

```

```cpp
void circ_list::split_list(circ_list& fh, circ_list& sh) const {
    if(this->tail == nullptr) return;
    pcella slow = tail->next, fast = tail->next;
    pcella mid = nullptr;
    bool midi = false;
    int sum1 = 0, sum2 = 0;
    sum1 += slow->info;
    if(tail != tail->next)
        fh.append(slow->info);
    else
        sh.append(slow->info);
    slow = slow->next;
    fast = fast->next->next;
    
    while(fast != tail->next and fast != tail->next->next){
        if(fast != tail){
            sum1 += slow->info;
            fh.append(slow->info);
        }
        else midi = true;
        mid = slow;
        slow = slow->next;
        fast = fast->next->next;
    }
    while(fast != slow){
        sum2 += slow->info;
        sh.append(slow->info);
        slow = slow->next;
        fast = fast->next->next;
    }
    
    if(midi){
        if(sum1 >= sum2) sh.tail->next = new Cella{mid->info, sh.tail->next};
        else{
            fh.tail->next = new Cella{mid->info, fh.tail->next};
            fh.tail = fh.tail->next;
        }
    }
}
```

```cpp
void circ_list::split_list(circ_list& fh, circ_list& sh) const {
	if(!tail) returm;
	
}
```
