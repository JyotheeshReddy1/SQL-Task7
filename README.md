-- SQL-Task7 --
-- Task 7:Creating Views

-- Create Tables

CREATE TABLE Departments (
    DeptID INT PRIMARY KEY,
    DeptName VARCHAR(50)
);

CREATE TABLE Employees (
    EmpID INT PRIMARY KEY,
    EmpName VARCHAR(50),
    DepartmentID INT FOREIGN KEY REFERENCES Departments(DeptID),
    Salary DECIMAL(10,2)
);

-- Insert Sample Data

INSERT INTO Departments VALUES 
(1, 'HR'),
(2, 'IT'),
(3, 'Finance');

INSERT INTO Employees VALUES
(101, 'Alice', 1, 60000),
(102, 'Bob', 2, 75000),
(103, 'Charlie', 2, 50000),
(104, 'Diana', 3, 80000),
(105, 'Eve', 1, 45000);

-- Create Views

-- Simple View --
CREATE VIEW EmployeePublicInfo AS
SELECT EmpName, DepartmentID
FROM Employees;

-- Complex View with JOIN --
CREATE VIEW EmployeeWithDept AS
SELECT e.EmpID, e.EmpName, d.DeptName, e.Salary
FROM Employees e
JOIN Departments d ON e.DepartmentID = d.DeptID;

-- Aggregated View --
CREATE VIEW DeptSalaryStats AS
SELECT d.DeptName, 
       AVG(e.Salary) AS AvgSalary, 
       COUNT(*) AS TotalEmployees
FROM Employees e
JOIN Departments d ON e.DepartmentID = d.DeptID
GROUP BY d.DeptName;

-- Step 4: Use Views (Examples)

-- 1: Public employee info --
SELECT * FROM EmployeePublicInfo;

-- 2: Employees with department names & salary filter --
SELECT EmpName, DeptName, Salary 
FROM EmployeeWithDept
WHERE Salary > 60000;

-- 3: Department salary stats with filter --
SELECT * FROM DeptSalaryStats WHERE AvgSalary > 55000;
