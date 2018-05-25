Funció "Dia que surt"

```sql

create function dbo.diasurt(@pres as int)
returns date
as begin
	declare @dia as date, @data_ingres as date, @dies_delicte as int
	set @dia=(select DATEADD(day,@dies_delicte,@data_ingres))
	set @data_ingres= (select data_ingres
				from pres
				where id=@pres)
				
	set @dies_delicte= (select sum(dies_pel_delicte)
				from condemna
				where id_pres=@pres)
				
	set @dia=(select DATEADD(day,@dies_delicte,@data_ingres))
	return @dia
end

```
