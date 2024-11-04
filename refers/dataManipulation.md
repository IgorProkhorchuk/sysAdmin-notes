Data Manipulation Language (DML) in PostgreSQL includes commands to retrieve, insert, update, and delete data within database tables. This is a core part of SQL operations in PostgreSQL, allowing users to handle data dynamically.

### Overview of DML Commands in PostgreSQL

1. **SELECT** - Retrieve data from tables.
2. **INSERT** - Add new data to tables.
3. **UPDATE** - Modify existing data in tables.
4. **DELETE** - Remove data from tables.

Let’s examine each of these commands in detail.

---

### 1. **SELECT** - Retrieving Data

The `SELECT` statement retrieves data from one or more tables. It allows you to specify columns, filter results, and sort or group data.

#### Basic Syntax:
```sql
SELECT column1, column2, ... FROM table_name;
```

#### Example:
```sql
SELECT first_name, last_name FROM employees;
```

#### Additional Clauses and Options:

- **WHERE**: Filters rows based on conditions.
  ```sql
  SELECT first_name, last_name FROM employees WHERE department_id = 5;
  ```

- **ORDER BY**: Sorts results by columns.
  ```sql
  SELECT first_name, last_name FROM employees ORDER BY last_name ASC;
  ```

- **GROUP BY**: Groups rows sharing a property and allows for aggregate functions like `SUM`, `COUNT`, etc.
  ```sql
  SELECT department_id, COUNT(employee_id) AS employee_count FROM employees GROUP BY department_id;
  ```

- **JOIN**: Combines rows from multiple tables based on a related column.
  ```sql
  SELECT e.first_name, e.last_name, d.department_name
  FROM employees e
  JOIN departments d ON e.department_id = d.department_id;
  ```

- **Aggregations**: Use aggregate functions like `SUM`, `AVG`, `MIN`, `MAX`, `COUNT`.
  ```sql
  SELECT department_id, AVG(salary) AS average_salary FROM employees GROUP BY department_id;
  ```

---

### 2. **INSERT** - Adding Data

The `INSERT` statement adds new rows to a table. Each `INSERT` operation can specify values for one or more columns.

#### Basic Syntax:
```sql
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);
```

#### Example:
```sql
INSERT INTO employees (first_name, last_name, department_id, hire_date, salary)
VALUES ('Jane', 'Doe', 3, '2024-11-01', 55000.00);
```

#### Inserting Multiple Rows:
You can add multiple rows in a single `INSERT` statement.
```sql
INSERT INTO employees (first_name, last_name, department_id, hire_date, salary)
VALUES 
    ('Alice', 'Smith', 2, '2024-10-20', 60000.00),
    ('Bob', 'Johnson', 4, '2024-10-21', 62000.00);
```

#### Insert with `DEFAULT`:
You can omit columns that have a `DEFAULT` value or explicitly use the `DEFAULT` keyword.
```sql
INSERT INTO employees (first_name, last_name, department_id)
VALUES ('Chris', 'Evans', DEFAULT);
```

#### Returning Values:
The `RETURNING` clause allows you to return data from the inserted row(s).
```sql
INSERT INTO employees (first_name, last_name, department_id, hire_date, salary)
VALUES ('David', 'Lee', 1, '2024-11-04', 59000.00)
RETURNING employee_id, hire_date;
```

---

### 3. **UPDATE** - Modifying Data

The `UPDATE` statement modifies existing rows in a table. You can update one or more columns, and optionally, use a `WHERE` clause to specify which rows to update.

#### Basic Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition;
```

#### Example:
```sql
UPDATE employees
SET salary = salary * 1.05
WHERE department_id = 2;
```

#### Update Multiple Columns:
```sql
UPDATE employees
SET salary = salary + 1000, last_name = 'Smith'
WHERE employee_id = 1;
```

#### Using `WHERE` with `UPDATE`:
If no `WHERE` condition is specified, all rows in the table will be updated.
```sql
UPDATE employees
SET hire_date = CURRENT_DATE;
```

#### Returning Values:
Similar to `INSERT`, you can use `RETURNING` to retrieve the updated values.
```sql
UPDATE employees
SET salary = salary * 1.10
WHERE department_id = 3
RETURNING employee_id, salary;
```

---

### 4. **DELETE** - Removing Data

The `DELETE` statement removes rows from a table. Be cautious when using `DELETE` without a `WHERE` clause, as it will delete all rows in the table.

#### Basic Syntax:
```sql
DELETE FROM table_name WHERE condition;
```

#### Example:
```sql
DELETE FROM employees
WHERE employee_id = 10;
```

#### Deleting Multiple Rows:
Use `WHERE` conditions to specify which rows to delete.
```sql
DELETE FROM employees
WHERE department_id = 4;
```

#### Returning Values:
You can use `RETURNING` to get data from the deleted rows.
```sql
DELETE FROM employees
WHERE employee_id = 15
RETURNING first_name, last_name;
```

---

### 5. **Advanced Data Manipulation**

#### Using CTEs (Common Table Expressions)
Common Table Expressions (CTEs) allow you to create temporary result sets to simplify complex queries.

##### Example:
```sql
WITH dept_avg_salary AS (
    SELECT department_id, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
)
SELECT e.first_name, e.last_name, d.avg_salary
FROM employees e
JOIN dept_avg_salary d ON e.department_id = d.department_id
WHERE e.salary > d.avg_salary;
```

#### Using `UPSERT` (Insert or Update)
PostgreSQL has the `ON CONFLICT` clause for handling duplicate key violations.

##### Example:
```sql
INSERT INTO employees (employee_id, first_name, last_name, salary)
VALUES (1, 'John', 'Doe', 60000)
ON CONFLICT (employee_id) DO UPDATE
SET salary = EXCLUDED.salary;
```

In this example, if an `employee_id` conflict occurs, the row is updated instead of inserted.

#### Using Subqueries in DML
Subqueries can be used to provide values for `INSERT`, `UPDATE`, or `DELETE` statements.

##### Example:
```sql
UPDATE employees
SET salary = salary * 1.10
WHERE department_id = (
    SELECT department_id FROM departments WHERE department_name = 'Sales'
);
```

#### Using Window Functions with `SELECT`
Window functions allow you to perform calculations across a set of table rows related to the current row.

##### Example:
```sql
SELECT first_name, last_name, salary,
       RANK() OVER (ORDER BY salary DESC) AS salary_rank
FROM employees;
```

#### Using JSON and JSONB Columns
PostgreSQL supports JSON and JSONB types, allowing you to store and manipulate JSON data.

##### Inserting JSON Data:
```sql
INSERT INTO employee_details (employee_id, info)
VALUES (1, '{"first_name": "Jane", "last_name": "Doe", "age": 30}'::JSONB);
```

##### Querying JSON Data:
```sql
SELECT info->>'first_name' AS first_name
FROM employee_details
WHERE info->>'last_name' = 'Doe';
```

#### Working with Arrays
PostgreSQL supports array data types, and you can perform operations on arrays.

##### Example:
```sql
SELECT first_name, last_name
FROM employees
WHERE department_id = ANY (ARRAY[2, 3, 5]);
```

---

### Summary

**DML operations** in PostgreSQL offer robust options for managing data effectively:
- `SELECT` allows for flexible data retrieval, filtering, sorting, and grouping.
- `INSERT` adds rows to a table, supporting single or multiple row inserts, defaults, and returning values.
- `UPDATE` modifies existing rows, with powerful conditional updates and value returns.
- `DELETE` removes rows, with control over which rows to delete and options to return affected data.

**Advanced features** like CTEs, `ON CONFLICT` handling, subqueries, window functions, and JSON/Array data manipulation provide powerful tools to enhance and optimize data management in PostgreSQL.