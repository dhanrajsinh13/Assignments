---
title: -- PL/SQL Exercises (Unit-2 to 4)
created: 2025-03-15T13:41:32+05:30
lastUpdated: 2025-03-15T13:42:29+05:30
category: 
---

-- PL/SQL Exercises (Unit-2 to 4)

-- 1. Calculate the square of a number and display on screen
DECLARE 
    num NUMBER := 5; 
    square NUMBER;
BEGIN 
    square := num * num;
    DBMS_OUTPUT.PUT_LINE('Square of ' || num || ' is ' || square);
END;
/

-- 2. Display information of a given student
DECLARE 
    v_sno Student.sno%TYPE;
    v_sname Student.sname%TYPE;
    v_address Student.address%TYPE;
    v_city Student.city%TYPE;
BEGIN 
    SELECT sno, sname, address, city INTO v_sno, v_sname, v_address, v_city FROM Student WHERE sno = 1;
    DBMS_OUTPUT.PUT_LINE('Student No: ' || v_sno || ', Name: ' || v_sname || ', Address: ' || v_address || ', City: ' || v_city);
END;
/

-- 3. Raise the salary by 20% for a given employee
DECLARE 
    v_eno Emp_Salary.eno%TYPE := 101;
BEGIN 
    UPDATE Emp_Salary SET salary = salary * 1.2 WHERE eno = v_eno;
    COMMIT;
END;
/

-- 4. Update commission if NULL else raise by 25%
BEGIN 
    UPDATE Emp SET commission = CASE WHEN commission IS NULL THEN 0.1 ELSE commission * 1.25 END;
    COMMIT;
END;
/

-- 5. Procedure to calculate incentive and check if record updated
CREATE OR REPLACE PROCEDURE CalcIncentive (p_eno NUMBER) AS
    v_count NUMBER;
BEGIN 
    UPDATE Emp SET target_status = 'Achieved' WHERE eno = p_eno;
    v_count := SQL%ROWCOUNT;
    IF v_count > 0 THEN
        DBMS_OUTPUT.PUT_LINE('Record updated successfully.');
    ELSE
        DBMS_OUTPUT.PUT_LINE('No record found.');
    END IF;
END;
/

-- 6. Prepare Net Salary
DECLARE 
    v_eno Salary.eno%TYPE := 101;
    v_basic Salary.basic%TYPE;
    v_da NUMBER;
    v_hra NUMBER := 500;
    v_it NUMBER;
    v_total_allowance NUMBER;
    v_total_deduction NUMBER;
    v_netpay NUMBER;
BEGIN 
    SELECT basic INTO v_basic FROM Salary WHERE eno = v_eno;
    v_da := v_basic * 0.59;
    v_it := v_basic * 0.02;
    v_total_allowance := v_basic + v_da + v_hra;
    v_total_deduction := v_it;
    v_netpay := v_total_allowance - v_total_deduction;
    
    INSERT INTO Net_salary VALUES (v_eno, v_total_allowance, v_total_deduction, v_netpay);
    COMMIT;
END;
/

-- 7. Print prime numbers between 1 to 50
DECLARE 
    v_num NUMBER := 2;
    v_is_prime BOOLEAN;
BEGIN 
    WHILE v_num <= 50 LOOP
        v_is_prime := TRUE;
        FOR i IN 2..SQRT(v_num) LOOP
            IF v_num MOD i = 0 THEN
                v_is_prime := FALSE;
                EXIT;
            END IF;
        END LOOP;
        IF v_is_prime THEN
            DBMS_OUTPUT.PUT_LINE(v_num);
        END IF;
        v_num := v_num + 1;
    END LOOP;
END;
/

-- PL/SQL Exercises (Unit-2 to 4) Continued

-- 8. Insert records from one table to another
BEGIN
    INSERT INTO Emp_Backup (eno, ename, city, salary)
    SELECT eno, ename, city, salary FROM Emp;
    COMMIT;
END;
/

-- 9. Display 5th and 10th employees using Control Structures
DECLARE
    CURSOR emp_cursor IS SELECT eno, ename FROM Emp;
    v_eno Emp.eno%TYPE;
    v_ename Emp.ename%TYPE;
    v_count NUMBER := 0;
BEGIN
    OPEN emp_cursor;
    LOOP
        FETCH emp_cursor INTO v_eno, v_ename;
        EXIT WHEN emp_cursor%NOTFOUND;
        v_count := v_count + 1;
        IF v_count = 5 OR v_count = 10 THEN
            DBMS_OUTPUT.PUT_LINE('Employee: ' || v_eno || ' - ' || v_ename);
        END IF;
    END LOOP;
    CLOSE emp_cursor;
END;
/

-- 10. Display week day of the given date using CASE statement
DECLARE
    v_date DATE := SYSDATE;
    v_day VARCHAR2(20);
BEGIN
    SELECT CASE TO_CHAR(v_date, 'D')
        WHEN '1' THEN 'Sunday'
        WHEN '2' THEN 'Monday'
        WHEN '3' THEN 'Tuesday'
        WHEN '4' THEN 'Wednesday'
        WHEN '5' THEN 'Thursday'
        WHEN '6' THEN 'Friday'
        WHEN '7' THEN 'Saturday'
    END INTO v_day FROM dual;
    DBMS_OUTPUT.PUT_LINE('Day of the week: ' || v_day);
END;
/

-- 11. Implicit cursor to delete employee record
DECLARE
    v_eno Emp.eno%TYPE := 101;
BEGIN
    DELETE FROM Emp WHERE eno = v_eno;
    IF SQL%ROWCOUNT > 0 THEN
        DBMS_OUTPUT.PUT_LINE('Record deleted successfully.');
    ELSE
        DBMS_OUTPUT.PUT_LINE('No record found.');
    END IF;
END;
/

-- 12. Cursor to display first five student records
DECLARE
    CURSOR stud_cursor IS SELECT sno, sname, city, salary FROM Student;
    v_sno Student.sno%TYPE;
    v_sname Student.sname%TYPE;
    v_city Student.city%TYPE;
    v_salary Student.salary%TYPE;
    v_count NUMBER := 0;
BEGIN
    OPEN stud_cursor;
    LOOP
        FETCH stud_cursor INTO v_sno, v_sname, v_city, v_salary;
        EXIT WHEN stud_cursor%NOTFOUND OR v_count = 5;
        DBMS_OUTPUT.PUT_LINE(v_sno || ', ' || v_sname || ', ' || v_city || ', ' || v_salary);
        v_count := v_count + 1;
    END LOOP;
    CLOSE stud_cursor;
END;
/

-- 13. Explicit cursor to print employees with salary above average
DECLARE
    CURSOR emp_cursor IS SELECT ename, job, salary FROM Emp WHERE salary > (SELECT AVG(salary) FROM Emp);
    v_ename Emp.ename%TYPE;
    v_job Emp.job%TYPE;
    v_salary Emp.salary%TYPE;
BEGIN
    OPEN emp_cursor;
    LOOP
        FETCH emp_cursor INTO v_ename, v_job, v_salary;
        EXIT WHEN emp_cursor%NOTFOUND;
        DBMS_OUTPUT.PUT_LINE('Employee: ' || v_ename || ', Job: ' || v_job || ', Salary: ' || v_salary);
    END LOOP;
    CLOSE emp_cursor;
END;
/

-- 14. Stored Procedure to change manager ID to highest paid employee
CREATE OR REPLACE PROCEDURE Change_Manager (p_dept_id NUMBER) AS
    v_highest_eno NUMBER;
BEGIN
    SELECT eno INTO v_highest_eno FROM Emp WHERE salary = (SELECT MAX(salary) FROM Emp WHERE dept_id = p_dept_id) AND dept_id = p_dept_id;
    UPDATE Department SET manager_id = v_highest_eno WHERE dept_id = p_dept_id;
    COMMIT;
END;
/

-- PL/SQL Exercises (Unit-2 to 4) Continued

-- 15. Procedure to check if a year is a leap year
CREATE OR REPLACE PROCEDURE Check_Leap_Year(p_year NUMBER) AS
    v_result VARCHAR2(20);
BEGIN
    IF (MOD(p_year, 4) = 0 AND MOD(p_year, 100) <> 0) OR MOD(p_year, 400) = 0 THEN
        v_result := 'Leap Year';
    ELSE
        v_result := 'Not a Leap Year';
    END IF;
    DBMS_OUTPUT.PUT_LINE(v_result);
END;
/

-- 16. Procedure to display multiplication table
CREATE OR REPLACE PROCEDURE Multiplication_Table(p_number NUMBER) AS
    v_result NUMBER;
BEGIN
    FOR i IN 1..10 LOOP
        v_result := p_number * i;
        DBMS_OUTPUT.PUT_LINE(p_number || ' x ' || i || ' = ' || v_result);
    END LOOP;
END;
/

-- 17. Procedure to insert a new employee
CREATE OR REPLACE PROCEDURE Newemp_Proc(p_eno NUMBER, p_ename VARCHAR2, p_sal NUMBER) AS
BEGIN
    INSERT INTO Emp (eno, ename, salary) VALUES (p_eno, p_ename, p_sal);
    COMMIT;
    DBMS_OUTPUT.PUT_LINE('New employee inserted.');
END;
/

-- 18. Procedure to return employee details
CREATE OR REPLACE PROCEDURE Get_Employee_Info(p_eno NUMBER) AS
    v_ename Emp.ename%TYPE;
    v_city Emp.city%TYPE;
    v_salary Emp.salary%TYPE;
BEGIN
    SELECT ename, city, salary INTO v_ename, v_city, v_salary FROM Emp WHERE eno = p_eno;
    DBMS_OUTPUT.PUT_LINE('Employee: ' || v_ename || ', City: ' || v_city || ', Salary: ' || v_salary);
END;
/

-- 19. Procedure to display all employees using a cursor
CREATE OR REPLACE PROCEDURE DisplayEmp_Proc AS
    CURSOR emp_cursor IS SELECT eno, ename FROM Emp;
    v_eno Emp.eno%TYPE;
    v_ename Emp.ename%TYPE;
BEGIN
    OPEN emp_cursor;
    LOOP
        FETCH emp_cursor INTO v_eno, v_ename;
        EXIT WHEN emp_cursor%NOTFOUND;
        DBMS_OUTPUT.PUT_LINE('Employee: ' || v_eno || ' - ' || v_ename);
    END LOOP;
    CLOSE emp_cursor;
END;
/

-- 20. Function to check if a number is prime
CREATE OR REPLACE FUNCTION Is_Prime(p_num NUMBER) RETURN VARCHAR2 AS
    v_flag BOOLEAN := TRUE;
BEGIN
    IF p_num < 2 THEN RETURN 'Not Prime'; END IF;
    FOR i IN 2..SQRT(p_num) LOOP
        IF MOD(p_num, i) = 0 THEN
            v_flag := FALSE;
            EXIT;
        END IF;
    END LOOP;
    RETURN CASE WHEN v_flag THEN 'Prime' ELSE 'Not Prime' END;
END;
/

-- 21. Function to reverse a string
CREATE OR REPLACE FUNCTION Reverse_String(p_str VARCHAR2) RETURN VARCHAR2 AS
    v_reversed VARCHAR2(100);
BEGIN
    v_reversed := REVERSE(p_str);
    RETURN v_reversed;
END;
/

-- 22. Function to return employee salary
CREATE OR REPLACE FUNCTION Get_Salary(p_eno NUMBER) RETURN NUMBER AS
    v_salary Emp.salary%TYPE;
BEGIN
    SELECT salary INTO v_salary FROM Emp WHERE eno = p_eno;
    RETURN v_salary;
END;
/

-- 23. Function to return department manager name
CREATE OR REPLACE FUNCTION Get_Manager(p_dept_id NUMBER) RETURN VARCHAR2 AS
    v_manager VARCHAR2(100);
BEGIN
    SELECT ename INTO v_manager FROM Emp WHERE eno = (SELECT manager_id FROM Department WHERE dept_id = p_dept_id);
    RETURN v_manager;
END;
/

-- 24. Add exception handling to Get_Salary function
CREATE OR REPLACE FUNCTION Get_Salary_Handled(p_eno NUMBER) RETURN NUMBER AS
    v_salary Emp.salary%TYPE;
BEGIN
    SELECT salary INTO v_salary FROM Emp WHERE eno = p_eno;
    RETURN v_salary;
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Error: Employee not found');
        RETURN NULL;
END;
/

-- 25. Trigger to convert name to uppercase on insert
CREATE OR REPLACE TRIGGER Emp_Name_Uppercase
BEFORE INSERT ON Emp
FOR EACH ROW
BEGIN
    :NEW.ename := UPPER(:NEW.ename);
END;
/

-- 26. Trigger to prevent modifications before 6 AM and after 10 PM
CREATE OR REPLACE TRIGGER Restrict_Modifications
BEFORE INSERT OR UPDATE OR DELETE ON Emp
BEGIN
    IF TO_CHAR(SYSDATE, 'HH24') NOT BETWEEN 6 AND 22 THEN
        RAISE_APPLICATION_ERROR(-20001, 'Modifications allowed only between 6 AM and 10 PM');
    END IF;
END;
/

-- 27. Trigger to ensure salary is not decreased
CREATE OR REPLACE TRIGGER Prevent_Salary_Decrease
BEFORE UPDATE ON Emp
FOR EACH ROW
BEGIN
    IF :NEW.salary < :OLD.salary THEN
        RAISE_APPLICATION_ERROR(-20002, 'Salary cannot be decreased');
    END IF;
END;
/

-- 28. Trigger to ensure mark is not zero or negative
CREATE OR REPLACE TRIGGER Validate_Mark
BEFORE INSERT OR UPDATE ON Student
FOR EACH ROW
BEGIN
    IF :NEW.mark <= 0 THEN
        RAISE_APPLICATION_ERROR(-20003, 'Mark must be positive');
    END IF;
END;
/

-- 29. Trigger to ensure student_id starts with 'M'
CREATE OR REPLACE TRIGGER Validate_Student_ID
BEFORE INSERT OR UPDATE ON Student
FOR EACH ROW
BEGIN
    IF SUBSTR(:NEW.sno, 1, 1) <> 'M' THEN
        RAISE_APPLICATION_ERROR(-20004, 'Student ID must start with M');
    END IF;
END;
/

-- All exercises completed

