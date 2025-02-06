-- Create database only if it does not exist
CREATE DATABASE IF NOT EXISTS ORG123;
SHOW DATABASES;
USE ORG123;

-- Drop tables if they already exist to avoid errors
DROP TABLE IF EXISTS Bonus;
DROP TABLE IF EXISTS Title;
DROP TABLE IF EXISTS Worker;

-- Create the Worker table
CREATE TABLE Worker (
	WORKER_ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
	FIRST_NAME CHAR(25),
	LAST_NAME CHAR(25),
	SALARY INT,
	JOINING_DATE DATETIME,
	DEPARTMENT CHAR(25)
);

-- Insert data into Worker table
INSERT INTO Worker 
	(FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT) VALUES
		('Monika', 'Arora', 100000, '2020-02-14 09:00:00', 'HR'),
		('Niharika', 'Verma', 80000, '2011-06-14 09:00:00', 'Admin'),
		('Vishal', 'Singhal', 300000, '2020-02-14 09:00:00', 'HR'),
		('Amitabh', 'Singh', 500000, '2020-02-14 09:00:00', 'Admin'),
		('Vivek', 'Bhati', 500000, '2011-06-14 09:00:00', 'Admin'),
		('Vipul', 'Diwan', 200000, '2011-06-14 09:00:00', 'Account'),
		('Satish', 'Kumar', 75000, '2020-01-14 09:00:00', 'Account'),
		('Geetika', 'Chauhan', 90000, '2011-04-14 09:00:00', 'Admin');

-- Create the Bonus table
CREATE TABLE Bonus (
	WORKER_REF_ID INT,
	BONUS_AMOUNT INT,
	BONUS_DATE DATE,
	FOREIGN KEY (WORKER_REF_ID)
		REFERENCES
Worker(WORKER_ID)
        ON DELETE CASCADE
);

-- Insert data into Bonus table
INSERT INTO Bonus 
	(WORKER_REF_ID, BONUS_AMOUNT, BONUS_DATE) VALUES
		(1, 5000, '2020-02-16'),
		(2, 3000, '2011-06-16'),
		(3, 4000, '2020-02-16'),
		(1, 4500, '2020-02-16'),
		(2, 3500, '2011-06-16');

-- Create the Title table
CREATE TABLE Title (
	WORKER_REF_ID INT,
	WORKER_TITLE CHAR(25),
	AFFECTED_FROM DATETIME,
	FOREIGN KEY (WORKER_REF_ID)
		REFERENCES Worker(WORKER_ID)
        ON DELETE CASCADE
);

-- Insert data into Title table
INSERT INTO Title 
	(WORKER_REF_ID, WORKER_TITLE, AFFECTED_FROM) VALUES
		(1, 'Manager', '2016-02-20 00:00:00'),
		(2, 'Executive', '2016-06-11 00:00:00'),
		(8, 'Executive', '2016-06-11 00:00:00'),
		(5, 'Manager', '2016-06-11 00:00:00'),
		(4, 'Asst. Manager', '2016-06-11 00:00:00'),
		(7, 'Executive', '2016-06-11 00:00:00'),
		(6, 'Lead', '2016-06-11 00:00:00'),
		(3, 'Lead', '2016-06-11 00:00:00');

-- Queries:

-- 1. Select workers with salary not between 100000 and 200000
SELECT * FROM Worker WHERE SALARY NOT BETWEEN 100000 AND 200000;

-- 2. Select first names of workers with specific worker IDs
SELECT FIRST_NAME FROM Worker WHERE WORKER_ID IN (2, 4, 6);

-- 3. Select workers with salary between 200000 and 400000 and specific worker IDs
SELECT * FROM Worker 
WHERE SALARY BETWEEN 200000 AND 400000 
AND WORKER_ID IN (1, 2, 3, 4, 5);

-- 4. Describe the Worker table
DESC Worker;

-- 5. Get the minimum salary in the HR department
SELECT MIN(SALARY) FROM Worker WHERE DEPARTMENT = 'HR';

-- 6. Get distinct departments
SELECT DISTINCT DEPARTMENT FROM Worker;

-- 7. Alias example - Rename WORKER_ID as EMP_ID
SELECT WORKER_ID AS EMP_ID FROM Worker;

-- 8. UNION ALL: Get worker IDs and first names combined into a single column
SELECT WORKER_ID FROM Worker
UNION ALL
SELECT FIRST_NAME FROM Worker;

-- 9. UNION with ORDER BY: Get department and worker IDs for specific salaries
SELECT DEPARTMENT, WORKER_ID FROM Worker WHERE SALARY = 100000
UNION 
SELECT DEPARTMENT, WORKER_ID FROM Worker WHERE SALARY = 200000
ORDER BY WORKER_ID;

-- 10. CASE statement to classify workers based on salary
SELECT WORKER_ID, FIRST_NAME, DEPARTMENT,
CASE
    WHEN SALARY > 100000 THEN 'Rich People'
    WHEN SALARY BETWEEN 50000 AND 100000 THEN 'Middle Class People'
    ELSE 'Poor'
END AS People_stage_wise 
FROM Worker;
    ELSE 'Poor people'
END 
AS People_stage_wise
FROM worker;

