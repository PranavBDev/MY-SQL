show databases;
create database VIT;
USE ViT;
create table BOE(
student_id int, 
s_name varchar(100), 
s_mark int
);
show tables from ViT;
select * from BOE;
insert into BOE values (101, 'Amatya', 99),
(102, 'Rohan', 95),
(103, 'Sneha', 92),
(104, 'Kiran', 98),
(105, 'Priya', 97);
desc BOE;
alter table BOE drop column s_contact;
insert into BOE values (106, 'Shambhu', 97);
alter table BOE add(
	s_country varchar(25) DEFAULT 'INDIA'
);
use vit;
alter table boe rename column
	s_country TO s_state;
desc boe;

create database practice1;
use practice1;
create table Mech(s_id int,s_name varchar(25));
START TRANSACTION;
insert into Mech values (101,'jayanth');
SAVEPOINT A;
update mech set s_id=102 where s_id=101;
SAVEPOINT B;
insert into Mech values (103,'Karthick');
select * from mech;
SAVEPOINT C;
select * from mech;
ROLLBACK TO B;
select * from mech;
commit;

CREATE DATABASE ORG123;
SHOW DATABASES;
USE ORG123;

CREATE TABLE Worker (
	WORKER_ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
	FIRST_NAME CHAR(25),
	LAST_NAME CHAR(25),
	SALARY INT(15),
	JOINING_DATE DATETIME,
	DEPARTMENT CHAR(25)
);

INSERT INTO Worker 
	(WORKER_ID, FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT) VALUES
		(001, 'Monika', 'Arora', 100000, '14-02-20 09.00.00', 'HR'),
		(002, 'Niharika', 'Verma', 80000, '14-06-11 09.00.00', 'Admin'),
		(003, 'Vishal', 'Singhal', 300000, '14-02-20 09.00.00', 'HR'),
		(004, 'Amitabh', 'Singh', 500000, '14-02-20 09.00.00', 'Admin'),
		(005, 'Vivek', 'Bhati', 500000, '14-06-11 09.00.00', 'Admin'),
		(006, 'Vipul', 'Diwan', 200000, '14-06-11 09.00.00', 'Account'),
		(007, 'Satish', 'Kumar', 75000, '14-01-20 09.00.00', 'Account'),
		(008, 'Geetika', 'Chauhan', 90000, '14-04-11 09.00.00', 'Admin');

SELECT * FROM worker
WHERE salary BETWEEN 200000 AND 400000
AND worker_id IN (1,2,3,4,5);

SELECT worker_id, first_name,department,
CASE
    WHEN salary > 300000 THEN 'Rich people'
    WHEN salary <=300000 && salary >=100000 THEN 'Middle stage'
    ELSE 'Poor people'
END 
AS People_stage_wise
FROM worker;

