
```cpp
#include<iostream>
#include<vector>
#include<list>
class Polynomial{
  public:
    Polynomial();
    Polynomial(const Polynomial& p);
    void set(int exponent, int coeff);
    int at(int exponent) const;
    void read();
    int evaluate(int x) const;
    Polynomial differentiate(int order) const;
    int degree() const;
    void print() const;
    
  private:
    int intpow(int base, int exponent) const;
    struct monom{
        int a;
        int exp;
        monom* next;
    };
    typedef struct monom* mono;
    mono head;
};


//////// Pre-implemented part/////////////

//Do not change this method! It reads a Polynomial 
void Polynomial::read() {
  int coeff, exponent;
  do {
    std::cin>>exponent;
    if (exponent>=0)  {
      std::cin>>coeff;
      set(exponent, coeff);
    }
  } while (exponent>=0);
}


//Do not change this method! It prints a Polynomial
void Polynomial::print() const {
  int n = degree();

  for (int i=0; i<=n; i++) {
    if (at(i)!=0) 
      std::cout<<"+("<<at(i)<<")x^"<<i;
  }
  std::cout<<std::endl;
}



//Do not change this method! It simply computes the integer power
//It could be useful!
int Polynomial::intpow(int base, int exponent) const {
  int res=1;

  while (exponent>0) {
    res = res*base;
    exponent--;
  }
  return res;
}


//Methods for exercise 1

//Default constructor: builds the polynomial 0
Polynomial::Polynomial() {
    head = nullptr;
}

//Copy constructor
Polynomial::Polynomial(const Polynomial& p) {
    if(!p.head){
        head = nullptr;
        return;
    }
    mono h_p = p.head;
    head = new monom{h_p->a, h_p->exp, nullptr};
    h_p = h_p->next;
    mono h = head;
    while(h_p != nullptr){
        h->next = new monom{h_p->a, h_p->exp, nullptr};
        h_p = h_p->next;
        h = h->next;
    }
}

//Returns the coefficient of the terms  x^exponent
//If it has not been added it returns 0
//Notice that we have only one version of at
//It does not return a reference, just an int. So we can only read with at!
int Polynomial::at(int exponent) const {
    mono h = head;
    while(h && h->exp != exponent)
        h = h->next;
        
    if(h == nullptr) return 0;
    else return h->a;
}



//Set to coeff the coefficient of x^exponent. If this is present, 
//it will be overwritten. Setting the coefficient to 0 means 
//the removal from the polynomial representation
void Polynomial::set(int exponent, int coeff) {
    if(!head and coeff != 0)
        head = new monom{coeff, exponent, nullptr};
    else if(!head) return;
    else if(coeff != 0){
        mono h = head;
        while(h){
            if(h->exp == exponent){
                h->a = coeff;
                return;
            }
            if(h->next == nullptr){
                h->next = new monom{coeff, exponent, nullptr};
                return;
            }
            h = h->next;
        }
    }else{
        mono h = head;
        if(head->exp == exponent){
            head = head->next;
            delete h;
            return;
        }
        if(!head->next) return;
        while(h->next->next){
            if(h->next->exp == exponent){
                mono tmp = h->next;
                h->next = h->next->next;
                delete tmp;
                return;
            }
            h = h->next;
        }
        if(h->next->exp == exponent){
            delete h->next;
            h->next = nullptr;
        }
    }
}

//Evaluate a polynomial for a certain x
int Polynomial::evaluate(int x) const{
    int val = 0;
    mono h = head;
    while(h){
        val += h->a * intpow(x, h->exp);
        h = h->next;
    }      
    return val;
}

//Methods for exercise 2


//Returns the degree of a polynomial. The polynomial 0 has degree 0
int Polynomial::degree() const{
    if(!head) return 0;
    mono h = head;
    int deg = 0;
    while(h){
        if(h->exp > deg) deg = h->exp;
        h = h->next;
    }
    return deg;
}

//Methods for exercise 3

//This *recursive* function computes the n-th derivative of the polynomial
Polynomial Polynomial::differentiate(int order) const {
    if(order == 0) return *this;
    mono h = head;
    while(h){
        h->a *= h->exp;
        h->exp--;
        h = h->next;
    }
    differentiate(order-1);
    return *this;
}
```