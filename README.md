create database UniversityDB
use UniversityDB;
create table Departments(
DepartmentID INT PRIMARY KEY auto_increment, 
DepartmentName varchar(100) NOT NULL
);

Create table Students(
StudentID INT PRIMARY KEY auto_increment,
NAME VARCHAR(100) NOT NULL,
AGE INT NOT NULL,
DEPARTMENTID INT,
FOREIGN KEY(DepartmentID) REFERENCES Departments(DepartmentID)
);

Create TABLE Courses(
CourseID INT PRIMARY KEY auto_increment,
CourseName VARCHAR(100) NOT NULL,
StudentID INT,
foreign key(StudentID) REFERENCES Students(StudentID)
);

INSERT INTO Departments(DepartmentName) values
('Computer Science'),
('Mechical Engineering'),
('Electrical Engineering');

INSERT INTO Students(NAME, AGE, DepartmentID) values
('ALICE JOHSON',21,1),
('BOB SMITH',22,2),
('CHARLIE BROWN',20,1),
('DAVID WHITE',23,3),
('EMMA WATSON',21,2);

Insert into Courses(CourseName,StudentID) VALUES
('DATABASE MANAGEMENT',1),
('OPERATING SYSTEM',1),
('THERMODYNAMICS',2),
('DIGITAL CIRCUITS',3),
('ARTIIFICIAL INTELLIGENCE',1),
('HEAT TRANSFER',2),
('POWER SYSTEMS',4),
('DATA STRUCTURES',3),
('FLUID MECHANICS',5),
('MACHINE LEARNING',1);

SELECT Students.StudentID, Students.Name, Students.Age, Departments.DepartmentName
FROM Students
JOIN Departments on Students.DepartmentId = Departments.DepartmentID;

SELECT Students.Name 
FROM Students 
JOIN Courses ON Students.StudentID = Courses.StudentID 
WHERE Courses.CourseName = 'Artificial Intelligence';

SELECT Departments.DepartmentName, COUNT(Students.StudentID) AS StudentCount 
FROM Departments 
LEFT JOIN Students ON Departments.DepartmentID = Students.DepartmentID 
GROUP BY Departments.DepartmentName;

SELECT Courses.CourseName 
FROM Courses 
JOIN Students ON Courses.StudentID = Students.StudentID 
WHERE Students.Name = 'Alice Johnson';

SELECT Students.Name, COUNT(Courses.CourseID) AS CourseCount 
FROM Students 
JOIN Courses ON Students.StudentID = Courses.StudentID 
GROUP BY Students.StudentID 
HAVING CourseCount > 1;

SELECT Departments.DepartmentName, AVG(Students.Age) AS AvgAge 
FROM Departments 
JOIN Students ON Departments.DepartmentID = Students.DepartmentID 
GROUP BY Departments.DepartmentName;

SELECT Departments.DepartmentName 
FROM Departments 
JOIN Students ON Departments.DepartmentID = Students.DepartmentID 
GROUP BY Departments.DepartmentName 
ORDER BY COUNT(Students.StudentID) DESC 
LIMIT 1;

SELECT Students.Name 
FROM Students 
LEFT JOIN Courses ON Students.StudentID = Courses.StudentID 
WHERE Courses.StudentID IS NULL;

SELECT Students.Name, COUNT(Courses.CourseID) AS TotalCourses 
FROM Students 
LEFT JOIN Courses ON Students.StudentID = Courses.StudentID 
GROUP BY Students.StudentID;

SELECT Students.Name 
FROM Students 
JOIN Departments ON Students.DepartmentID = Departments.DepartmentID 
JOIN Courses ON Students.StudentID = Courses.StudentID 
WHERE Departments.DepartmentName = 'Computer Science' 
AND Courses.CourseName LIKE '%Data%';
