-- 1. Write a PL/SQL Block to calculate the square of a number and display on the screen
```
DECLARE
    num NUMBER := 5;
    square NUMBER;
BEGIN
    square := num * num;
    DBMS_OUTPUT.PUT_LINE('Square of ' || num || ' is ' || square);
END;
/

```
-- 2. Write a PL/SQL block to display student information
```
DECLARE
    v_sno Student.sno%TYPE;
    v_sname Student.sname%TYPE;
    v_address Student.address%TYPE;
    v_city Student.city%TYPE;
BEGIN
    SELECT sno, sname, address, city INTO v_sno, v_sname, v_address, v_city FROM Student WHERE sno = 101;
    DBMS_OUTPUT.PUT_LINE('Student No: ' || v_sno || ', Name: ' || v_sname || ', Address: ' || v_address || ', City: ' || v_city);
END;
/

```
-- 3. Write a PL/SQL block to raise employee salary by 20%
```
DECLARE
    v_salary Emp_Salary.salary%TYPE;
BEGIN
    SELECT salary INTO v_salary FROM Emp_Salary WHERE eno = 1;
    v_salary := v_salary * 1.2;
    UPDATE Emp_Salary SET salary = v_salary WHERE eno = 1;
    DBMS_OUTPUT.PUT_LINE('Salary updated to ' || v_salary);
END;
/
```

-- 4. Update commission of employees
```
DECLARE
    v_commission Emp.commission%TYPE;
BEGIN
    FOR emp IN (SELECT eno, commission FROM Emp) LOOP
        IF emp.commission IS NULL THEN
            UPDATE Emp SET commission = 0.1 WHERE eno = emp.eno;
        ELSE
            UPDATE Emp SET commission = emp.commission * 1.25 WHERE eno = emp.eno;
        END IF;
    END LOOP;
    COMMIT;
    DBMS_OUTPUT.PUT_LINE('Commissions Updated');
END;
/
```

-- 5. Procedure to calculate incentive
```
CREATE OR REPLACE PROCEDURE Calculate_Incentive (p_eno IN Emp.eno%TYPE) AS
    v_target_status Emp.target_status%TYPE;
BEGIN
    SELECT target_status INTO v_target_status FROM Emp WHERE eno = p_eno;
    IF v_target_status = 'Achieved' THEN
        DBMS_OUTPUT.PUT_LINE('Incentive granted. Record updated.');
    ELSE
        DBMS_OUTPUT.PUT_LINE('No incentive as target not achieved.');
    END IF;
END;
/

```
-- 6. Calculate Net Salary
```
DECLARE
    v_basic Salary.basic%TYPE;
    v_da NUMBER;
    v_hra NUMBER := 500;
    v_it NUMBER;
    v_total_allowance NUMBER;
    v_total_deduction NUMBER;
    v_netpay NUMBER;
BEGIN
    SELECT basic INTO v_basic FROM Salary WHERE eno = 1;
    v_da := v_basic * 0.59;
    v_it := v_basic * 0.02;
    v_total_allowance := v_basic + v_da + v_hra;
    v_total_deduction := v_it;
    v_netpay := v_total_allowance - v_total_deduction;
    DBMS_OUTPUT.PUT_LINE('Net Salary: ' || v_netpay);
END;
/
```

-- 7. Print prime numbers between 1 to 50
```
DECLARE
    v_num NUMBER;
    v_prime BOOLEAN;
BEGIN
    FOR v_num IN 2..50 LOOP
        v_prime := TRUE;
        FOR i IN 2..SQRT(v_num) LOOP
            IF v_num MOD i = 0 THEN
                v_prime := FALSE;
                EXIT;
            END IF;
        END LOOP;
        IF v_prime THEN
            DBMS_OUTPUT.PUT_LINE(v_num);
        END IF;
    END LOOP;
END;
/
```

-- 8. Insert records from one table to another
```
INSERT INTO New_Table (col1, col2) SELECT col1, col2 FROM Old_Table;
COMMIT;

```
-- 9. Display weekday of given date
```
DECLARE
    v_date DATE := '15-MAR-2025';
    v_day VARCHAR2(20);
BEGIN
    SELECT TO_CHAR(v_date, 'DAY') INTO v_day FROM DUAL;
    DBMS_OUTPUT.PUT_LINE('Weekday: ' || v_day);
END;
/
```

-- 10. Implicit cursor to delete employee
```
DECLARE
    v_eno Emp.eno%TYPE := 3;
BEGIN
    DELETE FROM Emp WHERE eno = v_eno;
    IF SQL%FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Employee deleted.');
    ELSE
        DBMS_OUTPUT.PUT_LINE('Employee not found.');
    END IF;
END;
/
```

-- 11. Explicit cursor to display employees with above average salary
```
DECLARE
    CURSOR emp_cur IS SELECT ename, job, salary FROM Emp WHERE salary > (SELECT AVG(salary) FROM Emp);
    v_ename Emp.ename%TYPE;
    v_job Emp.job%TYPE;
    v_salary Emp.salary%TYPE;
BEGIN
    OPEN emp_cur;
    LOOP
        FETCH emp_cur INTO v_ename, v_job, v_salary;
        EXIT WHEN emp_cur%NOTFOUND;
        DBMS_OUTPUT.PUT_LINE(v_ename || ' - ' || v_job || ' - ' || v_salary);
    END LOOP;
    CLOSE emp_cur;
END;
/
```

-- 12. Stored procedure to update manager ID for highest salary employee in a department
```
CREATE OR REPLACE PROCEDURE Update_Manager (p_dept_id IN Department.dept_id%TYPE) AS
    v_highest_salary Emp.salary%TYPE;
    v_highest_emp Emp.eno%TYPE;
BEGIN
    SELECT eno, salary INTO v_highest_emp, v_highest_salary FROM Emp WHERE dept_id = p_dept_id ORDER BY salary DESC FETCH FIRST 1 ROW ONLY;
    UPDATE Department SET manager_id = v_highest_emp WHERE dept_id = p_dept_id;
    DBMS_OUTPUT.PUT_LINE('Manager updated to employee: ' || v_highest_emp);
END;
/
```

-- 13. Trigger to capitalize names on insert
```
CREATE OR REPLACE TRIGGER Capitalize_Name
BEFORE INSERT ON Emp
FOR EACH ROW
BEGIN
    :NEW.ename := UPPER(:NEW.ename);
END;
/
```

-- 14. Trigger to prevent salary decrease
```
CREATE OR REPLACE TRIGGER Prevent_Salary_Decrease
BEFORE UPDATE OF salary ON Emp
FOR EACH ROW
BEGIN
    IF :NEW.salary < :OLD.salary THEN
        RAISE_APPLICATION_ERROR(-20001, 'Salary cannot be decreased!');
    END IF;
END;
/
```

-- 15. Procedure to check if a year is a leap year
```
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
```

-- 16. Procedure to display multiplication table
```
CREATE OR REPLACE PROCEDURE Multiplication_Table(p_number NUMBER) AS
    v_result NUMBER;
BEGIN
    FOR i IN 1..10 LOOP
        v_result := p_number * i;
        DBMS_OUTPUT.PUT_LINE(p_number || ' x ' || i || ' = ' || v_result);
    END LOOP;
END;
/
```

-- 17. Procedure to insert a new employee
```
CREATE OR REPLACE PROCEDURE Newemp_Proc(p_eno NUMBER, p_ename VARCHAR2, p_sal NUMBER) AS
BEGIN
    INSERT INTO Emp (eno, ename, salary) VALUES (p_eno, p_ename, p_sal);
    COMMIT;
    DBMS_OUTPUT.PUT_LINE('New employee inserted.');
END;
/
```

-- 18. Procedure to return employee details
```
CREATE OR REPLACE PROCEDURE Get_Employee_Info(p_eno NUMBER) AS
    v_ename Emp.ename%TYPE;
    v_city Emp.city%TYPE;
    v_salary Emp.salary%TYPE;
BEGIN
    SELECT ename, city, salary INTO v_ename, v_city, v_salary FROM Emp WHERE eno = p_eno;
    DBMS_OUTPUT.PUT_LINE('Employee: ' || v_ename || ', City: ' || v_city || ', Salary: ' || v_salary);
END;
/

```
-- 19. Procedure to display all employees using a cursor
```
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
```

-- 20. Function to check if a number is prime
```
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
```

-- 21. Function to reverse a string
```
CREATE OR REPLACE FUNCTION Reverse_String(p_str VARCHAR2) RETURN VARCHAR2 AS
    v_reversed VARCHAR2(100);
BEGIN
    v_reversed := REVERSE(p_str);
    RETURN v_reversed;
END;
/
```

-- 22. Function to return employee salary
```
CREATE OR REPLACE FUNCTION Get_Salary(p_eno NUMBER) RETURN NUMBER AS
    v_salary Emp.salary%TYPE;
BEGIN
    SELECT salary INTO v_salary FROM Emp WHERE eno = p_eno;
    RETURN v_salary;
END;
/
```

-- 23. Function to return department manager name
```
CREATE OR REPLACE FUNCTION Get_Manager(p_dept_id NUMBER) RETURN VARCHAR2 AS
    v_manager VARCHAR2(100);
BEGIN
    SELECT ename INTO v_manager FROM Emp WHERE eno = (SELECT manager_id FROM Department WHERE dept_id = p_dept_id);
    RETURN v_manager;
END;
/
```

-- 24. Add exception handling to Get_Salary function
```
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
```

-- 25. Trigger to convert name to uppercase on insert
```
CREATE OR REPLACE TRIGGER Emp_Name_Uppercase
BEFORE INSERT ON Emp
FOR EACH ROW
BEGIN
    :NEW.ename := UPPER(:NEW.ename);
END;
/
```

-- 26. Trigger to prevent modifications before 6 AM and after 10 PM
```
CREATE OR REPLACE TRIGGER Restrict_Modifications
BEFORE INSERT OR UPDATE OR DELETE ON Emp
BEGIN
    IF TO_CHAR(SYSDATE, 'HH24') NOT BETWEEN 6 AND 22 THEN
        RAISE_APPLICATION_ERROR(-20001, 'Modifications allowed only between 6 AM and 10 PM');
    END IF;
END;
/
```

-- 27. Trigger to ensure salary is not decreased
```
CREATE OR REPLACE TRIGGER Prevent_Salary_Decrease
BEFORE UPDATE ON Emp
FOR EACH ROW
BEGIN
    IF :NEW.salary < :OLD.salary THEN
        RAISE_APPLICATION_ERROR(-20002, 'Salary cannot be decreased');
    END IF;
END;
/
```

-- 28. Trigger to ensure mark is not zero or negative
```
CREATE OR REPLACE TRIGGER Validate_Mark
BEFORE INSERT OR UPDATE ON Student
FOR EACH ROW
BEGIN
    IF :NEW.mark <= 0 THEN
        RAISE_APPLICATION_ERROR(-20003, 'Mark must be positive');
    END IF;
END;
/
```

-- 29. Trigger to ensure student_id starts with 'M'
```
CREATE OR REPLACE TRIGGER Validate_Student_ID
BEFORE INSERT OR UPDATE ON Student
FOR EACH ROW
BEGIN
    IF SUBSTR(:NEW.sno, 1, 1) <> 'M' THEN
        RAISE_APPLICATION_ERROR(-20004, 'Student ID must start with M');
    END IF;
END;
/

```
-- All exercises completed
