
Espressioni: calcolano qualcosa e hanno un tipo
es:
```
5
5+3
x+4
x<5 && y >7
```
Statement: fa qualcosa 



Dynamic Dispatcing


Subsumtion (sussunzione, contrario di assunzione)
Si possomo creare dei dati generali e metterci dentro una variabile più specifica (sottostante ad essa, sottoclasse). Non vale il contrario, cioè mettere in una sottoclasse una variabile più generale.
Questo interessa cosa succede a compiler time, non a runtime.
Succede non solo nei binding ma anche nel passaggio di parametri
```
void eats(animal a){};

Dog fido = new Dog(...);
pippo.eats(Dog); //va bene per subsumtion da dog a animal
```


Liste e Array diverse solo di contratto. Fanno le stesse cose ma in modi diversi. Sono comunque entrambe lineari e indicizzabili, ma gli array hanno anche contiguità e sono di conseguenza più prestazionali.

Classe e interfacce.
L'interfaccia definisce solo le firme dei metodi ma non anche la loro implementazione (tranne nel caso dei default)


l'operatore == su tipi primitivi confronta il valore. il tipo deve per forza essere uguale altrimenti c'è errore di compilazione.
Su oggetti non primitivi confronta le reference e ritorna true solo se i 2 tipi sono esattamente lo stesso, non se hanno gli stessi valori.
