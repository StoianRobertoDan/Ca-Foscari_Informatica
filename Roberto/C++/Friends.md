

```cpp
std::ostream& operator<<(std::ostram& os, token const& t){
	os << "value: " << t.m_value << "; type: " << m-type;
	return os;
}
```
	overloading 

è esterna alla classe token e se m_value e m_type sono privati, operator non potrà accedervi.
Se invece nella parte pubblica della classe scriviamo:
```cpp
friend std::ostream& operator<<(std::ostream& os, token const& t);
```

essa verrà riconosciuta. Non è comunque una funzione di classe ma avrà accesso all'area privata