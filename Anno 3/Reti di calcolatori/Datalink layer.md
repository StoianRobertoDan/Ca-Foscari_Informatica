... 

CRC (Cyclic redundancy check): checksum
Internet Checksum: campo di 16 bit in complemento ad uno (0 e 1 campiati con il loro corrispettivo). 


BER 
Perdere (con un errore) il primo e ultimo bit di un DataPack porta alla perdita di tutto il pack. Se abbiamo un 2.6% di perdita ci si aspetta il 26% dei pacchetti persi.

Sequence numbers:
	Dividiamo i pacchetti in pari e dispari con un solo bit
	ABP (alternating bit protocol).
		Nel pdf c'è la state machine
		Ho bisogno di 4 stati, 2 bit di controllo e un buffer
		I pacchetti stano in stallo fino all'arrivo de D(okn)
SDU (Service Data Unit) un pacchetto che arriva dal layer superiore.

