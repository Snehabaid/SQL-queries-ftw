-- INIT database
-- Create the Students table
CREATE TABLE Students (
    student_id INT PRIMARY KEY,
    name VARCHAR(50),
    age INT,
    grade_level INT
);

-- Create the Courses table
CREATE TABLE Courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(50),
    credits INT
);

-- Create the Enrollments table
CREATE TABLE Enrollments (
    enrollment_id INT PRIMARY KEY,
    student_id INT,
    course_id INT,
    grade DECIMAL(3, 2),
    FOREIGN KEY (student_id) REFERENCES Students(student_id),
    FOREIGN KEY (course_id) REFERENCES Courses(course_id)
);

-- Insert sample data into Students
INSERT INTO Students (student_id, name, age, grade_level) VALUES
(1, 'Alice', 20, 3),
(2, 'Bob', 21, 4),
(3, 'Charlie', 19, 3),
(4, 'Diana', 22, 4),
(5, 'Ethan', 20, 3);

-- Insert sample data into Courses
INSERT INTO Courses (course_id, course_name, credits) VALUES
(1, 'Math', 3),
(2, 'Science', 4),
(3, 'History', 3),
(4, 'Art', 2);

-- Insert sample data into Enrollments
INSERT INTO Enrollments (enrollment_id, student_id, course_id, grade) VALUES
(1, 1, 1, 3.5),
(2, 1, 2, 4.0),
(3, 2, 1, 2.5),
(4, 2, 3, 3.0),
(5, 3, 2, 3.0),
(6, 3, 4, 2.0),
(7, 4, 1, 3.5),
(8, 4, 3, 4.0),
(9, 5, 2, 3.0),
(10, 5, 4, 3.5);
SELECT AVG(grade) AS average_grade
FROM Enrollments;

<img width="472" alt="image" src="https://github.com/user-attachments/assets/e8beab25-47bb-4f92-a65b-3ff952e5fbd1">


SELECT Students.name, Courses.course_name
FROM Students
INNER JOIN Enrollments ON Students.student_id = Enrollments.student_id
INNER JOIN Courses ON Enrollments.course_id = Courses.course_id; 1 

<img width="437" alt="image" src="https://github.com/user-attachments/assets/eec421aa-a4fe-467b-91bf-c0268acd0e2b">


SELECT grade_level, COUNT(*) AS student_count 
FROM Students 
GROUP BY grade_level;

<img width="502" alt="image" src="https://github.com/user-attachments/assets/f8a1b6f6-fe5c-4cfa-a7a0-ef0e9c85bff5">


SELECT Courses.course_name, MAX(Enrollments.grade) AS max_grade
FROM Courses
INNER JOIN Enrollments ON Courses.course_id = Enrollments.course_id
GROUP BY Courses.course_name;

<img width="512" alt="image" src="https://github.com/user-attachments/assets/572df237-9bce-4c49-9f5f-b3e05ef964bd">


SELECT AVG(grade) AS average_grade 
FROM Enrollments 
INNER JOIN Students ON Enrollments.student_id = Students.student_id 
WHERE Students.grade_level = 3;

<img width="393" alt="image" src="https://github.com/user-attachments/assets/94d22b36-abe7-48e9-99ca-52e60e1f5ab4">


SELECT Students.name, Courses.course_name, Courses.credits
FROM Students
INNER JOIN Enrollments ON Students.student_id = Enrollments.student_id
INNER JOIN Courses ON Enrollments.course_id = Courses.course_id;

<img width="475" alt="image" src="https://github.com/user-attachments/assets/8c1a9b56-7895-4c76-b883-5142f348312b">


SELECT Courses.course_name
FROM Courses
INNER JOIN Enrollments ON Courses.course_id = Enrollments.course_id
GROUP BY Courses.course_id
HAVING AVG(Enrollments.grade) > 3.0;

<img width="341" alt="image" src="https://github.com/user-attachments/assets/0abb1009-35f5-4781-a570-1c93e012d478">


SELECT Students.student_id, Students.name 
FROM Students 
LEFT JOIN Enrollments ON Students.student_id = Enrollments.student_id 
WHERE Enrollments.grade IS NULL OR Enrollments.grade <> 4.0 
GROUP BY Students.student_id, Students.name 
HAVING MAX(Enrollments.grade) IS NULL OR MAX(Enrollments.grade) <> 4.0;

<img width="470" alt="image" src="https://github.com/user-attachments/assets/565ffd52-f27a-448b-94cb-640412c40854">


SELECT Students.name
FROM Students
INNER JOIN Enrollments ON Students.student_id = Enrollments.student_id
GROUP BY Students.student_id
HAVING AVG(Enrollments.grade) > (SELECT AVG(grade) FROM Enrollments);

<img width="383" alt="image" src="https://github.com/user-attachments/assets/4e42755d-1f9f-4e65-908b-296938f08902">


SELECT Students.name, COUNT(Enrollments.course_id) AS total_courses, AVG(Enrollments.grade) AS average_grade
FROM Students
INNER JOIN Enrollments ON Students.student_id = Enrollments.student_id
GROUP BY Students.student_id;

<img width="490" alt="image" src="https://github.com/user-attachments/assets/7bdb37ba-4b36-43e0-9ddb-52f2d275cfaf">








