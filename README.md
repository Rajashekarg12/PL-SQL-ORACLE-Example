# PL-SQL-ORACLE-Example

## Block

    DECLARE
      Declartion statement
    BEGIN 
      Executable statement
    Exceptions
      Exception handling statement
    END;

## Variable

#### Declaring variables

    variablename datatype;

...

    SET SERVEROUTPUT ON;

    DECLARE 
        vString VARCHAR2(20);
        vNumber NUMBER(20);
    BEGIN
       NULL;
    END;

####  Variable checking

    SET SERVEROUTPUT ON;

    DECLARE 
        vString VARCHAR2(20) NOT NULL;
        vNumber NUMBER(20) NOT NULL;
    BEGIN
       NULL;
    END;

#### Variables with initial or default value

    SET SERVEROUTPUT ON;

    DECLARE 
        vString VARCHAR2(20) := 'Hello world';
        vNumber NUMBER(20) := 2020;
    BEGIN
        dbms_output.put_line(vString);
        dbms_output.put_line(vNumber);
    END;
    /
     DECLARE 
        vString VARCHAR2(20) DEFAULT 'Hello world';
        vNumber NUMBER(20) DEFAULT 2020;
    BEGIN
        dbms_output.put_line(vString);
        dbms_output.put_line(vNumber);
    END;

#### Variables constants

you must initialize a constants at its declaration 

    SET SERVEROUTPUT ON;

    DECLARE 
        vPI CONSTANT NUMBER(7,6) := 3.141592;
        vMsg CONSTANT NVARCHAR2(20) := 'This is constants';
    BEGIN
        dbms_output.put_line(vPI);
        dbms_output.put_line(vMsg);
    END;
    /
    DECLARE 
        vPI CONSTANT NUMBER(7,6) DEFAULT 3.141592;
        vMsg CONSTANT NVARCHAR2(20) DEFAULT 'This is constants';
    BEGIN
        dbms_output.put_line(vPI);
        dbms_output.put_line(vMsg);
    END;
  

## Data type

    

#### %TYPE

    SET SERVEROUTPUT ON;

    DECLARE 
        vUserId NUMBER(20,0);
        vUsername VARCHAR2(100);
        vPassword VARCHAR2(200);
        vEnabled NUMBER(1,0);
        vCreateDate TIMESTAMP(6);
        vAcountExpiredDate DATE;
    BEGIN
        SELECT 
            USER_ID, 
            username,
            password, 
            ENABLED, 
            CREATE_DATE, 
            ACCOUNT_EXPIRED_DATE
            into 
            vUserId, 
            vUsername, 
            vPassword, 
            vEnabled, 
            vCreateDate, 
            vAcountExpiredDate
        FROM USERS WHERE username = 'tirmizee';
        dbms_output.put_line(vUserId);
        dbms_output.put_line(vUsername);
        dbms_output.put_line(vPassword);
        dbms_output.put_line(vEnabled);
        dbms_output.put_line(vCreateDate);
        dbms_output.put_line(vAcountExpiredDate);
    END;
    /
    DECLARE 
        vUserId USERS.USER_ID%TYPE;
        vUsername USERS.username%TYPE;
        vPassword USERS.password%TYPE;
        vEnabled USERS.ENABLED%TYPE;
        vCreateDate USERS.CREATE_DATE%TYPE;
        vAcountExpiredDate USERS.ACCOUNT_EXPIRED_DATE%TYPE;
    BEGIN
        SELECT 
            USER_ID, 
            username,
            password, 
            ENABLED, 
            CREATE_DATE, 
            ACCOUNT_EXPIRED_DATE
            into 
            vUserId, 
            vUsername, 
            vPassword, 
            vEnabled, 
            vCreateDate, 
            vAcountExpiredDate
        FROM USERS WHERE username = 'tirmizee';
        dbms_output.put_line(vUserId);
        dbms_output.put_line(vUsername);
        dbms_output.put_line(vPassword);
        dbms_output.put_line(vEnabled);
        dbms_output.put_line(vCreateDate);
        dbms_output.put_line(vAcountExpiredDate);
    END;

#### %ROWTYPE

    SET SERVEROUTPUT ON;

    DECLARE 
        vEmpId NUMBER(19,0);
        vEmpCode VARCHAR2(20 BYTE);
        vEmpFirstName VARCHAR2(100 BYTE);
        vEmpLastName VARCHAR2(100 BYTE);
        vManagerId NUMBER(19,0);
    BEGIN
        SELECT * INTO
           vEmpId,
           vEmpCode,
           vEmpFirstName,
           vEmpLastName,
           vManagerId
        FROM employee WHERE EMP_ID = 1;
        dbms_output.put_line(vEmpId);
        dbms_output.put_line(vEmpCode);
        dbms_output.put_line(vEmpFirstName);
        dbms_output.put_line(vEmpLastName);
        dbms_output.put_line(vManagerId);
    END;
    /
    DECLARE 
        tempEmp employee%ROWTYPE;
    BEGIN
        SELECT * INTO tempEmp FROM employee WHERE EMP_ID = 1;
        dbms_output.put_line(tempEmp.EMP_ID);
        dbms_output.put_line(tempEmp.EMP_CODE);
        dbms_output.put_line(tempEmp.EMP_FIRST_NAME);
        dbms_output.put_line(tempEmp.EMP_LAST_NAME);
        dbms_output.put_line(tempEmp.MANAGER_ID);
    END;


## Select into

    SET SERVEROUTPUT ON;

    DECLARE 
        vString VARCHAR2(200);
    BEGIN
       SELECT password into vString from USERS WHERE username = 'tirmizee';
       dbms_output.put_line(vString);
    END;
    /
    DECLARE 
        vString VARCHAR2(200);
        vNumber NUMBER(1,0);
    BEGIN
        SELECT 
            password, 
            enabled 
            into 
            vString, 
            vNumber  
        from USERS WHERE username = 'tirmizee';
        dbms_output.put_line(vString);
        dbms_output.put_line(vNumber);
    END;

## Conditional Statements

#### IF - THEN

    IF condition THEN
        statement;
        ...
    END IF;

...

    SET SERVEROUTPU ON;

    DECLARE
        vAge number(2,0) := 26;
    BEGIN
        IF vAge = 26 THEN
            dbms_output.put_line('Age is ' || vAge);
            dbms_output.put_line('Age is ' || vAge);
        END IF;
        dbms_output.put_line('Finish');
    END;
    /
    DECLARE
        vFirstName VARCHAR2(100) := 'Pratya';
        vLastName VARCHAR2(100) := 'Yeekhaday';
    BEGIN
        IF vFirstName = 'Pratya' AND vLastName = 'Yeekhaday' THEN
            dbms_output.put_line('Fullname is ' || vFirstName || ' ' ||vlastname);
        END IF;
        dbms_output.put_line('Finish');
    END;

#### IF-THEN-ELSE

    IF condition THEN
        statement;
    ELSE
        statement;
    END IF;
...

    SET SERVEROUTPU ON;

    DECLARE
        vNumber NUMBER(3) := 2;
    BEGIN
        IF MOD(vNumber, 2) = 0 THEN
            dbms_output.put_line('vNumber is event');
        ELSE 
            dbms_output.put_line('vNumber is odd');
        END IF;
        dbms_output.put_line('Finish');
    END;
    
#### IF-THEN-ELSIF    

    IF condition1 THEN
        statement;
    ELSIF condition2 THEN
        statement;
    ELSIF condition3 THEN
        statement;
    ELSE
        statement;
    END IF;

...

    SET SERVEROUTPU ON;

    DECLARE
        vScore NUMBER(3) := 90;
    BEGIN
        IF vScore >= 80 THEN
            dbms_output.put_line('Grade A');
        ELSIF vScore >= 70 THEN
            dbms_output.put_line('Grade B');
        ELSIF vScore >= 60 THEN
            dbms_output.put_line('Grade C');
        ELSIF vScore >= 50 THEN
            dbms_output.put_line('Grade D');
        ELSE
            dbms_output.put_line('Grade F');
        END IF;
        dbms_output.put_line('Finish');
    END;
    
#### Case Expression

    CASE search_expression
        WHEN input_expression THEN statement;
        ....
        ELSE statement;
    END CASE;

.

    SET SERVEROUTPU ON;

    DECLARE
        vScore NUMBER(3) := 2;
        vResult NVARCHAR2(10);
    BEGIN
        CASE vscore
            WHEN 0 THEN vResult := 'ONE';
            WHEN 1 THEN vResult := 'TWO';
            WHEN 2 THEN vResult := 'THREE';
            WHEN 3 THEN vResult := 'FOUR';
            WHEN 4 THEN vResult := 'FIVE';
            WHEN 5 THEN vResult := 'SIX';
            WHEN 6 THEN vResult := 'SEVEN';
            WHEN 7 THEN vResult := 'EIGHT';
            ELSE vResult := 'ERROR';
        END CASE;
        dbms_output.put_line(vResult);
    END;

## LOOP statement

#### Simple loop

    LOOP
        statement1;
        statement2;
        EXIT statement;
    END LOOP;

##### Simple loop with exit

    SET SERVEROUTPU ON;

    DECLARE
        vCount NUMBER(3) DEFAULT 0;
        vResult NUMBER;
    BEGIN
        LOOP
            vCount := vCount + 1;
            vResult := 19 * vCount;
            dbms_output.put_line('count '|| vCount || ' result ' || vResult);
            IF vCount >= 10 THEN
                EXIT;
            END IF;
        END LOOP;
        dbms_output.put_line('Finish');
    END;
    
##### Simple loop with exit when

    DECLARE
        vCount NUMBER(3) DEFAULT 0;
        vResult NUMBER;
    BEGIN
        LOOP
            vCount := vCount + 1;
            vResult := 19 * vCount;
            dbms_output.put_line('count '|| vCount || ' result ' || vResult);
            EXIT WHEN vCount >= 10;
        END LOOP;
        dbms_output.put_line('Finish');
    END;

#### While loop

    WHILE diffcondition LOOP
        statement1;
        statement1;
    END LOOP;

...

    SET SERVEROUTPU ON;

    DECLARE
        vCount NUMBER(3) DEFAULT 0;
        vResult NUMBER;
    BEGIN
        WHILE vCount <= 10 LOOP
            vResult := 19 * vCount;
            dbms_output.put_line('count '|| vCount || ' result ' || vResult);
            vCount := vCount + 1;
        END LOOP;
        dbms_output.put_line('Finish');
    END;
    /
    DECLARE
        vTest BOOLEAN DEFAULT TRUE;
        vCount NUMBER(3) DEFAULT 0;
        vResult NUMBER;
    BEGIN
        WHILE vTest LOOP
            vResult := 19 * vCount;
            dbms_output.put_line('count '|| vCount || ' result ' || vResult);
            vCount := vCount + 1;
            IF vCount >= 10 THEN
                vTest := FALSE;
            END IF;
        END LOOP;
        dbms_output.put_line('Finish');
    END;

#### FOR Loop

    FOR count IN [REVERSE] lower .. upper LOOP
        statement;
        statement;
    END LOOP;

...

    SET SERVEROUTPU ON;

    BEGIN
        FOR counter IN 1..10 LOOP
            dbms_output.put_line('counter ' || counter);
        END LOOP;
        dbms_output.put_line('Finish');
    END;
    /
    BEGIN
        FOR counter IN REVERSE 1..10 LOOP
            dbms_output.put_line('counter ' || counter);
        END LOOP;
        dbms_output.put_line('Finish');
    END;

## CURSOR

- ### Implicit Cursor

- ### Explicit Cursor

#### Syntax

    CURSOR cursor_name IS select_statement;

#### Explicit Cursor fetch single row

    SET SERVEROUTPU ON;

    DECLARE
        vTemp employee%ROWTYPE;
        CURSOR CURSOR_EMPLOYEE IS 
        SELECT
            *
        FROM employee WHERE emp_id = 1; 
    BEGIN
        OPEN CURSOR_EMPLOYEE;
            FETCH CURSOR_EMPLOYEE INTO vTemp;
            dbms_output.put_line(vTemp.emp_code);
        CLOSE CURSOR_EMPLOYEE;
    END;

#### Explicit Cursor fetch multiple row

    SET SERVEROUTPU ON;

    DECLARE
        vFirstName NVARCHAR2(100);
        vLastName NVARCHAR2(100);
        CURSOR CURSOR_EMPLOYEE IS 
        SELECT
            emp_first_name,
            emp_last_name
        FROM employee;
    BEGIN
        OPEN CURSOR_EMPLOYEE;
            LOOP
                FETCH CURSOR_EMPLOYEE INTO vFirstName, vLastName; 
                EXIT WHEN CURSOR_EMPLOYEE%NOTFOUND;
                dbms_output.put_line(vFirstName || ' ' ||vLastName);
            END LOOP;
        CLOSE CURSOR_EMPLOYEE;
    END;

#### Explicit Cursor FOR Loop

    SET SERVEROUTPU ON;

    DECLARE
        CURSOR CURSOR_EMPLOYEE IS 
        SELECT
            *
        FROM employee WHERE emp_id > 1; 
    BEGIN
        FOR row_cursor IN CURSOR_EMPLOYEE LOOP
            dbms_output.put_line(row_cursor.emp_code || ' ' || row_cursor.EMP_FIRST_NAME);
        END LOOP;
    END;

#### Explicit Cursor with parameterized

    CURSOR cursor_name(parameter_name data_type, ..N) IS select_statement;
.
    
    SET SERVEROUTPU ON;

    DECLARE
        CURSOR CURSOR_EMPLOYEE(pEmpId NUMBER) IS 
        SELECT
            *
        FROM employee WHERE emp_id > pEmpId; 
    BEGIN
        FOR row_cursor IN CURSOR_EMPLOYEE(1) LOOP
            dbms_output.put_line(row_cursor.emp_code || ' ' || row_cursor.EMP_FIRST_NAME);
        END LOOP;
    END;
    /
    DECLARE
        CURSOR CURSOR_EMPLOYEE(pEmpId NUMBER, pName NVARCHAR2) IS 
        SELECT
            *
        FROM employee WHERE emp_id > pEmpId AND emp_first_name <> pName; 
    BEGIN
        FOR row_cursor IN CURSOR_EMPLOYEE(1,'PPP') LOOP
            dbms_output.put_line(row_cursor.emp_code || ' ' || row_cursor.EMP_FIRST_NAME);
        END LOOP;
    END;
   
#### Explicit Cursor with parameterized and default value   
   
    SET SERVEROUTPU ON;

    DECLARE
        CURSOR CURSOR_EMPLOYEE(pEmpId NUMBER := 1, pName NVARCHAR2 := 'PPP') IS 
        SELECT
            *
        FROM employee WHERE emp_id > pEmpId AND emp_first_name <> pName; 
    BEGIN
        FOR row_cursor IN CURSOR_EMPLOYEE LOOP
            dbms_output.put_line(row_cursor.emp_code || ' ' || row_cursor.EMP_FIRST_NAME);
        END LOOP;
    END;

## Record Datatype

    TYPE type_name IS RECORD (
       field_name data_type,
       field_name data_type,
       ...N
    );
.

    SET SERVEROUTPU ON;

    DECLARE
        TYPE customType IS RECORD (
            username users.username%TYPE,
            ENABLED users.enabled%TYPE,
            FIRST_NAME profile.first_name%TYPE,
            LAST_NAME profile.last_name%TYPE,
            CITIZEN_ID profile.citizen_id%TYPE,
            TEL profile.tel%TYPE,
            EMAIL profile.email %TYPE
        );
        vDetail customType;
        CURSOR CURSOR_DETAIL(pLimit number := 1) IS 
            SELECT
                u.username,
                u.ENABLED,
                p.FIRST_NAME,
                p.LAST_NAME,
                p.CITIZEN_ID,
                p.TEL,
                p.EMAIL
            FROM users u
            INNER JOIN profile p ON u.profile_id = p.profile_id
            WHERE ROWNUM <= pLimit;
    BEGIN
        OPEN CURSOR_DETAIL(10);
            LOOP 
                FETCH CURSOR_DETAIL INTO vDetail;
                EXIT WHEN CURSOR_DETAIL%NOTFOUND;
                dbms_output.put_line(vdetail.username);
                dbms_output.put_line(vdetail.ENABLED);
                dbms_output.put_line(vdetail.FIRST_NAME);
                dbms_output.put_line(vdetail.LAST_NAME);
                dbms_output.put_line(vdetail.CITIZEN_ID);
                dbms_output.put_line(vdetail.TEL);
                dbms_output.put_line(vdetail.EMAIL);
                dbms_output.put_line('END ROW');
            END LOOP;
        CLOSE CURSOR_DETAIL;
        FOR temp IN CURSOR_DETAIL(2) LOOP
            vDetail := temp;
            dbms_output.put_line(vdetail.username);
            dbms_output.put_line(vdetail.ENABLED);
            dbms_output.put_line(vdetail.FIRST_NAME);
            dbms_output.put_line(vdetail.LAST_NAME);
            dbms_output.put_line(vdetail.CITIZEN_ID);
            dbms_output.put_line(vdetail.TEL);
            dbms_output.put_line(vdetail.EMAIL);
            dbms_output.put_line('END ROW2');
        END LOOP;
    END;
    
## Functions 

#### Syntax

    CREATE [OR REPLACE] FUNCTION function_name(Parameter 1, Parameter 2,...) RETURN data_type
    IS
        Declare variable...;
    BEGIN
        executable statement;
        RETURN (value);
    END;

#### Creating functions

    SET SERVEROUTPU ON;

    CREATE OR REPLACE FUNCTION funcAdd(num1 NUMBER, num2 NUMBER) RETURN NUMBER
    IS
        vResult NUMBER;
    BEGIN
        vResult := num1 + num2;
        RETURN vResult;
    END;
    /
    DECLARE
        vTemp NUMBER := funcAdd(10, 20);
    BEGIN
        dbms_output.put_line(vTemp);
    END;

## Stored Procedure 

    CREATE [OR REPLACE] PROCEDURE procedure_name(Parameter 1, Parameter 2,...) 
    IS
        Declare variable...;
    BEGIN
        executable statement;
    EXCEPTION
        executable statement;
    END procedure_name;

#### Simple Procedure

    CREATE OR REPLACE PROCEDURE SIMPLE_PROCEDURE AS
        vCode NVARCHAR2(20) DEFAULT '001';
        vName NVARCHAR2(100) := 'Pratya Yeekhaday';
    BEGIN
        dbms_output.put_line(vCode);
        dbms_output.put_line(vName);
    END SIMPLE_PROCEDURE;
    /
    SET SERVEROUTPU ON;
    EXEC SIMPLE_PROCEDURE;

#### Simple Procedure with handle exception

    CREATE OR REPLACE PROCEDURE SIMPLE_PROCEDURE AS
        vCode NVARCHAR2(20);
        vName NVARCHAR2(100);
    BEGIN
        vCode := '00100000000000000000000000000000000000000000000000000';
        vName := 'Pratya Yeekhaday';
        dbms_output.put_line(vCode);
        dbms_output.put_line(vName);
    EXCEPTION
      WHEN OTHERS THEN
        dbms_output.put_line('EXCEPTION' || SQLCODE || ' : ' || SQLERRM);
    END SIMPLE_PROCEDURE;
    /
    SET SERVEROUTPU ON;
    EXEC SIMPLE_PROCEDURE;

### Reference

- https://itsourteamwork.wordpress.com/2009/12/29/anchor-data-types-using-rowtype-in-oracle/

- https://www.databasestar.com/oracle-sqlcode-sqlerrm/
