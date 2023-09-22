
```cpp

#include <iostram>
#include <string>

int S(){
	char c=0;
	std::cin >> c;
	std::cin.putback(c);

	if(c == '('){
		int h1 = T();
		int h2 = s();
		return std::max<int>(h1,h2;)
	}
	return 0;
}

int T(){
	char c=0;
	std::cin >> c;
	int h = S();
	std::cin >> c;
	return h+1
}

int main(){
	
}
```