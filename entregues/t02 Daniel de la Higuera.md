```

create table celles(
número int not null,
aforament int not null,
núm_mòdul int not null,
constraint celles_pk
primary key (número),
);

create table pressos(
número int not null,
nom varchar(500) not null,
data_ingrés datetime not null,
num_cella int not null,
constraint pressos_pk
primary key (número),
constraint pressos_a_celles_fk
foreign key (num_cella)
references celles (número)
);

create table delictes(
códi int not null,
nom varchar(400) not null,
constraint delictes_pk
primary key (códi)
);



create table permíssos(
des_de datetime not null,
fins_a datetime not null,
número_pres int not null
constraint permíssos_pk
primary key (des_de),
constraint permíssos_a_pressos_fk
foreign key (número_pres)
references pressos (número)
);

create table comdemnes(
dies_pel_delicte int not null,
códi_delicte int not null,
número_pres int not null,
constraint comdemnes_pk
primary key (códi_delicte, número_pres),
constraint comdemnes_a_pressos_fk
foreign key (número_pres)
references pressos(número),
constraint comdemnes_a_delictes_fk
foreign key (códi_delicte)
references delictes (códi)
);



```
