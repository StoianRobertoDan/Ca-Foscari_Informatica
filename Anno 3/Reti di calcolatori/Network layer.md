Le Forwarding Tables devono essere consistent, con un preciso passo da un host all'altro.
	Possibili errori:
		Black Holes: quando un router non ha/legge la forwarding table e fa il drop del pacchetto.
		Loop del Routing: 2 o più routing loop the package between themselves
The router is divided in 2 functions:
	Data Plane:
	Control Plane: it need packages that don't have data but information to populate the forwarding tables.
Maximum Transfer Unit: 
	1500B for cabled connection
	2000B for wireless connection
	... 
Since the Host doesn't know what is the MTU of the routers, if it has sent a package with a bigger MTU the router with a lower MTU will drop the package and send back an error message so the host know how big make the package before sending it again.
The routers could also break the package in smaller units to send to the next router but it's not used because if the router doesn't receive all the units it will wait with saved packages making everything slower.

