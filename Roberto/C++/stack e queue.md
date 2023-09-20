```cpp
#include<stack>
#include<

//policy LIFO (last in, first out)
void test_stack(){
	std::stack<int> s;
	//1, 2, 3, 4 ---> s.push(4) ---> 1, 2, 3, 4
	s.push(1);
	s.push(2);
	s.push(3);
	//1, 2, 3, 4 ---> s.pop() ---> 1, 2, 3
	std::cout<< s.top() << std::endl;
	s.pop();
	std::cout<< s.top() << std::endl;
}

//policy FIFO(First in First out)
void test_queue(){
	std::queue<int> q;
	//1, 2, 3, 4 ---> s.push(4) ---> 1, 2, 3, 4
	q.push(1);
	q.push(2);
	q.push(3);
	//1, 2, 3, 4 ---> s.pop() ---> 1, 2, 3
	std::cout<< q.front() << std::endl;
	q.pop();
	std::cout<< q.front() << std::endl;
}

//funtore (functor) == oggetto che definisce operator(x, y)
//Si può usare come funzione (my_comp f; f(x, y) --> es. x < y)
struct my_comp{
	bool operator()(int x, int y){
		//diamo priorità ai pari
		if(x%2==0){
			if(y%2==0) return true;
		}
		else{
			if(y%2!=0) return false;
		}
		else return x>y;
	}
};

//policy custom (decisa da noi)
void test_priority_queue(){
	//priprota <
	//std::priority_queue<int> pq;
	//priorità pari
	std::priority_queue<int, std::vector<int>, my_comp> pq;
	pq.push(2);
	pq.push(9);
	pq.push(1);
	pq.push(13);
	pq.push(132);
	pq.push(5);
	while(!pq.empty()){
		std::cout<< pq.top() << std::endl;
		pq.pop();
	}
}
/*
struct funct_0001{
	funct_0001(int& v) : w(v) {}
	bool operator()(int x, int y){
		return x*w>y;
	}
	int& w;
}*/

struct date{
	int dd;
	int mm;
	int yyyy;
}

void test_lambda(){
	stdd::vector<date> v;
	v.push_back({2, 3, 2020});
	v.push_back({2, 3, 2020});
	v.push_back({2, 3, 2020});
	v.push_back({2, 3, 2020});

	std::sort(v.begin(), v.end(),
		[](date& d1, date& d2){
			return d1.yyyy < d2.yyyy;
		}
	);
	for(auto x:v){
		std::cout << x.dd << " " << x.mm << " " << x.yyyy << " " << std::endl;
	}
}

int main(){
	std::vector<int> v = {5, 6, 1, 25, 45}

	//sort con funtore
	std::sort(v.begin, v.end(), my_comp{};

	int w = 5;
	//sort con lambda function
	std::sort(v.begin(), v.end(),
		[w] (int x, int y) -> bool {return x>y;}); //la specifica del tipo restituito (bool) è opzionale (il compilatote la può dedurre automaticamente)
	//w catturato per reference
	auto f = [&w] (int x, int y) -> bool {return x+w>y;};
	// = --> cattura per valore di tutte le cariavili di ambiente
	auto g = [=] (int x, int y) -> bool {return x+w>y;};
	// & --> cattura per reference di tutte le cariavili di ambiente
	auto r = [&] (int x, int y) -> bool {return x+w>y;};
	// tutte le variabili catturate per valore, eccetto w(per reference)
	auto z = [=, &w] (int x, int y) -> bool {return x+w>y;};
	// tutte le variabili catturate per reference, eccetto w(per valore)
	auto z = [&, w] (int x, int y) -> bool {return x+w>y;};

```