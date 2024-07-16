# PostgreSQL-students-database-part-2

This project is the second part of my Relational Databases certification provided by freeCodeCamp.org. It involves writing and running a series of SQL queries to extract specific information from a PostgreSQL student database. The database schema and data were created in the first part of the project.

## Project Structure

```
/project_directory
│
├── students.sql
│ └── (SQL script to create the database tables)
│
└── student_info.sh
└── (Bash script to run various SQL queries on the student database)

```

## Learned Concepts

During this project, I gained practical experience with the following concepts:

1. **Database Schema Design**: Understanding how to structure a relational database with tables and relationships.
2. **SQL Query Writing**: Crafting complex SQL queries to retrieve and manipulate data.
3. **Bash Scripting**: Automating database operations and running SQL commands through scripts.
4. **Data Extraction**: Extracting specific information from a database based on given criteria.
5. **Data Aggregation**: Using SQL functions to aggregate and summarize data.
6. **String Operations**: Performing case-insensitive searches and pattern matching in SQL.
7. **Conditional Logic**: Applying conditional logic in SQL queries to filter and sort data.
8. **Joining Tables**: Using various types of joins to combine data from multiple tables.
9. **Subqueries**: Writing subqueries to retrieve intermediate results for further processing.

## Script Explanation

The `student_info.sh` script performs the following tasks:

1. **Prints a heading for the script output.**

```
echo -e "\n~~ My Computer Science Students ~~\n"
```

</br>

2. **Retrieves the first name, last name, and GPA of students with a 4.0 GPA.**

```
SELECT first_name, last_name, gpa FROM students WHERE gpa = 4.0;

```

</br>

3. **Lists all course names whose first letter is before 'D' in the alphabet.**

```
SELECT course FROM courses WHERE course < 'D';

```

</br>

4. **Retrieves the first name, last name, and GPA of students whose last name begins with 'R' or after and have a GPA greater than 3.8 or less than 2.0.**

```
SELECT first_name, last_name, gpa FROM students WHERE last_name >= 'R' AND (gpa > 3.8 OR gpa < 2.0);

```

</br>

5. **Lists the last name of students whose last name contains a case-insensitive 'sa' or has an 'r' as the second to last letter.**

```
SELECT last_name FROM students WHERE last_name ILIKE '%sa%' OR last_name ILIKE '%r_';

```

</br>

6. **Retrieves the first name, last name, and GPA of students who have not selected a major and either their first name begins with 'D' or they have a GPA greater than 3.0.**

```
SELECT first_name, last_name, gpa FROM students WHERE major_id IS NULL AND (first_name LIKE 'D%' OR gpa > 3.0);

```

</br>

7. **Lists the course name of the first five courses, in reverse alphabetical order, that have an 'e' as the second letter or end with an 's'**

```
SELECT course FROM courses WHERE course LIKE '_e%' OR course LIKE '%s' ORDER BY course DESC LIMIT 5;

```

</br>

8. **Calculates the average GPA of all students rounded to two decimal places.**

```
SELECT ROUND(AVG(gpa), 2) FROM students;

```

</br>

9. **Lists the major ID, total number of students, and average GPA for each major ID with more than one student.**

```
SELECT major_id, COUNT(*) AS number_of_students, ROUND(AVG(gpa), 2) AS average_gpa FROM students GROUP BY major_id HAVING COUNT(*) > 1;

```

</br>

10. **Lists majors that either no student is taking or has a student whose first name contains a case-insensitive 'ma'**

```
SELECT major FROM majors FULL JOIN students ON majors.major_id = students.major_id WHERE student_id IS NULL OR first_name ILIKE '%ma%' ORDER BY major;

```

</br>

11. **Lists unique courses, in reverse alphabetical order, that no student or 'Obie Hilpert' is taking.**

```
SELECT DISTINCT(course) FROM courses FULL JOIN majors_courses USING(course_id) FULL JOIN students USING(major_id) WHERE student_id IS NULL OR student_id=23 ORDER BY course DESC;

```

</br>

12. **Lists courses with only one student enrolled.**

```
SELECT course FROM courses FULL JOIN majors_courses USING(course_id) FULL JOIN students USING(major_id) GROUP BY course HAVING COUNT(DISTINCT(student_id)) = 1 ORDER BY course;

```

Each query corresponds to a specific task required to extract and manipulate data from the student database. The script checks for correct query results and moves to the next task upon completion.

## Screenshots

![Screenshot](./Screenshot_2024-07-16_183256.png)

If the database is deleted you can run this script it will create database, tables and insert the values.
