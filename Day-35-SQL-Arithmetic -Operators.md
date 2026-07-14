# Day 35 from today we will learn about SQL operators and today we will focus on Arithmetic operators

The arithmetic operators are used to perform mathematical operations on numeric data types. The common arithmetic operators in SQL include:

for this we will use the employees table which contains the following columns: employee_id, first_name, last_name, salary, and department_id.

Employee Table:

  ![Employee Table](./src/assits/Day-35-Arithematic-Operator-Practic-images/Employee_table.png)


1. Addition (+): Used to add two numbers together.
   Example: SELECT * FROM employees WHERE salary + 1000 > 5000;
   Output: This query will return all employees whose salary plus 1000 is greater than 5000.

   ![Addition](./src/assits/Day-35-Arithematic-Operator-Practic-images/Arithematic_Addition_operator_practic.png)


2. Subtraction (-): Used to subtract one number from another.
   Example: SELECT * FROM employees WHERE salary - 1000 < 4000;
   Output: This query will return all employees whose salary minus 1000 is less than 4000.

   ![Subtraction](./src/assits/Day-35-Arithematic-Operator-Practic-images/Arithematic_Subtraction_operator_practic.png)


3. Multiplication (*): Used to multiply two numbers.
   Example: SELECT * FROM employees WHERE salary * 2 = 10000;
   Output: This query will return all employees whose salary multiplied by 2 equals 10000.
   
   ![Multiplication](./src/assits/Day-35-Arithematic-Operator-Practic-images/Arithematic_Multiplication_operator_practic.png)

4. Division (/): Used to divide one number by another.
   Example: SELECT * FROM employees WHERE salary / 2 = 2500;
   Output: This query will return all employees whose salary divided by 2 equals 2500.
   
   ![Division](./src/assits/Day-35-Arithematic-Operator-Practic-images/Arithematic_Division_operator_practic.png)

5. Modulus (%): Used to find the remainder of a division operation.
   Example: SELECT * FROM employees WHERE salary % 1000 = 0;
   Output: This query will return all employees whose salary is divisible by 1000 with no remainder.
   
   ![Modulus](./src/assits/Day-35-Arithematic-Operator-Practic-images/Arithematic_Modulus_operator_practic.png) 
   