```sql

-- //////////////////////////
-- Pre-defined Functions

SELECT Length(NAME)
FROM   personal
WHERE  id = 2;

SELECT Char_length(NAME)
FROM   personal
WHERE  id = 2;

SELECT Concat("yahoo", "baba", "youtube", "channel") AS NAME;

SELECT Concat_ws("-", "baba", "youtube", "channel") AS NAME;

SELECT Substring("yahoo baba", 3) AS NAME;

SELECT Substring_index("www.yahoobaba.net", ".", 1) AS NAME;

SELECT Space(10) AS NAME;

SELECT Pow(2, 3);

SELECT Round(1234.987);

SELECT Ceil(4.23);

SELECT Floor(4.23);

SELECT Abs(-56.25);

SELECT Sign(-25);

SELECT Sign(25);

SELECT Sec_to_time("5454") AS Time;

SELECT Timestamp("2019-06-15", "13:15:20") AS Time;

SELECT Format(255.3568, 2) AS Value;

SELECT Find_in_set("shyam", "ram,mohan,shyam") AS NAME;

SELECT Field("mohan", "ram", "mohan", "shyam") AS NAME;



-- //////////////////////////
-- Primary and Foreign Key

CREATE TABLE city
  (
     cid      INT NOT NULL auto_increment,
     cityname VARCHAR(50) NOT NULL,
     PRIMARY KEY (cid)
  );

INSERT INTO city
            (cityname)
VALUES     ('Agra'),
            ('Delhi'),
            ('Bhopal'),
            ('Jaipur'),
            ('Noida');

CREATE TABLE personal
  (
     id         INT NOT NULL,
     name       VARCHAR(50) NOT NULL,
     percentage INT NOT NULL,
     age        INT NOT NULL,
     gender     VARCHAR(1) NOT NULL,
     city       INT NOT NULL,
     PRIMARY KEY(id),
     FOREIGN KEY (city) REFERENCES city(cid)
  );


INSERT INTO PERSONAL(id,name,percentage,age,gender,city)
VALUES
(1,"Ram Kumar","45","13","M",1),
(2,"Sarita Kumari","56","21","F",2),
(3,"Salman Khan","62","20","M",1),
(4,"Juhi Chawla","47","18","F",3),
(5,"Anil Kapoor","74","22","M",1),
(6,"John Abraham","64","21","M",2),
(7,"Shahid Kapoor","52","20","M",1);


SELECT * FROM   personal;

-- //////////////////////////
--Indexing

CREATE TABLE students
  (
     id         INT NOT NULL,
     name       VARCHAR(50) NOT NULL,
     percentage INT NOT NULL,
     dob        DATE NOT NULL,
     age        INT NOT NULL,
     gender     VARCHAR(1) NOT NULL,
     city       INT NOT NULL,
     courses    INT NOT NULL,
     PRIMARY KEY (id),
     FOREIGN KEY (city) REFERENCES city (cid),
     FOREIGN KEY (courses) REFERENCES courses (course_id)
  );


INSERT INTO students(id,name,percentage,dob,age,gender,city,courses)
VALUES
(1,"Ram Kumar","45","2000-05-10","19","M",1,1),
(2,"Sarita Kumari","85","1997-02-03","22","F",2,2),
(3,"Salman Khan","29","1999-11-12","20","M",1,1),
(4,"Juhi Chawla","47","2001-07-16","18","F",3,1),
(5,"Anil Kapoor","74","1997-01-03","22","M",1,3),
(6,"John Abraham","64","1998-08-10","21","M",2,2),
(7,"Shahid Kapoor","62","1999-12-08","20","M",1,3);


SELECT *
FROM   students
WHERE  dob > "1999-01-01";

CREATE INDEX studdob ON students (dob);

SHOW INDEX FROM students;

DROP INDEX studdob ON students;

SHOW INDEX FROM students;


-- //////////////////////////
--JOINS

CREATE TABLE personal
  (
     id         INT NOT NULL,
     name       VARCHAR(50) NOT NULL,
     percentage INT NOT NULL,
     age        INT NOT NULL,
     gender     VARCHAR(1) NOT NULL,
     city       INT NOT NULL,
     PRIMARY KEY (id),
     FOREIGN KEY (city) REFERENCES city (cid)
  );

CREATE TABLE city
  (
     cid      INT NOT NULL auto_increment,
     cityname VARCHAR(50) NOT NULL,
     PRIMARY KEY (cid)
  );

INSERT INTO personal(id,name,percentage,age,gender,city)
VALUES
(1,"Ram Kumar","45","13","M",1),
(2,"Sarita Kumari","56","21","F",2),
(3,"Salman Khan","62","20","M",1),
(4,"Juhi Chawla","47","18","F",3),
(5,"Anil Kapoor","74","22","M",1),
(6,"John Abraham","64","21","M",2),
(7,"Shahid Kapoor","52","20","M",1);

INSERT INTO city(cityname)
VALUES('Agra'),
('Delhi'),
('Bhopal'),
('Jaipur'),
('Noida');

-- //////////////////////////
--INNER JOIN

SELECT p.id,
       p.name,
       p.percentage,
       p.age,
       p.gender,
       c.cityname
FROM   personal AS p
       INNER JOIN city AS c
               ON p.city = c.cid
WHERE  c.cityname = "agra"
ORDER  BY p.NAME;

-- //////////////////////////
--LEFT JOIN

SELECT p.id,
       p.name,
       p.percentage,
       p.age,
       p.gender,
       c.cityname
FROM   personal AS p
       LEFT JOIN city AS c
              ON p.city = c.cid
WHERE  gender = "m"
ORDER  BY p.NAME;

SELECT p.id,
       p.NAME,
       p.percentage,
       p.age,
       p.gender,
       c.cityname
FROM   city AS c
       LEFT JOIN personal AS p
              ON p.city = c.cid
ORDER  BY p.NAME;

-- //////////////////////////
--RIGHT JOIN

SELECT p.id,
       p.name,
       p.percentage,
       p.age,
       p.gender,
       c.cityname
FROM   personal AS p
       RIGHT JOIN city AS c
               ON p.city = c.cid;

SELECT p.id,
       p.name,
       p.percentage,
       p.age,
       p.gender,
       c.cityname
FROM   city AS c
       RIGHT JOIN personal AS p
               ON p.city = c.cid
WHERE  gender = "m"
ORDER  BY p.NAME;

-- //////////////////////////
--CROSS JOIN

SELECT p.id,
       p.name,
       c.cityname
FROM   personal p
       CROSS JOIN city c;

-- //////////////////////////
-- UNION & UNIONALL

CREATE TABLE courses
  (
     course_id   INT NOT NULL auto_increment,
     course_name VARCHAR(50) NOT NULL,
     PRIMARY KEY (course_id)
  );

CREATE TABLE city
  (
     cid      INT NOT NULL auto_increment,
     cityname VARCHAR(50) NOT NULL,
     PRIMARY KEY (cid)
  );

CREATE TABLE students
  (
     id      INT NOT NULL,
     name    VARCHAR(50) NOT NULL,
     age     INT NOT NULL,
     gender  VARCHAR(1) NOT NULL,
     city    INT NOT NULL,
     courses INT NOT NULL,
     PRIMARY KEY (id),
     FOREIGN KEY (city) REFERENCES city (cid),
     FOREIGN KEY (courses) REFERENCES courses (course_id)
  );

CREATE TABLE lecturers
  (
     id      INT NOT NULL,
     name    VARCHAR(50) NOT NULL,
     age     INT NOT NULL,
     gender  VARCHAR(1) NOT NULL,
     city    INT NOT NULL,
     courses INT NOT NULL,
     PRIMARY KEY (id),
     FOREIGN KEY (city) REFERENCES city (cid),
     FOREIGN KEY (courses) REFERENCES courses (course_id)
  );

INSERT INTO city(cityname)
VALUES('Agra'),
('Delhi'),
('Bhopal'),
('Jaipur'),
('Noida');

INSERT INTO courses(course_name)
VALUES('Btech'),
('BCA'),
('MBA');

INSERT INTO personal(id,name,percentage,age,gender,city,courses)
VALUES
(1,"Ram Kumar","45","13","M",1,1),
(2,"Sarita Kumari","56","21","F",2,2),
(3,"Salman Khan","62","20","M",1,1),
(4,"Juhi Chawla","47","18","F",3,1),
(5,"Anil Kapoor","74","22","M",1,3),
(6,"John Abraham","64","21","M",2,2),
(7,"Shahid Kapoor","52","20","M",1,3);

INSERT INTO lecturers(id,name,age,gender,city,courses)
VALUES
(1,"Raj Kapoor","37","M",1,2),
(2,"Sadhna","39","F",4,3),
(3,"Ram Kumar","38","M",2,1),
(4,"Salim Khan","45","M",3,2),
(5,"Nagma","42","F",2,1);


SELECT * FROM students
UNION
SELECT * FROM lecturers;

SELECT name FROM students
UNION
SELECT name FROM lecturers;

SELECT name FROM students
UNION ALL
SELECT name FROM lecturers;

SELECT name,age FROM students WHERE gender ="M"
UNION ALL
SELECT name,age FROM lecturers WHERE gender ="M";

SELECT name,age FROM students WHERE gender ="M"
UNION ALL
SELECT name,age FROM lecturers WHERE gender ="F";

SELECT name,age FROM students WHERE city = 2
UNION ALL
SELECT name,age FROM lecturers WHERE city = 2;


-- //////////////////////////
-- VIEWS

CREATE VIEW studentdata
AS
  SELECT id,NAME,course_name
  FROM   students s
         INNER JOIN courses c
                 ON s.courses = c.course_id;

SELECT * FROM studentdata;

ALTER VIEW studentdata
AS
  SELECT id,NAME,course_name,cityname
  FROM   students s
         INNER JOIN courses c
                 ON s.courses = c.course_id
         INNER JOIN city ci
                 ON s.city = ci.cid;

SELECT * FROM studentdata;

CREATE OR REPLACE VIEW studentdata
AS
  SELECT id,NAME,course_name,cityname
  FROM   students s
         INNER JOIN courses c
                 ON s.courses = c.course_id
         INNER JOIN city ci
                 ON s.city = ci.cid;

RENAME TABLE studentdata TO studentcourse;

SELECT * FROM studentcourse;

DROP VIEW studentcourse;


-- //////////////////////////
-- SubQuery

CREATE TABLE courses
  (
     course_id   INT NOT NULL auto_increment,
     course_name VARCHAR(50) NOT NULL,
     PRIMARY KEY (course_id)
  );


CREATE TABLE personal
  (
     id         INT NOT NULL,
     NAME       VARCHAR(50) NOT NULL,
     percentage INT NOT NULL,
     age        INT NOT NULL,
     gender     VARCHAR(1) NOT NULL,
     city       INT NOT NULL,
     courses    INT NOT NULL,
     PRIMARY KEY (id),
     FOREIGN KEY (courses) REFERENCES courses (course_id)
  );

INSERT INTO courses(course_name)
VALUES('Btech'),
('BCA'),
('MBA');

INSERT INTO personal(id,name,percentage,age,gender,city,courses)
VALUES
(1,"Ram Kumar","45","13","M",1,1),
(2,"Sarita Kumari","56","21","F",2,2),
(3,"Salman Khan","62","20","M",1,1),
(4,"Juhi Chawla","47","18","F",3,1),
(5,"Anil Kapoor","74","22","M",1,3),
(6,"John Abraham","64","21","M",2,2),
(7,"Shahid Kapoor","52","20","M",1,3);

SELECT NAME
FROM   personal
WHERE  courses = (SELECT course_id
                  FROM   courses
                  WHERE  course_name = "mba");

SELECT course_id
FROM   courses
WHERE  course_name IN ( "mba", "btech" );

SELECT NAME
FROM   personal
WHERE  courses IN (SELECT course_id
                  FROM   courses
                  WHERE  course_name IN ( "mba", "btech" ));


SELECT NAME
FROM   personal
WHERE  EXISTS (SELECT course_id
              FROM   courses
              WHERE  course_name IN ( "mba" ));

SELECT NAME
FROM   personal
WHERE  EXISTS (SELECT course_id
              FROM   courses
              WHERE  course_name IN ( "mtech" ));


SELECT NAME
FROM   personal
WHERE NOT EXISTS (SELECT course_id
              FROM   courses
              WHERE  course_name IN ( "mtech" ));

SELECT NAME
FROM   personal
WHERE NOT EXISTS (SELECT course_id
               FROM   courses
               WHERE  course_name IN ( "mba" ));


-- //////////////////////////
-- User Defined Funtions

-- Scalar Valued Functions

DELIMITER $$

CREATE FUNCTION add_five(`num` AS INT)
RETURNS INT
AS
  BEGIN
      RETURN( `num` + 5 )
  END $$

DELIMITER ;

SELECT mysql.add_five(10);


-- Table Valued Functions

CREATE TABLE personal
  (
     id         INT NOT NULL,
     name       VARCHAR(50) NOT NULL,
     percentage INT NOT NULL,
     age        INT NOT NULL,
     gender     VARCHAR(1) NOT NULL,
     city       INT NOT NULL,
     PRIMARY KEY (id)
  );

INSERT INTO personal(id,name,percentage,age,gender,city)
VALUES
(1,"Ram Kumar","45","13","M","Agra"),
(2,"Sarita Kumari","56","21","F","Delhi"),
(3,"Salman Khan","62","20","M","Agra"),
(4,"Juhi Chawla","47","18","F","Bhopal"),
(5,"Anil Kapoor","74","22","M","Agra"),
(6,"John Abraham","64","21","M","Delhi"),
(7,"Shahid Kapoor","52","20","M","Agra")

CREATE FUNCTION select_gender(@gender AS VARCHAR(1))
RETURNS TABLE
AS
    RETURN
      (SELECT *
       FROM   personal
       WHERE  gender = @gender)

SELECT mysql.select_gender("M");



-- //////////////////////////
-- Stored Procedures

DELIMITER $$

CREATE PROCEDURE sp_name()
BEGIN
  -- statements
END $$

DELIMITER ;

-- Parameterless Stored Procedure
DELIMITER $$

CREATE PROCEDURE personlist()
AS
  BEGIN
    SELECT *
    FROM   personal
    WHERE  gender = "m"
  END $$

DELIMITER ;

-- Example 1
-- calculate area and circumference of circle and display result on cli.
-- radius of circle is 7.

DELIMITER $$

CREATE PROCEDURE sp_circle()
BEGIN
	DECLARE v_radius DOUBLE DEFAULT 7.0;
	DECLARE v_area DOUBLE;
	DECLARE v_circum DOUBLE;

	SET v_area = 3.142 * v_radius * v_radius;
	SELECT 2 * 3.142 * v_radius INTO v_circum;

	SELECT v_radius AS radius, v_area AS area, v_circum AS circum;
END;
$$

DELIMITER ;

CALL sp_circle();


-- Parameterized Stored Procedure
DELIMITER $$

CREATE PROCEDURE personlist()
@p_id INT = 1,
@p_name VARCHAR(50) = 'John Abraham'
AS
  BEGIN
    SELECT * FROM personal WHERE id = @p_id
    SELECT * FROM personal WHERE name = @p_name
  END $$

DELIMITER ;

EXECUTE personlist 4, 'Anil Kapoor';

-- Example 2
-- calculate area and perimeter of a square and put result into results table.
-- side of square should be taken as procedure param.

DROP PROCEDURE IF EXISTS sp_square;

DELIMITER $$

CREATE PROCEDURE sp_square(v_side DOUBLE)
BEGIN
	DECLARE v_area DOUBLE;
	DECLARE v_peri DOUBLE;
	DECLARE v_output VARCHAR(80);

	SET v_area = v_side * v_side;
	SET v_peri = 4 * v_side;
	SET v_output = CONCAT('side=', v_side, ', area=', v_area, ', peri=', v_peri);

	INSERT INTO result VALUES(1, v_output);
END;
$$

DELIMITER ;

-- CALL sp_square(10);
-- SELECT * FROM result;
-- CALL sp_square(20);
-- SELECT * FROM result;
-- CALL sp_square(30);
-- SELECT * FROM result;

-- named variables
EXECUTE personlist @p_name = 'Anil Kapoor', @p_id = 4;

-- Example 3
-- perform addition of even numbers in given range and display result on cli.
-- range will be given as argument.

DELIMITER $$

CREATE PROCEDURE sp_evenadd(v_low INT, v_high INT)
BEGIN
	DECLARE v_i INT;
	DECLARE v_sum INT DEFAULT 0;

	SET v_i = v_low; -- initialization
	WHILE v_i <= v_high DO -- condition

		IF v_i % 2 = 0 THEN
			SET v_sum = v_sum + v_i;
		END IF;

		SET v_i = v_i + 1; -- modification

	END WHILE;

	SELECT v_low AS low, v_high AS high, v_sum AS result;
END;
$$

DELIMITER ;

-- CALL sp_evenadd(1, 10);

-- Example 4
-- take a number as argument. check if it is prime or not.
-- put result into results table.

DELIMITER $$

CREATE PROCEDURE sp_prime(v_num INT)
BEGIN
  DECLARE v_i INT DEFAULT 2;

  prime: LOOP
    IF v_i >= v_num THEN
      INSERT INTO result VALUES (v_num, 'Prime');
      LEAVE prime;
    END IF;

    IF v_num % v_i = 0 THEN
      INSERT INTO result VALUES (v_num, 'Not Prime');
      LEAVE prime;
    END IF;

    SET v_i = v_i + 1;
  END LOOP;
END;
$$

DELIMITER ;

-- TRUNCATE result;
-- CALL sp_prime(7);
-- CALL sp_prime(49);
-- CALL sp_prime(81);
-- CALL sp_prime(83);
-- CALL sp_prime(51);
-- CALL sp_prime(101);
-- SELECT * FROM result;

-- Parameterized Stored Procedure
DELIMITER $$

CREATE PROC addDigit
@num1 INT,
@num2 INT,
@result INT OUTPUT
AS
BEGIN
    SET @result = @num1 + @num2;
END $$

DELIMITER ;

DECLARE @EId INT
EXECUTE addDigit 2, 2, @EId OUTPUT;

SELECT @EId;


-- Example 5
-- write a SP to calculate square of a number.
-- number will be given as parameter.
-- return must be returned via paramter.

DELIMITER $$

CREATE PROCEDURE sp_sqr1(IN v_n INT, OUT v_res INT)
BEGIN
  SET v_res = v_n * v_n;
END;
$$

DELIMITER ;

-- SET @v_num = 5;
-- SET @v_result = 0;
-- CALL sp_sqr1(@v_num, @v_result);
-- SELECT @v_num AS number, @v_result AS result;

-- Example 6
-- write a SP to calculate square of a number.
-- number will be given as parameter and result should be returned in same parameter.

DELIMITER $$

CREATE PROCEDURE sp_sqr2(INOUT v_num INT)
BEGIN
	SET v_num = v_num * v_num;
END;
$$

DELIMITER ;

-- SET @v_num = 6;
-- CALL sp_sqr2(@v_num);

-- //////////////////////////
-- Triggers

-- CREATE TRIGGER
CREATE TRIGGER trig_name
AFTER|BEFORE dml_op ON table
FOR EACH ROW
BEGIN
-- body;
-- use OLD & NEW keywords
-- to access old/new rows.
-- INSERT triggers – NEW rows.
-- DELETE triggers – OLD rows.
END;

-- SHOW TRIGGERS
SHOW TRIGGERS FROM db_name;

-- DROP TRIGGER
DROP TRIGGER trig_name;

CREATE TABLE accounts(id INT, type CHAR(20), balance DOUBLE);

INSERT INTO accounts VALUES (1, 'Saving', 10000),
(2, 'Saving', 2000),
(3, 'Current', 25000),
(4, 'Saving', 7000);

CREATE TABLE transactions(accid INT, type CHAR(20), tim DATETIME, amount DOUBLE);

-- Trigger

DELIMITER $$

CREATE TRIGGER trig_updatebalance
AFTER INSERT ON transactions
FOR EACH ROW
BEGIN
    DECLARE v_accid INT DEFAULT NEW.accid;
    DECLARE v_amount DOUBLE DEFAULT NEW.amount;
    DECLARE v_type CHAR(20) DEFAULT NEW.type;

    IF v_type = 'DEPOSIT' THEN
        UPDATE accounts SET balance = balance + v_amount WHERE id = v_accid;
    ELSE
        UPDATE accounts SET balance = balance - v_amount WHERE id = v_accid;
    END IF;
END;
$$

DELIMITER ;


SELECT * FROM accounts;
INSERT INTO transactions VALUES (1, 'WITHDRAW', NOW(), 2000);
SELECT * FROM accounts;
INSERT INTO transactions VALUES (2, 'DEPOSIT', NOW(), 500);
SELECT * FROM accounts;
SELECT * FROM transactions;

SHOW TRIGGERS FROM gbs_practice;

```
