il vcs è un server di salvataggio che manage differenti versioni del programma (vengono mantenute le versioni precedenti). viene usato principalmente per codici sorgente e si può fare upload e donload dal server.


Git:
usato soppratutto dai developer per tenere traccia dei software e rende possibile il lavoro in contemporanea. si può usare anche per altri tipi di file e progetti.
Da più sicurezza perchè i codici vengono salvati e copiati su più server.
Scaricando un codice si scarica una copia e lavorandoci si creano commit, salvataggi delle modifiche. I commit possono essere tanti prima di fare l'upload della nuova versione oppure essere integrati tutti nella nuova versione. 
Le istruzioni di pull e push servono a spostare i codici tra server e macchina. la pull è diversa dalla copia (clone) perchè ci deve essere già il progetto nella macchina e non sovrascrive il progetto già esistente.
Fare commit contemporaneamente senza fare pull comporta complicanze perchè vengono cambiare cose diverse contemporaneamente. Git allora non permette di fare il push di un commit di una versione precedente e invece chiede di fare il pull, cerca di fare una merge dei 2 progetti se le modifiche sono su file diversi o su parti diverse e se non riesce a fare il merge automatico richiede che si faccia un merge manuale prima di fare la push.

