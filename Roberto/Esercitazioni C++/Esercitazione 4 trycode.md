1. polinomio
```cpp
#include<iostream>
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
    struct polinomio{
        int coef;
        int esp;
        polinomio* next;
        polinomio* prv;
    };
    typedef polinomio* poly;
    poly head;
    poly tail;
    int intpow(int base, int exponent) const;
    
    void append(int coef, int esp);
    void canc(poly& punt);
};


//////// Pre-implemented part/////////////

//Do not change this method! It reads a Polynomial 
void Polynomial::read() {
  int coeff, exponent;
  do {
    std::cin>>exponent;
    std::cout<<"Read ";
    if (exponent>=0)  {
        std::cout<<"Read-if ";
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

void Polynomial::append(int coef, int esp){
    std::cout<<"Append ";
    if(tail!=nullptr) tail->next = new polinomio{coef, esp, nullptr, tail};
    else head = new polinomio{coef, esp, nullptr, tail};
    //tail = new polinomio{coef, esp, nullptr, tail};
    std::cout<<"Append-end ";
}

void Polynomial::canc(poly& punt){
    std::cout<<"Canc ";
    if(punt == nullptr) return;
    else if(punt->next == nullptr){
        punt->prv->next = nullptr;
        delete punt;
    }
    else if(punt->prv == nullptr){
        punt->next->prv = nullptr;
        delete punt;
    }
    else{
        punt->prv->next = punt->next;
        delete punt;
    }
}

//Default constructor: builds the polynomial 0
Polynomial::Polynomial() {
    head = nullptr;
    tail = nullptr;
}

//Copy constructor
Polynomial::Polynomial(const Polynomial& p) {
    head = nullptr;
    tail = nullptr;
    poly copy = p.head;
    while(copy!=nullptr){
        append(copy->coef, copy->esp);
        copy = copy->next;
    }
}

//Returns the coefficient of the terms  x^exponent
//If it has not been added it returns 0
//Notice that we have only one version of at
//It does not return a reference, just an int. So we can only read with at!
int Polynomial::at(int exponent) const {
    std::cout<<"At ";
    if(head==nullptr) return 0;
    else{
        poly punt = head;
        while(punt!=nullptr){
            if (punt->esp != exponent) punt = punt->next;
            else return punt->coef;
        }
    }
    return 0;
}

//Set to coeff the coefficient of x^exponent. If this is present, 
//it will be overwritten. Setting the coefficient to 0 means 
//the removal from the polynomial representation
void Polynomial::set(int exponent, int coeff) {
    std::cout<<"Set ";
    if(head==nullptr){
        append(coeff, exponent);
        std::cout<<"Set-if ";
        return;
    } 
    else {
        std::cout<<"Set-else ";
        poly punt = head;
        while(punt!=nullptr){
            if(punt->esp == exponent){
                if(coeff == 0) canc(punt);
                else punt->coef = coeff;
                return;
            }
        }
        append(coeff, exponent);
    }
}


//Evaluate a polynomial for a certain x
int Polynomial::evaluate(int x) const{
    /*if(head==nullptr) return 0;
    else{
        int sum = 0;
        poly punt = head;
        while(punt!=nullptr){
            sum += (punt->coef * intpow(x, punt->esp));
            punt = punt->next;
        }
        return sum;
    }*/
    return 0;
}


//Methods for exercise 2


//Returns the degree of a polynomial. The polynomial 0 has degree 0
int Polynomial::degree() const{
  return 0;
}



//Methods for exercise 3

//This *recursive* function computes the n-th derivative of the polynomial
Polynomial Polynomial::differentiate(int order) const {
  return *this;
}
```
