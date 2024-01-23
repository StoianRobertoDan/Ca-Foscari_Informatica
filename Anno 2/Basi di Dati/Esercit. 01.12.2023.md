
```sql
select count(*)
from pizze pi
where not exists(select *
				 from ricette r natural join ingredienti i
				 where i.nome = 'pomodoro' and pi.codpizza = r.codpizza)

```

```sql
select pi.nome, count(pi.codpizza) as numordini
from pizze pi left join ordini o on pi.codpizza = o.codpizza and o.nomecliente = 'Mario Rossi'
group by pi.codpizza, pi.nome
order by numordini desc

select pi.nome, count(pi.codpizza) as numordini
from pizze pi left join ordini o on pi.codpizza = o.codpizza
where o.nomecliente = 'Mario Rossi' /*questo toglie i valori non usati (in questo caso le pizze non ordinate da mario rossi)*/
group by pi.codpizza, pi.nome
order by numordini desc
```

//clienti che hanno ordinato almeno 3 pizze diverse
```sql
select o.nomecliente
from ordini o /*non serve fare il join con pizze perchè basta guardare la chiave codpizze per vedere se sono diverse*/
group by o.nomecliente
having count(distinct o.codpizza) >= 3 /*importante distinct altrimenti seleziona in generale clienti che hanno ordinato almeno 3 pizze*/
```

Per ogni cliente trovare quante volte hanno ordinato margherita, capricciosa e boscaiola. Restituire eventuali 0.
```sql
select o.nomecliente, sum(case when pi.nome = 'Margherita' then 1 else 0) as numMargherita, sum(case when pi.nome = 'Capricciosa' then 1 else 0) as numCapricciosa, sum(case when pi.nome = 'Boscaiola' then 1 else 0) as numBoscaiola
from ordini o natural join pizze pi 
group by o.nomecliente
```

