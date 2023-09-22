1. Polinomio
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
    struct monom{
        int coef;
        int esp;
    };
    mutable std::vector<monom> polinom;
    
    int intpow(int base, int exponent) const;
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
}

//Copy constructor
Polynomial::Polynomial(const Polynomial& p) {
    polinom = p.polinom;
}

//Returns the coefficient of the terms  x^exponent
//If it has not been added it returns 0
//Notice that we have only one version of at
//It does not return a reference, just an int. So we can only read with at!
int Polynomial::at(int exponent) const {
    for(int i = 0; i < polinom.size(); i++) if(polinom[i].esp == exponent) return polinom[i].coef;
    return 0;
}

//Set to coeff the coefficient of x^exponent. If this is present, 
//it will be overwritten. Setting the coefficient to 0 means 
//the removal from the polynomial representation
void Polynomial::set(int exponent, int coeff) {
    for(int i = 0; i < polinom.size(); i++){
        if(polinom[i].esp == exponent){
            if(coeff != 0){
                polinom[i].coef = coeff;
                return;
            }
            else{
                polinom.erase(polinom.begin()+i);
                return;
            }
        }
    }
    if(coeff != 0) polinom.push_back({coeff, exponent});
}


//Evaluate a polynomial for a certain x
int Polynomial::evaluate(int x) const{
    int somma = 0;
    for(int i = 0; i < polinom.size(); i++) somma += polinom[i].coef * intpow(x, polinom[i].esp);
    return somma;
}

//Methods for exercise 2


//Returns the degree of a polynomial. The polynomial 0 has degree 0
int Polynomial::degree() const{
    int degree = 0;
    for(int i = 0; i < polinom.size(); i++) if(polinom[i].esp > degree) degree = polinom[i].esp;
    return degree;
}

//Methods for exercise 3

//This *recursive* function computes the n-th derivative of the polynomial
Polynomial Polynomial::differentiate(int order) const {
    if(order == 0) return *this;
    for(int i = 0; i < polinom.size(); i++){
    polinom[i].coef *= polinom[i].esp;
    polinom[i].esp--;
    }
    return differentiate(--order);
}
```
