
Cos'è un JSON? un file ricorsivo. Ha vari tipi

```cpp
#include<json.hpp>  //includo il header con se definizioni delle funzioni

json::json(){ set_null();}

bool json::is_list() const { return m_is_list;}
bool json::is_disctionary() const { return m_is_dict;}
bool json::is_string() const { return m_is_string;}
bool json::is_number() const { return m_is_number;}
bool json::is_bool() const { return m_is_bool;}
bool json::is_null() const { return m_is_null;}

double const& json::get_number() const{
	if(not is_number())
		throw json_exception{"get_number called on non numeric json"};
	return m_number;
}

bool const& json::get_bool() const{
	if(not is_bool())
		throw json_exception{"get_bool called on non numeric json"};
	return m_bool;
}

std::string const& json::get_string() const{
	if(not is_string())
		throw json_exception{"get_string called on non numeric json"};
	return m_string;
}

std::list<std::pair<std::string, json>> const& json::get_dict() const{
	if(not is_dictionary())
		throw json_exception{"get_dict called on non numeric json"};
	return m_dict;
}

std::list<json> const& json::get_list() const{
	if(not is_list())
		throw json_exception{"get_list called on non numeric json"};
	return m_list;
}

void json::set_null(){
	m_is_null = 1;
	m_is_bool = m_is_number = m_is_string = m_is_dict = m_is_list = 0;
	m_boolean = 0;
	m_number = 0;
	m_str = "";
	m_dict.clear();
	m_list.claar();
}

void json:set_string(std::string const& str){
	set_null();
	m_is_string = 1;
	m_is_null = 0;
	m_string = str;
}

void json:set_bool(bool const& boolean){
	set_null();
	m_is_bool = 1;
	m_is_null = 0;
	m_bool = boolean;
}

void json:set_number(double x){
	set_null();
	m_is_number = 1;
	m_is_null = 0;
	m_number = x;
}

void json:set_list(){
	set_null();
	m_is_list = 1;
	m_is_null = 0;
}

void json:set_dict(){
	set_null();
	m_is_dict = 1;
	m_is_null = 0;
}

void json::push_back(json const& x){
	if(not is_list())
		throw
	m_list.push_back
} //da finire

```