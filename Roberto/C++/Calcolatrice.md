```cpp 
#include <iostream>

int main(){

	int lval = 0; 
	char op = 0; 
	int rval = 0;
	 

	std::cin>>lval; // std::cin>>lval>>rval>>op
	std::cin>>op; //gli operatori << o >> sono operatori binari e lavorano in base al        
	//tipo che viene chiesto loro 
	std::cin>>rval;
	// ((std::cin>>lval)>>op)>>rval equivalenza 
	int res=0;

	if (op=='+'){
		res=lval+rval; 
	}
	else if(op=='-'){
		res=lval-rval;
	}
	else{
	std::cerr<<"ERRORE"<<op<<std::endl; 
	return 1; 
	}
	std::cout<<"il risultato è"<<res<<std::endl; 
	return 0; 
	

}
```


```cpp 

struct parse_error
	std::string err;
}

int evaluate(){
	std::cout<< "insert expression here (valid operations: +, -, /, *)"<< std::endl;
	std::cout<< "the expression must end with a ="<< std::endl;
	
	double lval=0, rval=0;
	char op=0;
	std::cin>> lval >> op;
	if(!std::cin) throw parse_error("invalid first operand or operator");
	while(op != '='){
		std::cin>> rval;
		if(!std::cin) throw parse_error("invalid operand");
		
		switch(op){
			case '+': lval += rval; break;
			case '-': lval -= rval; break;
			case '*': lval *= rval; break;
			case '/': lval /= rval; break;
			default: throw parse_error("invalid operator"); break;
		}
		std::cin>> op;
	}
	std::cout << "the result is: " << lval;
	return 0;
}

int main(){

	try{
		return evaluate();
	}catch(parse_error const& e){
		std::cerr << e.err << std::endl
		return 1;
	}

}
```

Nuovo file per struttura token
```cpp
#include <iostream>
#include <limits>

struct token{
	static constexpr double inf = std::numeric_limits<double>::max;

	token() : m_value(inf), m_type(0) {}

	/* meglio non usare questo:
	token(){
		m_value = inf;
		m_type = 0;
	} perchè questo fa 2 assegnamenti in più, non cambia ora ma con oggetti grossi si
	*/

	friend std::ostream& operator<<(std::ostream& os, token const& t);

	double get_value() const {return m_value;}
	char get_type() const {return m_type;}
	bool is_double() const {	return m_type == 0 and m_value != inf;}
	bool is_open() const {	return m_type == '(';}
	bool is_closed() const {	return m_type == '';}
	bool is_add() const {	return m_type == '+';}
	bool is_sub() const {	return m_type == '-';}
	bool is_mul() const {	return m_type == '*';}
	bool is_div() const {	return m_type == '/';}
	bool is_eq() const {	return m_type == '=';}
private:
	double m_value;
	char m_type;

};

std::ostream& operator<<(std::ostram& os, token const& t){
	os << "value: " << t.m_value << "; type: " << m-type;
	return os;
}


```