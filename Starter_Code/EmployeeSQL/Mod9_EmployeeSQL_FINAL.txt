-- Exported from QuickDBD: https://www.quickdatabasediagrams.com/
-- Link to schema: https://app.quickdatabasediagrams.com/#/d/xrYYU7
-- NOTE! If you have used non-SQL datatypes in your design, you will have to change these here.

-- Modify this code to update the DB schema diagram.
-- To reset the sample schema, replace everything with
-- two dots ('..' - without quotes).
DROP TABLE IF EXISTS DeptManagers
CREATE TABLE Departments (
    dept_no varchar(10)   NOT NULL,
    dept_name varchar(25) NOT NULL,
    CONSTRAINT pk_Departments PRIMARY KEY (
        dept_no
     )
);

CREATE TABLE DeptEmployees (
    emp_no int   NOT NULL,
    FOREIGN KEY (emp_no) REFERENCES Employees(emp_no),
    dept_no varchar(10)   NOT NULL,
    FOREIGN KEY (dept_no) REFERENCES Departments(dept_no),
    PRIMARY KEY (emp_no, dept_no)
);

CREATE TABLE Employees (
    emp_no int   NOT NULL,
    emp_title_id varchar(20)   NOT NULL,
    birth_date date   NOT NULL,
    first_name varchar(75)   NOT NULL,
    last_name varchar(75)   NOT NULL,
    sex varchar(10)   NOT NULL,
    hire_date date   NOT NULL,
    CONSTRAINT pk_Employees PRIMARY KEY (
        emp_no
     )
);

CREATE TABLE DeptManagers (
    dept_no varchar(10) NOT NULL,
	FOREIGN KEY (dept_no) REFERENCES Departments(dept_no),
    emp_no int NOT NULL,
	FOREIGN KEY (emp_no) REFERENCES Employees(emp_no),
	PRIMARY KEY (emp_no, dept_no)
	 
);


CREATE TABLE Salaries (
    emp_no int   NOT NULL,
	FOREIGN KEY (emp_no) REFERENCES Employees(emp_no),
    salary int   NOT NULL
);

CREATE TABLE Titles (
    title_id varchar(10)   NOT NULL,
    title varchar(30)   NOT NULL,
    CONSTRAINT pk_Titles PRIMARY KEY (
        title_id
     )
);

ALTER TABLE Departments ADD CONSTRAINT fk_Departments_dept_no FOREIGN KEY(dept_no)
REFERENCES DeptManagers (dept_no);

ALTER TABLE DeptEmployees ADD CONSTRAINT fk_DeptEmployees_emp_no FOREIGN KEY(emp_no)
REFERENCES Employees (emp_no);

ALTER TABLE DeptEmployees ADD CONSTRAINT fk_DeptEmployees_dept_no FOREIGN KEY(dept_no)
REFERENCES Departments (dept_no);

ALTER TABLE DeptManagers ADD CONSTRAINT fk_DeptManagers_emp_no FOREIGN KEY(emp_no)
REFERENCES Employees (emp_no);

ALTER TABLE Employees ADD CONSTRAINT fk_Employees_emp_title_id FOREIGN KEY(emp_title_id)
REFERENCES Titles (title_id);

ALTER TABLE Salaries ADD CONSTRAINT fk_Salaries_emp_no FOREIGN KEY(emp_no)
REFERENCES Employees (emp_no);