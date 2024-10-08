-- Criar schema se não existir
CREATE SCHEMA IF NOT EXISTS azure_company;

-- Usar schema
SET search_path TO azure_company;

-- Consultar constraints da tabela
SELECT * FROM information_schema.table_constraints
	WHERE constraint_schema = 'azure_company';

-- Criar tabela employee
CREATE TABLE employee (
	Fname VARCHAR(15) NOT NULL,
	Minit CHAR(1),
	Lname VARCHAR(15) NOT NULL,
	Ssn CHAR(9) NOT NULL, 
	Bdate DATE,
	Address VARCHAR(30),
	Sex CHAR(1),
	Salary DECIMAL(10, 2),
	Super_ssn CHAR(9),
	Dno INT NOT NULL,
	CONSTRAINT chk_salary_employee CHECK (Salary > 2000.0),
	CONSTRAINT pk_employee PRIMARY KEY (Ssn)
);

-- Adicionar foreign key
ALTER TABLE employee 
	ADD CONSTRAINT fk_employee 
	FOREIGN KEY(Super_ssn) REFERENCES employee(Ssn)
	ON DELETE SET NULL
	ON UPDATE CASCADE;

-- Adicionar coluna com valor padrão
ALTER TABLE employee 
	ALTER COLUMN Dno SET DEFAULT 1;

-- Criar tabela department
CREATE TABLE department (
	Dname VARCHAR(15) NOT NULL,
	Dnumber INT NOT NULL,
	Mgr_ssn CHAR(9) NOT NULL,
	Mgr_start_date DATE, 
	Dept_create_date DATE,
	CONSTRAINT chk_date_dept CHECK (Dept_create_date < Mgr_start_date),
	CONSTRAINT pk_dept PRIMARY KEY (Dnumber),
	CONSTRAINT unique_name_dept UNIQUE (Dname),
	FOREIGN KEY (Mgr_ssn) REFERENCES employee(Ssn)
);

-- Modificar foreign key
ALTER TABLE department 
	DROP CONSTRAINT fk_dept, 
	ADD CONSTRAINT fk_dept FOREIGN KEY(Mgr_ssn) REFERENCES employee(Ssn)
	ON UPDATE CASCADE;

-- Criar tabela dept_locations
CREATE TABLE dept_locations (
	Dnumber INT NOT NULL,
	Dlocation VARCHAR(15) NOT NULL,
	CONSTRAINT pk_dept_locations PRIMARY KEY (Dnumber, Dlocation),
	CONSTRAINT fk_dept_locations FOREIGN KEY (Dnumber) REFERENCES department (Dnumber)
);

-- Modificar foreign key
ALTER TABLE dept_locations 
	DROP CONSTRAINT fk_dept_locations, 
	ADD CONSTRAINT fk_dept_locations FOREIGN KEY (Dnumber) REFERENCES department(Dnumber)
	ON DELETE CASCADE
	ON UPDATE CASCADE;

-- Criar tabela project
CREATE TABLE project (
	Pname VARCHAR(15) NOT NULL,
	Pnumber INT NOT NULL,
	Plocation VARCHAR(15),
	Dnum INT NOT NULL,
	PRIMARY KEY (Pnumber),
	CONSTRAINT unique_project UNIQUE (Pname),
	CONSTRAINT fk_project FOREIGN KEY (Dnum) REFERENCES department(Dnumber)
);

-- Criar tabela works_on
CREATE TABLE works_on (
	Essn CHAR(9) NOT NULL,
	Pno INT NOT NULL,
	Hours DECIMAL(3, 1) NOT NULL,
	PRIMARY KEY (Essn, Pno),
	CONSTRAINT fk_employee_works_on FOREIGN KEY (Essn) REFERENCES employee(Ssn),
	CONSTRAINT fk_project_works_on FOREIGN KEY (Pno) REFERENCES project(Pnumber)
);

-- Criar tabela dependent
DROP TABLE IF EXISTS dependent; -- Usar IF EXISTS para evitar erro se a tabela não existir
CREATE TABLE dependent (
	Essn CHAR(9) NOT NULL,
	Dependent_name VARCHAR(15) NOT NULL,
	Sex CHAR(1),
	Bdate DATE,
	Relationship VARCHAR(8),
	PRIMARY KEY (Essn, Dependent_name),
	CONSTRAINT fk_dependent FOREIGN KEY (Essn) REFERENCES employee(Ssn)
);

