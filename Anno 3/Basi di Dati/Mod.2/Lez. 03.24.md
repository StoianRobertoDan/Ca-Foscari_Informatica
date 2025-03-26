```plSQL
drop function if exists text();
drop function if exists text(s1 text, s2 text);
create or replace function text(s1 text, s2 text) return text
as $$
begin
	raise notice 'funzione: (% %)', s1, s2;
	return s1 || ' ' || s2;
end;
$$ language plpgsql;

select test('Hello', 'World');

```

```plsql
drop function if exists text();
drop function if exists text(s1 text, s2 text);
drop function if exists text(s1 text );
create or replace function text(maker text) return int
as $$
begin
	raise notice 'funzione: %', maker;
	return (select count(*) from lab.product p where p.maker like (test.maker))
end;
$$ language plpgsql;

select test('Asus');
```

```plsql
drop function if exists text();
drop function if exists text(s1 text, s2 text);
drop function if exists text(s1 text );
create or replace function text(maker text) return int
as $$
declare num int;
declare num2 int;
begin
	raise notice 'funzione: (%)', maker;
	select p.maker, count(*) into mak, num
	from lab.product p group by p.maker
	return (select count(*) from lab.product p where p.maker like (test.maker))
end;
$$ language plpgsql;

select test('Asus');
```