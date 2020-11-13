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

## Summary

1940 employees are eligible for mentorship. However, 90398 employees are retiring. So, there are not enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees.

-- number of employees eligible for mentorship

    SELECT COUNT (ce.emp_no)

    FROM mentorship_eligibilty as ce
-- number of employees retiring

SELECT COUNT (ce.emp_no)

FROM unique_title as ce