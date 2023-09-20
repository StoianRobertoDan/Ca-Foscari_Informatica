``` cpp
stack s;
s.push(40);
s.push(20);
s.pop(); //cancella il 40
s.pop(); //cancella il 20
```

stack -> lista di oggetti con una push e una pop
per migliorare le prestazioni si può usare un solo puntatore e:
	-usare per fare la push un append (aggiungere in coda)
	-usare per la pop una remove sulla testa
	MA push e pop in questo modo sembra che ci costringa


notazione polacca postfissa:
invece che 2 + 3 si scriverebbe 2 3 +
perchè è utile?
	(2 + 3) * 5 diventa  2 3 + 5 * e funzione
		si inserisce il 2, il 3 e l'operatore +, allora si fa 2+3, si toglie 2, 3 e + e si aggiunge il risultato 5. Allora si aggiunge 5 e loperatore * . Si calcola 5 * 5, si tolgono 5, 5 e * e si aggiunge il risultato 25.
	2 + 3 * 5 diventa 2 3 5 * + e funziona
		si inserisce il 2, il 3 , il 5 e l'operatore * , allora si fa 3 * 5 , si toglie 3, 5 e * e si aggiunge il risultato 15. Allora si aggiunge l'operatore +. Si calcola 2+15, si tolgono 2, 15 e + e si aggiunge il risultato 17.