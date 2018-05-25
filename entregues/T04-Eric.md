Funció "Dia que surt"

```

create function dbo.diaquesurt(@pres as int)
returns date
as begin
	declare @dia as date
	set @dia=(select DATEADD(day,sum(c.dies_pel_delicte),p.data_ingres)
				from pres p
				inner join condemna c
				on p.id=c.id_pres
				where p.id=@pres
				group by p.data_ingres)
	return @dia
end

```
