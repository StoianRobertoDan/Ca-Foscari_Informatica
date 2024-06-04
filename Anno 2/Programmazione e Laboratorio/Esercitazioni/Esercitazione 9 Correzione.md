
```cpp
class SquareMat{

 private:
	 std::vector<std::vector<int>> m;
};


SquareMat::SquareMat(int dim)}{
	m.resize(dim);
	for(int i = 0; i < m.dim; i++){
		m[i].resize(dim);
		for(int j = 0; j < dim; j++;)
			m[i][j] = 0;
	}
}

SquareMat::SquareMat(const SquareMat& s)}{
	int dim = s.size();
	m.resize(dim);
	for(int i = 0; i < dim; i++){
		m[i].resize(dim);
		for(int j = 0; j < dim; j++;)
			m[i][j] = s.at(i,j); // oppure s.m[i][j]
	}
}

int& SquareMat::at(int r, int c){
	return m[r][c];
}

SquareMat& SquareMat::reduce(int r, int c){
	SquareMat reduced(size() - 1);
	int r_idx = 0, c_idx = 0;
	for(int i = 0; i < size() i++){
		if(i != r){
			c_idx = 0;
			for(int j = 0; j < size(); j++){
				if(j != c){
					reduced.at(r_idx, c_idx) = m[i][j];
					c_idx++;
				}
			}
			r_idx++;
		}
	}
	return reduced;
}

int SquareMat::determinant() const{
	if(size == 1) return m[0][0];
	else{
		int det = 0, s = 1;
		for(int j = 0; j < size(); j++){
			SquareMat red = reduce(0, j);
			det += s * m[o][j] * red.determinant();
			s = -1 * s;
		}
		return det;
	}
}

//funzione sottointesa bool is_prime (int n){}

bool allprimes(SquareMat s){
	for(int i = 0; i < s,size(); i++)
		for(int j = 0; j < s,size(); j++)
			if(!is_prime(s.at(i, j))) return false;
}
```