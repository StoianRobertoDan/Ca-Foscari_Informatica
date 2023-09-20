
```cpp
#include <iostream>

template<typename T> class stack;
template<typename T> class stack{
    private:
        struct Obj{
            T info;
            Obj* next;
            Obj* prev;
        };
        typedef Obj Obj;
        Obj* head;
        Obj* tail;
    public:
        stack();
        stack(const stack<T>& stack_new);
        ~stack();
        stack<T>& delete_stack();
        stack<T>& operator=(const stack<T>& stack);
        stack<T>& operator-- ();
        T& top() const;
        stack<T>& operator+=(const T& obj);
        stack<T> operator+(const T& obj) const;
};

template<typename T> stack<T>::stack(){
    head = nullptr;
    tail = nullptr;
}

template<typename T> stack<T>::stack(const stack<T>& stack_new){  //da rivedere
    head = nullptr;
    tail = nullptr;
    Obj* h = stack_new.head;
    if(head == nullptr){
        head = new Obj{h->info, nullptr, nullptr};
        tail = head;
    }
    h = h->next;
    while(h != nullptr){
        tail->next = new Obj{h->info, nullptr, tail};
        tail = tail->next;
        h = h->next;
    }
}

template<typename T> stack<T>::~stack(){
    delete_stack();
}

template<typename T> stack<T>& stack<T>::delete_stack(){
    Obj* temp = head;
    while(temp!=nullptr){
        head = head->next;
        delete temp;
        temp = head;
    }
    return *this;
}

template<typename T> stack<T>& stack<T>::operator=(const stack<T>& stack_other){
    if(this != &stack_other){
        delete_stack();
        stack<T>stack_other;
    }
    return *this;
}

template<typename T> stack<T>& stack<T>::operator--(){
    if(tail->prev != nullptr){
        Obj* punt = tail->prev;
        punt->next = nullptr;
        delete tail;
        tail = punt;
    }
    return *this;
}

template<typename T> T& stack<T>::top() const{
    return tail->info;
}

template<typename T> stack<T>& stack<T>::operator+=(const T& obj){
    if(head == nullptr){
        head = new Obj{obj, nullptr, nullptr};
        tail = head;
    }
    else{
        tail->next = new Obj{obj, nullptr, tail};
        tail = tail->next;
    }
    return *this;
}

template<typename T> stack<T> stack<T>::operator+(const T& obj) const{
    stack<T> copy(*this);
    copy += obj;
    return copy;
}
```
