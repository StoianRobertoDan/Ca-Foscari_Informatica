Hanoi disk problem:
```cpp
//f = from pillar, t = to pillar, s = support pillar
void hanoi(int d, int f, int t, int s){
	if(d>1){
		hanoi(d-1, f, s, t);
		std::cout<<f<<"->"<<t<<endl;
		hanoi(d-1, s, f, t);
	}
	else{
	}
}
```


Colored tower problem:
```cpp
// base is either 'b' (blue) or 'r' (red)
int tower(int n, char base){
	if(n > 0){
		if(base == 'r') return town(n-1, 'b');
		else{
			int k1 = town(n-1, 'r');
			int k2 = town(n-1, 'b');
			return k1+k2;
		}
	}
}
```


precise sum problem:
```cpp
bool sum(const vector<int>& p, int s, int from){
	if(from < v.size())
		return sum(v, s, from++) || sum(v, s-v.at(from), from++);
	/*else {
		if(s==0) return true;
		else return false;
	}*/
	else return s==0;
}
```

Binary search
```cpp
bool binarysearch(const vector<int>& v, int n, int f, int t){
	if(f <= t) return false;
	if(f.at((f+t)/2) == n) return true;
	if(f.at((f+t)/2) < n) return binarysearch(v, n, ((f+t)/2)+1, t);
	if(f.at((f+t)/2) > n) return binarysearch(v, n, f, ((f+t)/2)-1);
}
```