Creazione di un processo:
- Creazione di un nuovo ID
- Allocazione della memoria
- Allocazione delle risorse
- Gestione delle informazioni del processo
- Creazione del PCB

Fork
La chiamata di sistema `fork()` è un'operazione fondamentale nei sistemi operativi basati su UNIX e simili. Questa chiamata di sistema consente di creare un nuovo processo (processo figlio) che è una copia esatta del processo chiamante (processo genitore). 

Quando un programma chiama `fork()`, il sistema operativo crea un nuovo processo che è una copia esatta del processo che ha effettuato la chiamata. Entrambi i processi (il processo genitore e il processo figlio) iniziano l'esecuzione a partire dal punto in cui si trova la chiamata a `fork()`. **Tuttavia, ciascun processo riceve un valore di ritorno diverso dalla chiamata a `fork()`, il quale indica quale processo è il genitore e quale è il figlio. **

Nel processo genitore, il valore di ritorno è il PID (Process IDentifier) del processo figlio appena creato. Nel processo figlio, il valore di ritorno è 0. Questo consente ai due processi di distinguersi l'uno dall'altro. Inoltre, entrambi i processi hanno il loro spazio di indirizzamento virtuale separato, quindi le modifiche fatte da uno dei processi non influenzano l'altro.

La chiamata di sistema `fork()` è ampiamente utilizzata per creare processi paralleli o per avviare nuovi programmi all'interno di un programma esistente. Ad esempio, molti server che possono gestire più richieste simultaneamente utilizzano `fork()` per creare un nuovo processo per gestire ogni richiesta.

Usando la fork ed eseguendo i 2 processi contemporaneamente se sono sullo stesso blocco (timesharing) tendono a stampare blocchi di un processo alternati a blocchi dell'altro mentre se sono su 2 blocchi diversi tendono ad andare in modo parallelo abbastanza alternati.