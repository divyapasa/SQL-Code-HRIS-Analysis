# SQL-Code-HRIS-Analysis
SQL code samples for HR Data
*************************************************************************************

**SQL CODE EXAMPLES AND REAL-TIME SCENARIOS
To automate data extraction and reporting processes using SQL scripts. 

1.	Display all employees hired between January 1, 2022, and December 31, 2022, and sort the result by the hire date.

SELECT employee_id, first_name, last_name, hire_date, salary 
FROM employees
WHERE hire_date BETWEEN '2022-01-01' AND '2022-12-31'
ORDER BY hire_date;

•	This SQL script will extract data of all employees who were hired between January 1, 2022, and December 31, 2022, and sort the result by the hire date. 
•	Further, we can save this script as a SQL file and execute it using a scheduling tool or command line interface to automate the data extraction process.

 We can save the result set in a CSV file using the following SQL script:

SELECT employee_id, first_name, last_name, hire_date, salary 
FROM employees
WHERE hire_date BETWEEN '2022-01-01' AND '2022-12-31'
ORDER BY hire_date
INTO OUTFILE '/path/to/file.csv'
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n';

•	This SQL script will save the result set in a CSV file located at the specified file path. 
•	We can use the same scheduling tool or command line interface to automate the process of saving the result set in a CSV file.
•	By automating these processes, we can generate HR reports more efficiently. 

To generate HR reports using the CSV file:

1.	Import the CSV file into a data visualization tool such as Tableau, Power BI, or Excel.
2.	Choosing the appropriate visualization format, such as bar chart, line chart, or table, depending on the type of HR report you want to generate.
3.	Selecting the data fields that we want to include in the HR report, such as employee ID, first name, last name, hire date, salary, and any other relevant fields.
4.	Customize the report by adding filters, sorting options, and formatting to make the report easier to understand.
5.	Save the report in a format that can be shared with others, such as PDF, PowerPoint, or Excel.

********************************************************************************************************

2.	Calculate each employee's total compensation based on their hourly rate and hours worked?

SELECT employee_id, 
 (hourly_rate * hours_worked + overtime_pay) AS total_compensation 
FROM employee;
	
This SQL query extracts data from table called "employee" with columns for "employee_id", "hourly_rate", "hours_worked", and "overtime_pay". The query calculates the total compensation for each employee by multiplying their hourly rate by the number of hours worked, and adding any overtime pay. The results will display the employee ID and their total compensation.

Explanation of how the calculation works:

The expression "(hourly_rate * hours_worked + overtime_pay)" calculates the total compensation for each employee. This expression multiplies the employee's hourly rate by the number of hours worked, and adds any overtime pay.


********************************************************************************************************How to automate payroll process:

3.	Calculate employee compensation, taxes, and deductions based on data stored in a database. calculate employee gross pay, federal tax, state tax, and net pay?

We had to retrieve the employee ID, first name, last name, hourly rate, hours worked, gross pay, federal tax, state tax, and net pay.


SELECT 
  employee_id, 
  first_name, 
  last_name, 
  hourly_rate, 
  hours_worked, 
  hourly_rate * hours_worked AS gross_pay, 
  gross_pay * federal_tax_rate AS federal_tax, 
  gross_pay * state_tax_rate AS state_tax, 
  gross_pay - federal_tax - state_tax AS net_pay 
FROM 
  employee, 
  tax_rates 
WHERE 
  employee.state = tax_rates.state;

Query explanation: 

•	The query extracts data from table called "employee" with columns for "employee_id", "first_name", "last_name", "hourly_rate", and "hours_worked". 
•	It also extracts data from another table called "tax_rates" with columns for "state", "federal_tax_rate", and "state_tax_rate". 
•	The query calculates each employee's gross pay by multiplying their hourly rate by the number of hours worked, and then calculates federal and state taxes and net pay based on the tax rates for the employee's state. 


Explanation of how the calculation works:

•	The expression "hourly_rate * hours_worked" calculates the gross pay for each employee. This expression multiplies the employee's hourly rate by the number of hours worked.
•	The expressions "gross_pay * federal_tax_rate" and "gross_pay * state_tax_rate" calculate the federal and state taxes for each employee, respectively. These expressions multiply the employee's gross pay by the federal and state tax rates for their state.
•	The expression "gross_pay - federal_tax - state_tax" calculates the net pay for each employee. This expression subtracts the federal and state taxes from the employee's gross pay.

********************************************************************************************************
Automate time and attendance tracking using sql 


4.	How to track time and attendance use data from an HR system that tracks employee attendance and time off?

SELECT 
  employee_id, 
  punch_in, 
  punch_out, 
  time_off_type 
FROM 
  attendance_data 
WHERE 
  punch_in BETWEEN '2023-01-01' AND '2023-01-31'
  AND time_off_type IS NULL;

•	This SQL code selects time and attendance data from the "attendance_data" table for the month of January 2023, but excludes any records for time off. 
•	The resulting data will include the employee ID, punch in time, punch out time, and any other relevant fields from the "attendance_data" table.


Once we extract the time and attendance data, we can use SQL to generate reports and analytics.

For example, a query to calculate the total hours worked by each employee for the month of January 2023:

SELECT 
  employee_id, 
  SUM(DATEDIFF(minute, punch_in, punch_out)) / 60.0 AS hours_worked 
FROM 
  attendance_data 
WHERE 
  punch_in BETWEEN '2023-01-01' AND '2023-01-31'
  AND time_off_type IS NULL 
GROUP BY 
  employee_id;

This query calculates the total hours worked by each employee for the month of January 2023, excluding any records for time off. The results will display the employee ID and total hours worked.


 Explanation of how the query works:

•	The SELECT statement specifies the columns to be retrieved from the "attendance_data" table. In this case, we want to retrieve the employee ID and the total hours worked.
•	The SUM function is used to add up the total number of minutes worked by each employee. The DATEDIFF function is used to calculate the difference between the punch in and punch out times in minutes.
•	The / 60.0 expression is used to convert the total number of minutes worked to hours.
•	The WHERE clause is used to filter the data based on certain conditions. In this case, we want to retrieve data for the month of January 2023, and exclude any records for time off.
•	The GROUP BY clause groups the data by employee ID, so that the total hours worked can be calculated separately for each employee.

********************************************************************************************************
Some commonly used sql queries to generate reports based on the requirement.

-- Headcount report by department and job title
SELECT Department, JobTitle, COUNT(*) AS Headcount
FROM Employees
GROUP BY Department, JobTitle;
	
-- Turnover report by department
SELECT Department, COUNT(*) AS TotalEmployees, SUM(CASE WHEN TerminationDate IS NOT NULL THEN 1 ELSE 0 END) AS Terminations, 
(CAST(SUM(CASE WHEN TerminationDate IS NOT NULL THEN 1 ELSE 0 END) AS FLOAT) / COUNT(*) * 100) AS TurnoverPercentage
FROM Employees
GROUP BY Department;

-- Diversity report by department and race/ethnicity
SELECT Department, RaceEthnicity, COUNT(*) AS Headcount
FROM Employees
GROUP BY Department, RaceEthnicity;


Identify trends and patterns:

-- Identify departments with high turnover rates
SELECT Department, COUNT(*) AS TotalEmployees, SUM(CASE WHEN TerminationDate IS NOT NULL THEN 1 ELSE 0 END) AS Terminations, 
(CAST(SUM(CASE WHEN TerminationDate IS NOT NULL THEN 1 ELSE 0 END) AS FLOAT) / COUNT(*) * 100) AS TurnoverPercentage
FROM Employees
WHERE HireDate >= '2019-01-01' AND TerminationDate IS NOT NULL
GROUP BY Department
HAVING TurnoverPercentage > 15;

-- Identify employees with high performance ratings
SELECT Name, JobTitle, PerformanceRating
FROM Employees
WHERE PerformanceRating >= 4;


Conduct data analysis:

-- Regression analysis to identify factors that impact employee turnover
SELECT JobTitle, Department, Salary, PerformanceRating, HireDate, TerminationDate
FROM Employees
WHERE HireDate >= '2019-01-01' AND TerminationDate IS NOT NULL;

-- Predictive modeling to forecast headcount by department
SELECT Department, COUNT(*) AS Headcount, YEAR(HireDate) AS Year, MONTH(HireDate) AS Month
FROM Employees
GROUP BY Department, YEAR(HireDate), MONTH(HireDate);


Troubleshoot data issues:

-- Query to identify employees with missing data
SELECT *
FROM Employees
WHERE Department IS NULL OR JobTitle IS NULL OR Salary IS NULL;

-- Query to identify discrepancies between HR and payroll systems
SELECT e.EmployeeID, e.Name, e.Department, e.JobTitle, e.Salary, p.Salary AS PayrollSalary
FROM Employees e
JOIN Payroll p ON e.EmployeeID = p.EmployeeID
WHERE e.Salary <> p.Salary;


********************************************************************************************************
