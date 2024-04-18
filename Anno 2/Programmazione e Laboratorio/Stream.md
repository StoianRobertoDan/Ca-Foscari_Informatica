
```cpp
include<iostream>
include<fstream>
include

void test_getline(){
	std::ifstream ifs{"myfile.txt"}; //mettiamo in ifs un file di testo
	std::string line;
	while(std::getline(ifs, line)){ //se non specifico niente va fino alla fine dei file stampando anche gli "a capo"
		std::cout<<line<<std::endl;
	}
}

void test_getline2(){
	std::string date {"26/03/2024"};
	std::istringstream iss {date};
	
	std::string day;
	std::string month;
	std::sting year;
	
	std::getline(iss, day, "/");
	std::getline(iss, month, "/");
	std::getline(iss, year, "/");
	std::cout << day << " " << month << " " << year << std::endl;
	//stampa "26 03 2024"
	int iday = stoi(day);
	int imonth = stoi(month);
	int iyear = stoi(year);
	std::cout << day << " " << month << " " << year << std::endl;
	//viene stampato "26 3 2024" poichè 
}

void save_vector_to_binary_file(){
	std::vector<int> v {12, 25, 3255, 57, 234};
	
	/*
	std::vector<int> vec (4, 100); //questo crea un vettore di dimensione 4 contenente 100, 100, 100, 100
	std::vector<int> vec {4, 100}; //questo crea un vettore di dimensione 2 contenente 2, 100
	*/
	
	uint64_t size = v.size();
	std::ofstream ofs {"my_integers", std::ios::binary};
	
	//reinterpret_cast<char const*>(&size) converte un puntatore ad un const char
	//es: se size contiene gli 8 byte ch6suc7 reinterpret_cast contiene un puntatore all'array "ch6suc7"
	ofs.write(reinterpret_cast<char const*>(&size), sizeof(size));
	//scriviamo v su file
	ofs.write(reinterpret_cast<char const*>(v.data()), sizeof(int)*size);
}

void red_from_file(){
	std::ifstream ifs {"my_integers", std::ios::binary}; //std::ios::binary molto importante
	
	uint64_t size = 0;
	std::vector<int> v;
	
	//estrai da dile sizeof(size) bytes e inserisce in memoria all'interno di &size
	ifs.read(reinterpret_cast<char*>(&size), sizeof(size));
	v.resize(size);
	ifs.read(reinterpret_cast<char*>(v.data()), sizeof(int)*size);
	for(auto x : v) std::cout << x << std::endl;
}
```


Bisogna usare .close() per chiudere uno stream su un file per poterne aprire un altro sullo stesso file. Viene fatto automaticamente alla fine dello scope in cui è stato chiamato.

```cpp
void f(std::istream& x){
	std::cout << x << \endl;
}

int main(){
	f(std::cin);
	
	std::string s{"stream"};
	std::istringstream iss{s};
	std::ifstream ifs;
	
	f(iss);
	f(ifs);
}
```