select * from employees;


--Retrieve all employees whose salary is greater than 50,000
select *
from employees
where salary >=50000.00;

--Using LIKE for Pattern Matching
--Find all employees whose names start with "J".

select *
from employees
where name like 'J%';

--Sorting Data
--Retrieve employee names in ascending order by last_name.

select *
from employees
order by name;

--Count the Number of Records
--Find the total number of employees in the employees table.


select *,count(*)over() as no_of_emp
from employees;


--Find Maximum & Minimum Values
--Retrieve the highest and lowest salary in the company.

select max(salary),min(salary)     ----it will only give me max and min
from employees;


select *,max(salary)over()  -------if i need more colmns with the condition which is max and min
from employees
where salary=(
select max(salary)
from employees
);

select *,min(salary)over()
from employees
where salary=(
select max(salary)
from employees
);


Average Salary Calculation

Find the average salary of employees.

--Average Salary Calculation
--Find the average salary of employees.

select round(avg(salary))
from employees;

select *,round(avg(salary)over()) as avg_sal
from employees;

--Grouping Data
--Find the number of employees in each department.
select *
from employees;

select *
from departments;

select count(department_id)
from employees
group by department_id;

--INNER JOIN

--Get a list of employees along with their department names (assuming employees and departments
--tables are joined by department_id).

select *
from employees as e
join departments as d
 on e.department_id=d.id
 order by department_id;

--LEFT JOIN
--If you want to retrieve all employees and their attendance records 
--(showing employees even if they don’t have attendance records)

select *
from attendance;

select *
from employees as e
right join attendance as a
on e.id=a.employee_id
order by name;

--Get all employees hired after January 1, 2023

select *
from employees
where hire_date>'2023-01-01' ;

--How many employees were hired after this date?
select count(*)
from employees
where hire_date>'2023-01-01' ;


-- Retrieve the employees from the ‘HR’ department.
select *
from departments;

select *
from employees
where department_id=2;

--Can you find the highest-paid employee in HR

select *, max(salary)over()
from employees
where department_id=2;



select *
from employees
where salary=(
select max(salary)
from employees
where  department_id=2);

--Get all employees sorted by salary in descending order.

select *
from employees
order by salary desc;

--Who is the second highest-paid employee?

Select *
from employees
order by salary desc
limit 1 offset 1;



 --Find employees earning between $55,000 and $75,000.


select * 
from employees
where salary between 55000 and 75000; 

--How many employees fall within this salary range?

select *,count(*)over() as no_of_emp 
from employees
where salary between 55000 and 75000; 

--List all employees with names starting with ‘A’ or ‘E’.

select *
from employees where name like 'A%' or name like 'E%';

--How many employees have names starting with ‘A’ or ‘E’?


select count(*)
from employees where name like 'A%' or name like 'E%';


SELECT 
    SUM(CASE WHEN name LIKE 'A%' THEN 1 ELSE 0 END) AS A_employees,
    SUM(CASE WHEN name LIKE 'E%' THEN 1 ELSE 0 END) AS E_employees
FROM employees;


--Get the total number of employees in the company.

select count(*)
from employees;


--Find the average salary of all employees.

select round(avg(salary))
from employees;

--Get a list of employees along with their department names.



select e.name,d.department_name
from employees as e
join departments as d
on e.department_id=d.id;


--How many employees are in each department?

select d.department_name,count(e.id)
from employees as e
join departments as d
on e.department_id=d.id
group by d.department_name ;

--Find all employees who were absent on February 2, 2024.

select*
from attendance;

select *
from employees as e
join attendance as a
on e.id=a.employee_id
where status='Absent' and date='2024-02-02';



--Increase the salary of all employees by 10%.

select *,(salary*0.1)+salary as new_salary
from employees;

DELETE FROM employees                       ---curdate()is current date
WHERE DATEDIFF(CURDATE(), hire_date) > 1825;  -- 1825 days = 5 years
                                                 -- datediff is difference btw the date given
