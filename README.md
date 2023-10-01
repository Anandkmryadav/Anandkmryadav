  How to find nth highest salary in sql (SQL SERVER)
 Script:
Create table Employees
(
     ID int primary key identity,
     FirstName nvarchar(50),
     LastName nvarchar(50),
     Gender nvarchar(50),
     Salary int
)
Insert into Employees values ('Anand', 'kumar', 'Male', 70000)
Insert into Employees values ('Arun', 'kmr', 'Male', 60000)
Insert into Employees values ('Sudhir', 'kr', 'Male', 45000)
Insert into Employees values ('Satish', 'Yadav', 'Male', 70000)
Insert into Employees values ('Soni', 'Kumari', 'Female', 45000)
Insert into Employees values ('Pinki', 'Kumari', 'Female', 30000)
Insert into Employees values ('Tanya', 'Kumari', 'Female', 35000)
Insert into Employees values ('Ritik', 'Kumar', 'Male', 80000)

 To  find the  highest salary it is straight forward. we can simply use the Max() function as shown below.
Select MAX(salary)as Maxsalary from Employees;

To get the second highest salary use a sub query along with MAX() function as show below.
Select MAX(salary)  as second_highest from Employees where salary <
(Select MAX(salary)   from Employees );

 Find the nth highest salary
SELECT Salary
FROM (
    SELECT Salary, ROW_NUMBER() OVER (ORDER BY Salary DESC) AS RowNum
    FROM Employees
) AS RankedSalaries
WHERE RowNum = 2;
 OR
SELECT TOP 1 salary FROM 
(
SELECT  DISTINCT  TOP /*nth number*/2 salary FROM Employees order by salary desc  
) as result
order by Salary
