# Otorgar un permís

```sql
create procedure otorgrarUnPermis(
@pres int , @dataInici date, @diesDePermis int
) as begin
	begin transaction
	set transaction isolation level serializable
	declare @percentatge int;
	set @percentatge = dbo.quinDiaSurt(@pres);
	if @percentatge < 50 
		begin
		raiserror('No pot',16,1); 
		rollback;
		end
	else
		begin
		declare @dataFinal date;
	select @dataFinal = DATEADD(day,@diesDePermis,@dataInici);
	declare @nSolapaments as int;
	select @nSolapaments = count(*) from permis p where not((p.des_de <= @dataInici and p.fins_a < @dataFinal) or (p.des_de > @dataFinal));
	if @nSolapaments > 0 
		begin
		raiserror('No pot',16,1); 
		rollback;
		end
	else
		begin
		insert into permis (id_pres,des_de,fins_a)
	values (@pres,@dataInici,@dataFinal);
	commit;
		end
		end
end
```
