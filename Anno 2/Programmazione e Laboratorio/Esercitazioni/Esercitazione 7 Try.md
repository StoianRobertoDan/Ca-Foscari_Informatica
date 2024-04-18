
```cpp
//deep copy the list from source to dest and return the pointer to the last element of the list
//pointed by dest, nullptr for the empty list
Pcell List_dl::Impl::copy(Pcell& dest, Pcell source) const{
    /*std::cout<<"Copy, should delete: ";
    while(dest){
        Pcell tmp = dest;
        dest = dest->next;
        //delete dest;
        std::cout << tmp->info << " ";
    }
    std::cout<<"postDestroy "<<std::endl;*/
    Pcell heads = source;
    Pcell head1 = dest, head2 = dest;

    while(heads){
        if(!dest){
            dest = new Cell{heads->info, nullptr, nullptr};
            head1 = dest;  
            head2 = dest; 
            //std::cout<<"addedFirst ";       
        }
        else{
            head2 = new Cell{heads->info, nullptr, head1};
            head1->next = head2;
            head1 = head1->next;
            //std::cout<<"addedMore ";
        }
        head2 = head2->next; 
        heads = heads->next;
    }
  return head1; 
}


/*Assignment with deep copy*/
List_dl& List_dl::operator=(const List_dl& l) {
    if (this != &l) { //protect from self-assignment 
        //std::cout<<"PreCopy ";
        pimpl->tail = pimpl->copy(pimpl->head, l.pimpl->head);
        //std::cout<<"PostCopy " << std::endl;
    }
    return *this;
}

/*This operator concatenates the two list (*this first and l follows)*/
List_dl List_dl::operator+(const List_dl& l) const {
    //std::cout<<"+opp ";
    List_dl result = *this;
    Pcell head = l.pimpl->head;
    while(head){
        //std::cout<<"whileApp ";
        result.append(head->info);
        head = head->next;
    }
    return result;
}
```