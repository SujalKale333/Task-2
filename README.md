# Task-2
created a Student Management Database and wrote basic queries. Now, let’s extend the database by adding new tables for Courses and Enrollments.



Student Management Database – SQL Task

CREATE DATABASE StudentDB;

USE StudentDB;
CREATE TABLE Students (
student_id INT PRIMARY KEY,
student_name VARCHAR(50),
department VARCHAR(30)
);

INSERT INTO Students VALUES
(1, 'Amit', 'IT'),
(2, 'Neha', 'IT'),
(3, 'Rahul', 'CSE'),
(4, 'Priya', 'CSE'),
(5, 'Sonal', 'ENTC');
CREATE TABLE Courses (
course_id INT PRIMARY KEY,
course_name VARCHAR(50),
credits INT
);

INSERT INTO Courses VALUES
(101, 'Database Systems', 4),
(102, 'Data Structures', 3),
(103, 'Operating Systems', 4);
CREATE TABLE Enrollments (
enrollment_id INT PRIMARY KEY,
student_id INT,
course_id INT,
marks INT,
FOREIGN KEY (student_id) REFERENCES Students(student_id),
FOREIGN KEY (course_id) REFERENCES Courses(course_id)
);

INSERT INTO Enrollments VALUES
(1, 1, 101, 88),
(2, 1, 102, 80),
(3, 2, 101, 75),
(4, 3, 102, 90),
(5, 3, 103, 95),
(6, 4, 103, 70),
(7, 5, 101, 78);

SELECT s.student_name, c.course_name, e.marks
FROM Enrollments e
JOIN Students s ON e.student_id = s.student_id
JOIN Courses c ON e.course_id = c.course_id;
SELECT c.course_name, AVG(e.marks) AS Average_Marks
FROM Enrollments e
JOIN Courses c ON e.course_id = c.course_id
GROUP BY c.course_name;

SELECT c.course_name, s.student_name, e.marks
FROM Enrollments e
JOIN Students s ON e.student_id = s.student_id
JOIN Courses c ON e.course_id = c.course_id
WHERE e.marks = (
SELECT MAX(marks)
FROM Enrollments
WHERE course_id = e.course_id
);

SELECT s.student_name, AVG(e.marks) AS Average_Marks
FROM Enrollments e
JOIN Students s ON e.student_id = s.student_id
GROUP BY s.student_name
ORDER BY Average_Marks DESC
LIMIT 1;

SELECT DISTINCT s.student_name
FROM Enrollments e
JOIN Students s ON e.student_id = s.student_id
WHERE e.marks > 80;
