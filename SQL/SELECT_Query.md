# SELECT Deep Dive

SELECT is the most frequently used SQL command. It is used to retrieve data from a table.

Basic syntax:

```sql
SELECT column1, column2
FROM table_name;
```

---

# Selecting All Columns

```sql
SELECT * FROM employees;
```

Returns every column in the table.

Avoid using `*` in production queries because:

* Slower performance
* Fetches unnecessary data
* Breaks when schema changes

Better approach:

```sql
SELECT id, name, salary FROM employees;
```

---

# Column Aliases

Aliases rename columns in output.

```sql
SELECT name AS employee_name
FROM employees;
```

You can also omit `AS`:

```sql
SELECT name employee_name
FROM employees;
```

---

# Aliases for Calculated Columns

```sql
SELECT name, salary * 12 AS yearly_salary
FROM employees;
```

---

# Arithmetic Operations in SELECT

You can perform calculations:

```sql
SELECT name, salary + 5000 AS bonus_salary
FROM employees;
```

```sql
SELECT name, salary * 1.10 AS increased_salary
FROM employees;
```

---

# Selecting Distinct Values

Removes duplicates.

```sql
SELECT DISTINCT department
FROM employees;
```

Without DISTINCT:

```text
IT
IT
HR
```

With DISTINCT:

```text
IT
HR
```

---

# Combining Columns

```sql
SELECT name || ' - ' || department AS employee_info
FROM employees;
```

(MySQL alternative)

```sql
SELECT CONCAT(name, ' - ', department) AS employee_info
FROM employees;
```

---

# Literal Values in SELECT

```sql
SELECT name, 'ACTIVE' AS status
FROM employees;
```

---

# Using Expressions

```sql
SELECT name, salary * 0.2 AS tax
FROM employees;
```

---

# Using Functions

```sql
SELECT UPPER(name)
FROM employees;
```

```sql
SELECT LOWER(name)
FROM employees;
```

```sql
SELECT LENGTH(name)
FROM employees;
```

---

# SELECT Without Table

```sql
SELECT 1 + 1;
```

Useful for testing expressions.

---

# Order of Execution (Important)

Even though SELECT appears first:

SQL executes in this order:

1. FROM
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. ORDER BY
7. LIMIT

---

# Example Demonstrating Order

```sql
SELECT name, salary * 12 AS yearly
FROM employees
WHERE salary > 50000;
```

Execution:

1. FROM employees
2. WHERE salary > 50000
3. SELECT calculation

---

# Multiple Expressions

```sql
SELECT 
    name,
    salary,
    salary * 12 AS yearly,
    salary * 0.10 AS bonus
FROM employees;
```

---

# Selecting Constant + Column

```sql
SELECT 
    'Employee:' AS label,
    name
FROM employees;
```

---

# Key Interview Points

* Avoid SELECT *
* Use aliases
* Use expressions
* Use DISTINCT properly
* Understand execution order
* Use functions

---

# Common Mistakes

Wrong:

```sql
SELECT salary * 12 yearly FROM employees;
```

Correct:

```sql
SELECT salary * 12 AS yearly FROM employees;
```

---

Wrong:

```sql
SELECT DISTINCT name, department FROM employees;
```

This removes duplicates of BOTH columns, not individually.

---

# Mental Model

SELECT is used to:

* Choose columns
* Transform data
* Calculate values
* Rename output
* Remove duplicates
