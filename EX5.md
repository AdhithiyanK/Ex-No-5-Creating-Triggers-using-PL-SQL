# Ex. No: 5 Creating Triggers using PL/SQL
## DATE:
### AIM: To create a Trigger using PL/SQL.

### Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
3. Create a trigger named as log_salary-update.
4. Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
5. End the trigger.
6. Update the salary of an employee in employee table.
7. Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
8. Display the employee table, salary_log table.

### Program:
```
CREATE TABLE employed(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);

CREATE TABLE sal_log (
  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
```
### Create employee table
![T1](https://github.com/AdhithiyanK/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/121029258/d25cdaee-e22f-4757-80e4-c2c49adf590f)


### Create salary_log table
![T2](https://github.com/AdhithiyanK/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/121029258/e82b9c5a-2138-4476-b321-ab887e37783f)

### PLSQL Trigger code
```
->Create the trigger
Create the trigger
CREATE OR REPLACE TRIGGER log_sal_update
BEFORE UPDATE ON employed
FOR EACH ROW
BEGIN
  IF :OLD.salary != :NEW.salary THEN
    INSERT INTO sal_log (empid, empname, old_salary, new_salary, update_date)
    VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
  END IF;
END;
/
->Update the salary of an employee
UPDATE employed
SET salary = 60000
WHERE empid = 1;
->Display the employee table
SELECT * FROM employed;

->Display the salary_log table
SELECT * FROM sal_log;
```
### Output:

![T3](https://github.com/AdhithiyanK/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/121029258/bd5f488b-9cba-4d8b-a781-23d36d219b22)

### Result:
The program has been implemented successfully.
