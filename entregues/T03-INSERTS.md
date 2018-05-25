CREATE TABLE

````sql

create table delicte(
codi int not null, 
nom varchar (200) not null,
constraint delicte_pk
primary key (codi)
);

create table cella(
numero_cella int not null,
aforament int not null,
numero_modul int not null,
constraint cella_pk 
primary key (numero_cella)
);

create table pres (
numero_pres int not null, 
nom varchar(200) not null,
data_ingres date not null,
numero_cella int not null,
constraint pres_pk
primary key (numero_pres),
constraint pres_cella 
foreign key (numero_cella)
references cella (numero_cella)
ON UPDATE CASCADE
);

create table comdenna (
dies_pel_delicte int not null,
numero_pres_pres int not null, 
codi_delicte int not null,
constraint comdenna_pk
primary key (dies_pel_delicte,numero_pres_pres,codi_delicte),
constraint delicte_comdenna 
foreign key (codi_delicte)
references delicte (codi),
constraint pres_comdenna 
foreign key (numero_pres_pres)
references pres (numero_pres),
);

create table permis (
des_de date not null,
fins_a date not null,
numero_pres_permis int not null, 
constraint permis_pk
primary key (numero_pres_permis,des_de),
constraint permis_pres
foreign key (numero_pres_permis)
references pres (numero_pres)
);

````

INSERTS

````sql 

insert into cella values (1,1,1)
insert into cella values (2,2,2)
insert into cella values (3,1,3)

insert into pres values (1,'Carlotta Pinkstone','2018-01-01',1)
insert into pres values (3,'Antonin Dolohov','2016-05-01',2)
insert into pres values (2,'Bartemius Crouch Jr','2015-01-01',3)

insert into delicte values (1,'Estatuto Internacional del Secreto Mágico')
insert into delicte values (2,'Torturar con la maldición Cruciatus')
insert into delicte values (3,'Assessinar')

insert into comdenna values (600,1,1)
insert into comdenna values (300,2,2)
insert into comdenna values (900,3,2)
insert into comdenna values (900,3,3)

````
