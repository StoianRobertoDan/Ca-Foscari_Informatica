Context free grammar

P -> Rules 

Example for tree parser:
- T -> (S)
- S -> $\epsilon$ | TS
Epsilon symbolizes empty

T writes parenthesis with S inside, S either ends there or add another T (and another S).

Parser (recursive) to count the height of the tree.
``The program will be called with "echo (()()) | ./program"
```cpp
#include<iostream>

struct parser_error{
	std::string msg;
	bool fatal = true;
};

int S();

int T(){ //T -> (S)
	char c = 0;
	std::cin>>c; //consume open parenthesis (
	//cin is formatted (skips spaces, endlines and tabs)
	//if(c != '(') throw parser_error{"Unexpected character. Expected '('.", false}; valid
	if(c != '(') throw parser_error{std::string{"Unexpected character. Expected '(', found: "} + c, false};
	int h = S();
	std::cin>>c; //consume closed parenthesis )
	return 1 + h;
	
}

int S(){ //S -> epsilon | TS
	//Peek is not formatted and will return a space if there is one
	char c = 0;
	std::cin>>c;
	std::cin.putback(c);

	if(c == ')') return 0; //
	if(c == '(') {
		int h1 = T();
		int h2 = S();
		return std::max(h1, h2);	
	}
	throw parser_error{std::string{"Exiting due to unexpected character. Expected '(' or ')', found: "} + c};
}

int main(){
	std::cout << "Insert tree: " << std::endl;
	//int h = T(); //is it possible to excecute the program by <echo "tree ex (()()(()))" | ./parser>
	int h;
	while(true){
		try{
			h = T();
			break; //If the parser doesn't throws an exception to catch than exits the loop
		}catch(parser_error e){
			std::cout << "Error: " << e.msg << std::endl;	
			//return 0; // or exit(0); in main exit and return works the same, but exit can interupt the whole program independently from where is called, return just ends the current funtion.
			if(e.fatal) exit(0);
			else std::cout<<"Skipping character."<< std::endl;
		}
	}
	std::cout << "Height: " << h << std::endl;
}
```


```cpp
using std;
double F();
double E();
double P();
double T();

double F(){ //F -> E=
	double result = E();
	char c = 0;
	cin>>c; //consumes =
	return result;
}

double T(){ //T -> -T | unsigned_double | (E)
	char c = 0;
	cin>>c;
	cin.putback(c);
	if(c == '-'){
		cin>>c; //consumes -
		return -T();
	}
	if(c == '('){
		cin>>c; //consumes (
		double res = E();
		cin>>c; //consumes )
		return res;
	}
	else{
		double res = 0.f;
		cin >> res; //consumes a number
		return res;
	}
}
```