--Data Analysis Questions

--List the employee number, last name, first name, sex, and salary of each employee.
CREATE VIEW emp_salary AS
	SELECT salaries.salary, employees.emp_no, employees.last_name, employees.first_name, employees.sex 
	FROM salaries
	INNER JOIN employees ON
	employees.emp_no=salaries.emp_no;

SELECT * FROM emp_salary

--List the first name, last name, and hire date for the employees who were hired in 1986.
CREATE VIEW year_hires AS
	SELECT first_name, last_name, hire_date
	FROM employees
	WHERE hire_date BETWEEN '1986-01-01' AND '1986-12-31';
	
SELECT * FROM year_hires


--List the manager of each department along with their department number, 
	--department name, employee number, last name, and first name.
CREATE VIEW manager_info AS
	SELECT deptmanagers.dept_no, deptmanagers.emp_no, departments.dept_name, employees.last_name, employees.first_name
	FROM deptmanagers
INNER JOIN departments ON
	departments.dept_no=deptmanagers.dept_no
INNER JOIN employees ON employees.emp_no=deptmanagers.emp_no;

SELECT * FROM manager_info
	

--List the department number for each employee along with that employee’s employee number, 
	--last name, first name, and department name.
DROP VIEW IF EXISTS employee_info
CREATE VIEW employee_info AS
	SELECT deptemployees.dept_no, departments.dept_name, deptemployees.emp_no, employees.last_name, employees.first_name
	FROM deptemployees
INNER JOIN departments ON
	departments.dept_no=deptemployees.dept_no
INNER JOIN employees ON employees.emp_no=deptemployees.emp_no;

SELECT * FROM employee_info

--List first name, last name, and sex of each employee whose first name is Hercules 
	--and whose last name begins with the letter B.
SELECT first_name, last_name, sex
	FROM employees
	WHERE first_name = 'Hercules' AND last_name LIKE 'B%';


--List each employee in the Sales department, including their employee number, last name, & first name.
SELECT emp_no, last_name, first_name, dept_name
	FROM employee_info
	WHERE dept_name = 'Sales'
	

--List each employee in the Sales and Development departments, including their employee number, last name, first name, and department name.
SELECT emp_no, last_name, first_name, dept_name
	FROM employee_info
	WHERE dept_name IN ('Sales', 'Development');


--List the frequency counts, in descending order, of all the employee last names 
	--(that is, how many employees share each last name).
SELECT last_name, COUNT(last_name) as "total_names"
FROM employees
GROUP BY last_name 
ORDER BY "total_names" DESC;
