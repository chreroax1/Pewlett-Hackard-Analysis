# Pewlett-Hackard-Analysis

## Background

Pewlett-Hackard’s employee data is in csv form as previously the company have been using excel and VBA to work with the data. However, they did an upgrade to SQL. Now, using SQL we need to determine the number of retiring employees per title, and identify employees who are eligible to participate in a mentorship program. Then, we’ll write a report that summarizes your analysis and helps prepare Bobby’s manager for the “silver tsunami” as many current employees reach retirement age.

## Results

- I created a Retirement Titles table that holds all the titles of current employees who were born between January 1, 1952 and December 31, 1955.

-- Create new table for retiring employees

SELECT emp_no, first_name, last_name

INTO retirement_title

FROM employees

WHERE (birth_date BETWEEN '1952-01-01' AND '1955-12-31')

SELECT * FROM retirement_title;

- Filter the data on the birth_date column to retrieve the employees who were born between 1952 and 1955. Then, order by the employee number.

-- Use Dictinct with Orderby to remove duplicate rows

SELECT DISTINCT ON (emp_no)
emp_no,
first_name,
last_name,
title
INTO unique_title
FROM new_table
ORDER BY emp_no,title DESC
;

select * from unique_title;

--making a new table "retiring_title"

SELECT title
INTO retiring_title
FROM unique_title

-- Employee count by title

SELECT COUNT (ce.title),ce.title
FROM retiring_title as ce
GROUP BY ce.title
ORDER BY ce.count DESC
;

            --Deliverable 2: The Employees Eligible for the Mentorship Program
			
SELECT employees.emp_no,
employees.first_name,
employees.last_name,
employees.birth_date, 
dept_emp.from_date,
dept_emp.to_date,
titles.title
INTO new_table1
From employees
INNER JOIN dept_emp
ON employees.emp_no=dept_emp.emp_no
INNER JOIN titles 
ON dept_emp.emp_no = titles.emp_no
WHERE (birth_date BETWEEN '1965-01-01' AND '1965-12-31'
);

select * from new_table;

-- Use Dictinct with Orderby to remove duplicate rows

SELECT DISTINCT ON (emp_no)
emp_no,
first_name,
last_name,
birth_date,
from_date,
to_date,
title
INTO mentorship_eligibilty
FROM new_table1
ORDER BY emp_no
;

select * from mentorship_eligibilty;

## Summary

1940 employees are eligible for mentorship. However, 90398 employees are retiring. So, there are not enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees.

-- number of employees eligible for mentorship

    SELECT COUNT (ce.emp_no)

    FROM mentorship_eligibilty as ce
-- number of employees retiring

SELECT COUNT (ce.emp_no)

FROM unique_title as ce
