Funcio Percentatge


```

create function dbo.percentatge (@numero_pres as int)
returns int
as begin
	declare @dies_totals as int
	set @dies_totals =(select sum(c.dies_per_delicte)
						from pres p
						inner join condena c
						on c.numero_pres = p.numero
						where @numero_pres= p.numero)
	declare @diferencia as int
	set @diferencia = (select datediff(day, data_ingres, GETDATE())
						from pres
						where @numero_pres = numero)
	declare @percentatge as int
	set @percentatge = ((@diferencia*100)/@dies_totals)
	if(@percentatge>100)
	begin
		set @percentatge = 100
	end
	return @percentatge
end

```
