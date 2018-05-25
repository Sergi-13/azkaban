Procedure Otorgapermis

```sql

create procedure Otorgapermis(
@nopres as int, @diainici as date, @ndedias as int)
as begin
	declare @datedif as int, @datafinal as date, @numerosolapaments as int
	set @datedif=DATEDIFF(day, @diainici, @ndedias)
	set @datafinal=DATEADD(day, @ndedias, @diainici)
	set @numerosolapaments= (select count(*) from Permisos p where not(p.fins <@datafinal or p.principi>@datafinal ))
	if (select dbo.porcentaje(@nopres,@diainici))<50
	  raiserror('no te més del 50% de condemna',1,1)
	else
	begin
		if(@numerosolapaments=0)
			begin
				insert into Permisos values (@diainici, @datafinal, @nopres)
			end
		else raiserror('Solapació',1,1)
	end
end


```
