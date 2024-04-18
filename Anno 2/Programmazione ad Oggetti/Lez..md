```java
package func;
import java.util.Collection;

public class lambda{
	//public static <A, B> Collection<A> map(Collection<A> c, ...);
	public static Integer f(Integer x) { return x + 1; }
	
	interface MyFunction<T>{ //funzione che prende un tipo e non ritorna niente
		void apply(T x);
	}
	
	interface MyFunction<A, B>{ //funzione che prende un tipo per la funzione e un tipo per il ritorno
		B apply(A x);
	}
	
	public static <A, B> Collection<B> map(Collection<A> c, Function<A, B> f){
		Collection<B> r = new ArrayList<>();
		for(A x : c){
			B b = f.apply(x);
			r.add(b); //si poteva anche scrivere r.add(f.apply(x))
		}
		return r;
	}
	
	public static <T> void forEach(Collection<T> c, Fumction <T, void> f){
		for(T x : c){
			f.apply(x);
		}
	}
	
	public static void main(String[] args){
		List<Integer> l = List.of(1, 2, 3, 4);
		forEach(l, new MyFunction<Integer>(){ //ItelliJ rende grigio la new della funzione perchè può essere scritto più velocemente. Come? lambda (Sotto)
			@Override
			public void apply(Integer x){
				System.out.print(x);
			}
		});
		
		forEach(l, x -> System.out.print(x)); //Versione con la lambda
		//Non gli stiamo dando ne il nome della funzione (Anonymus class) ne il tipo dei dati ne quello di ritorno
		
		forEach(l, new MyFunction<Integer>(){
			@Override
			public void apply(Integer x){ //Siccome passiamo per Integer passiamo per reference. Passanod per int passeremo per copia
				x = x + 1; //IntelliJ sottolinea la prima x come "variabile non uttilizzata"
			}
		});
		
		forEach(l, x -> x = x + 1);
		
		forEach(l, new MyFunction<Integer>(){
			@Override
			public void apply(Integer x){ 
				if(x > 5)
					x = x + 1;
			}
		});
		
		forEach(l, x -> {if(x > 5) x = x + 1;});
	}
	
	public static void main2(){
		List<Integer> l = new ArrayList<>();
		
		Collection<Integer> r1 = map(l, x -> x + 1);
		Collection<Integer> r1 = map(l, new Function<Integer, Integer>(){
			@Override
			
		});
		
	}
}


```

Function funzione che prende in input e ritorna. su usa la keyword apply
Supplier funzione che non prende in input e ritorna. Si usa Get
Consumer funzione che prende in input e non ritorna. si usa la keyword 
Runnable funzione che  non prende in input e non ritorna. Si usa Run

```c
int f(double x) {}
int(*)(double) //tutto questo è un tipo
int(*)(double) g = f; //dichiarazione e binding ma sbagliato
int(*g)(double) = f; //assegnazione e binding corretto

//funzione di secondo grado in C
//prende un array (puntatore alla prima e lunghezza perchè siamo in C) e una funzione (function pointer) f void che prende in input un int
void for_each(int* a, size_t len, void(*f)(int)){
	for(int i = 0; i < len; i++){
		f(a[i]);
	}
}

void print_int(int n){
	printf("%d/n", n);
}

void int(){
	int a[10];
	for_each(a, 10, print_int); //chiamata della funzione di secondo grado
	
	for_each(a, 10, printf("&d/n")) //in C non si può fare
}
```