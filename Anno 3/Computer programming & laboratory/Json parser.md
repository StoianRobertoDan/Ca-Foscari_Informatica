```cpp

struct json{
	json();
	bool is_list() const;
	bool is_dictionary() const;
	bool is_string() const;
	bool is_number() const;
	bool is_bool() const;
	bool is_null() const;

	double const& get_number() const;
	bool const& get_bool() const;
	std::string const& get_string() const;
	std::list<std::pair<std::string, json>>& get_dict();
	std::list<std::pair<std::string, json>> const& get_dict() const;
	std::list<json> const& get_list() const;

	//Setters
	//delete the current content of the json, convert it to string and  
	double 
privete:
	bool is_null;
	bool is_list;

	bool boolean;
	double m_double;
};
```