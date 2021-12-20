# Pewlett-Hackard-Analysis

Pewlett Hackard Analysis
Overview of Project
The Goal of this project for me and Bobby was to determine the number of retiring employees per title, and identify employees who are eligible to participate in a mentorship program. Then, we were tasked with writing a report that summarizes our analysis and helps prepare Bobby’s manager for the “silver tsunami” as many current employees reach retirement age.

Deliverable 1: The Number of Retiring Employees by Title
Deliverable 2: The Employees Eligible for the Mentorship Program
Deliverable 3: A written report on the employee database analysis README.md.
Resources and Before Start Notes:
Data Source: Employee_Database_challenge.sql
Data Tools: PostgreSQL, pgAdmin




Deliverable 1: The Number of Retiring Employees by Title
Deliverable Requirements:
Using the ERD you created in this module as a reference and your knowledge of SQL queries, create a Retirement Titles table that holds all the titles of current employees who were born between January 1, 1952 and December 31, 1955. Because some employees may have multiple titles in the database—for example, due to promotions—you’ll need to use the DISTINCT ON statement to create a table that contains the most recent title of each employee. Then, use the COUNT() function to create a final table that has the number of retirement-age employees by most recent job title.

A query is written and executed to create a Retirement Titles table for employees who are born between January 1, 1952 and December 31, 1955
The Retirement Titles table is exported as retirement_titles.csv
​A query is written and executed to create a Unique Titles table that contains the employee number, first and last name, and most recent title.
The Unique Titles table is exported as unique_titles.csv
A query is written and executed to create a Retiring Titles table that contains the number of titles filled by employees who are retiring.
The Retiring Titles table is exported as retiring_titles.csv
Results with detail analysis:
A query is written and executed to create a Retirement Titles table for employees who are born between January 1, 1952 and December 31, 1955.
Image with SQL, pgAdmin & QuickDBD Code below.

Code and Image

-- Follow the instructions below to complete Deliverable 1.
SELECT e.emp_no,
       e.first_name,
       e.last_name,
       t.title,
       t.from_date,
       t.to_date
INTO retirement_titles
FROM employees as e
INNER JOIN titles as t
ON (e.emp_no = t.emp_no)
WHERE (e.birth_date BETWEEN '1952-01-01' AND '1955-12-31')
order by e.emp_no;
name-of-you-image

The Retirement Titles table is exported as retirement_titles.csv
Exported retirement_titles.csv Image below.

Code and Image

name-of-you-image

​*A query is written and executed to create a Unique Titles table that contains the employee number, first and last name, and most recent title.
Image with SQL, pgAdmin & QuickDBD Code below.

Code and Image

-- Use Dictinct with Orderby to remove duplicate rows
SELECT DISTINCT ON (emp_no) emp_no,
first_name,
last_name,
title
INTO unique_titles
FROM retirement_titles
ORDER BY emp_no, title DESC;
name-of-you-image

The Unique Titles table is exported as unique_titles.csv
Exported unique_titles.csv Image below.

Code and Image

name-of-you-image

A query is written and executed to create a Retiring Titles table that contains the number of titles filled by employees who are retiring.
Image with SQL, pgAdmin & QuickDBD Code below.

Code and Image

-- Retrieve the number of employees by their most recent job title who are about to retire.
SELECT COUNT(ut.emp_no),
ut.title
INTO retiring_titles
FROM unique_titles as ut
GROUP BY title 
ORDER BY COUNT(title) DESC;
name-of-you-image

The Retiring Titles table is exported as retiring_titles.csv
Exported retiring_titles.csv Image below.

Code and Image

name-of-you-image

Deliverable 2: The Employees Eligible for the Mentorship Program
Deliverable Requirements:
Using the ERD you created in this module as a reference and your knowledge of SQL queries, create a mentorship-eligibility table that holds the current employees who were born between January 1, 1965 and December 31, 1965.

A query is written and executed to create a Mentorship Eligibility table for current employees who were born between January 1, 1965 and December 31, 1965.
The Mentorship Eligibility table is exported and saved as mentorship_eligibilty.csv
Results with detail analysis:
A query is written and executed to create a Mentorship Eligibility table for current employees who were born between January 1, 1965 and December 31, 1965.
Image with SQL, pgAdmin & QuickDBD Code below.

Code and Image

-- Write a query to create a Mentorship Eligibility table that holds the employees who are eligible to participate in a mentorship program.
SELECT DISTINCT ON(e.emp_no) e.emp_no, 
    e.first_name, 
    e.last_name, 
    e.birth_date,
    de.from_date,
    de.to_date,
    t.title
INTO mentorship_eligibilty
FROM employees as e
Left outer Join dept_emp as de
ON (e.emp_no = de.emp_no)
Left outer Join titles as t
ON (e.emp_no = t.emp_no)
WHERE (e.birth_date BETWEEN '1965-01-01' AND '1965-12-31')
ORDER BY e.emp_no;
name-of-you-image

The Mentorship Eligibility table is exported and saved as mentorship_eligibilty.csv"
Exported retiring_titles.csv Image below.

Code and Image

name-of-you-image

Deliverable 3: A written report on the employee database analysis
The analysis should contain the following:
Overview of the analysis
Explain the purpose of this analysis.:

In this deliverable, Bobby was tasked to determine the number of retiring employees per title, and identify employees who are eligible to participate in a mentorship program. Then, you’ll write a report that summarizes your analysis and helps prepare Bobby’s manager for the “silver tsunami” as many current employees reach retirement age.

Results
Provide a bulleted list with four major points from the two analysis deliverables. Use images as support where needed:

From the finding of the eligible retirees, High Percentage of the workforce could retire at any given time.
From the job titles of the eligible retirees, the breakdown is below.
32,452 Staff
29,415 Senior Engineer
14,221 Engineer
8,047 Senior Staff
4,502 Technique Leader
1,761 Assistant Engineer
Image Below

name-of-you-image

Summary
When Looking at the upcoming "Silver Tsunami" and trying to decideif Pewlett Hackard is in a good postion to handle it we can break dwon the question into two questions and answers.

1) How many roles will need to be filled as the "silver tsunami" begins to make an impact?.

90,398 roles are in urgent need to be filled out as soon as the workforce starts retiring at any given time.

2) Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?

No, we have 1,940 employees who are eligible to participate in a mentorship program.

name-of-you-image
