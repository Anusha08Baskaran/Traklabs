# Traklabs
Coding assessment


CREATE TABLE salaries (
	emp_no INT PRIMARY KEY,
	salary INT,
	from_date DATE,
	to_date DATE
);

CREATE TABLE departments (
	dept_no VARCHAR(50) PRIMARY KEY,
	dept_name VARCHAR(50)
);

CREATE TABLE employees (
	emp_no INT PRIMARY KEY,
	birth_date DATE,
	first_name VARCHAR(50),
	last_name VARCHAR(50),
	gender VARCHAR(50),
	hire_date DATE,
	FOREIGN KEY (emp_no) REFERENCES salaries(emp_no)
);

CREATE TABLE dept_emp (
	emp_no INT,
	dept_no VARCHAR(50),
	from_date DATE,
	to_date DATE,
	PRIMARY KEY (emp_no, dept_no),
	FOREIGN KEY (emp_no) REFERENCES employees(emp_no),
	FOREIGN KEY (dept_no) REFERENCES departments(dept_no)
);

CREATE TABLE dept_manager (
	dept_no VARCHAR(50),
	emp_no INT,
	from_date DATE,
	to_date DATE,
	PRIMARY KEY (dept_no, emp_no),
	FOREIGN KEY (dept_no) REFERENCES departments(dept_no),
	FOREIGN KEY (emp_no) REFERENCES employees(emp_no)
);

CREATE TABLE titles (
	emp_no INT,
	title VARCHAR(50),
	from_date DATE,
	to_date DATE,
	PRIMARY KEY (emp_no, title, from_date),
	FOREIGN KEY (emp_no) REFERENCES employees(emp_no)
); 



SELECT employees.emp_no, employees.last_name, employees.first_name, employees.gender, salaries.salary
FROM employees
INNER JOIN salaries ON employees.emp_no = salaries.emp_no;


SELECT emp_no, last_name, first_name, hire_date
FROM employees
WHERE hire_date >= '1986-01-01' and hire_date <= '1986-12-31';


SELECT dept_manager.dept_no, departments.dept_name, dept_manager.emp_no, employees.last_name, employees.first_name, dept_manager.from_date, dept_manager.to_date
FROM dept_manager
INNER JOIN departments ON dept_manager.dept_no = departments.dept_no
INNER JOIN employees ON employees.emp_no = dept_manager.emp_no;


SELECT employees.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM employees
INNER JOIN dept_emp ON dept_emp.emp_no = employees.emp_no
INNER JOIN departments ON departments.dept_no = dept_emp.dept_no;


SELECT emp_no, last_name, first_name
FROM employees
WHERE first_name = 'Hercules' AND last_name LIKE 'B%';


SELECT employees.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM employees
INNER JOIN dept_emp ON dept_emp.emp_no = employees.emp_no
INNER JOIN departments ON departments.dept_no = dept_emp.dept_no
WHERE departments.dept_name = 'Sales';


SELECT employees.emp_no, employees.last_name, employees.first_name, departments.dept_name
FROM employees
INNER JOIN dept_emp ON dept_emp.emp_no = employees.emp_no
INNER JOIN departments ON departments.dept_no = dept_emp.dept_no
WHERE departments.dept_name = 'Sales' OR departments.dept_name = 'Development';


SELECT last_name, COUNT(last_name) AS "Last Name Count"
FROM employees
GROUP BY last_name
ORDER BY "Last Name Count" DESC; 
 
 
UPDATE * FROM employees SET departments.dept_name='Sales';

UPDATE employees SET departments.dept_no=1 WHERE departments.dept_name='Sales';

DELETE FROM employees WHERE departments.dept_name='Development';







