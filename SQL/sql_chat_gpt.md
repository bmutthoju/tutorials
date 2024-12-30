# SQL - Chat GPT #

## Give the best SQL questions for FAANG interviews. ##

Here’s a curated list of **SQL questions** tailored to challenge your knowledge and problem-solving skills, suitable for FAANG-level interviews. These questions cover a range of difficulty levels and are designed to assess your expertise in querying, optimization, and advanced SQL concepts.

---

### 1. **Basic Queries**
- **Retrieve duplicate records:**  
  Write a query to find duplicate rows in a table.
  ```sql
  SELECT column1, column2, COUNT(*) 
  FROM table_name 
  GROUP BY column1, column2 
  HAVING COUNT(*) > 1;
  ```

- **Find the second-highest salary:**  
  ```sql
  SELECT MAX(salary) 
  FROM employee 
  WHERE salary < (SELECT MAX(salary) FROM employee);
  ```

- **Count distinct values:**  
  Write a query to count the number of unique users in a table.  
  ```sql
  SELECT COUNT(DISTINCT user_id) FROM users;
  ```

---

### 2. **Intermediate Queries**
- **Employees with the highest salary in each department:**  
  ```sql
  SELECT department_id, employee_id, salary
  FROM (
      SELECT department_id, employee_id, salary,
             RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS rank
      FROM employees
  ) AS ranked
  WHERE rank = 1;
  ```

- **Find the median salary:**  
  ```sql
  SELECT AVG(salary) AS median_salary
  FROM (
      SELECT salary
      FROM employees
      ORDER BY salary
      LIMIT 2 - (SELECT COUNT(*) FROM employees) % 2 OFFSET (SELECT (COUNT(*) - 1) / 2 FROM employees)
  ) AS median;
  ```

- **Find the most frequent item:**  
  ```sql
  SELECT item_id, COUNT(*) AS frequency
  FROM sales
  GROUP BY item_id
  ORDER BY COUNT(*) DESC
  LIMIT 1;
  ```

---

### 3. **Advanced Queries**
- **Find top 3 products by revenue for each category:**  
  ```sql
  SELECT category_id, product_id, revenue
  FROM (
      SELECT category_id, product_id, revenue,
             RANK() OVER (PARTITION BY category_id ORDER BY revenue DESC) AS rank
      FROM products
  ) AS ranked
  WHERE rank <= 3;
  ```

- **Detect cyclic dependencies in a graph (using adjacency list):**  
  ```sql
  WITH RECURSIVE cycle_check AS (
      SELECT node, connected_node, ARRAY[node] AS path
      FROM graph
      UNION ALL
      SELECT g.node, g.connected_node, path || g.connected_node
      FROM cycle_check c
      JOIN graph g ON c.connected_node = g.node
      WHERE NOT g.connected_node = ANY(path)
  )
  SELECT * FROM cycle_check WHERE ARRAY_LENGTH(path, 1) > COUNT(DISTINCT path);
  ```

- **Find consecutive days of high activity (e.g., >100 events):**  
  ```sql
  SELECT user_id, event_date
  FROM (
      SELECT user_id, event_date,
             LEAD(event_date) OVER (PARTITION BY user_id ORDER BY event_date) AS next_date,
             LAG(event_date) OVER (PARTITION BY user_id ORDER BY event_date) AS prev_date
      FROM events
      WHERE activity_count > 100
  ) AS temp
  WHERE DATEDIFF(next_date, event_date) = 1 OR DATEDIFF(event_date, prev_date) = 1;
  ```

---

### 4. **Performance-Oriented Questions**
- **Optimize a slow-running query:**  
  Analyze and improve the following query:
  ```sql
  SELECT * 
  FROM large_table1 t1
  JOIN large_table2 t2 ON t1.id = t2.foreign_id
  WHERE t1.status = 'active';
  ```

- **Index usage and query optimization:**  
  Explain how you would optimize a query fetching records by `status` and `date_range`.

- **Avoiding duplicates with window functions:**  
  Write a query to fetch the latest entry for each user while avoiding duplicates.

---

### 5. **Scenario-Based Questions**
- **User retention analysis:**  
  Write a query to calculate the retention rate of users (Day N active users / Day 1 active users).  
- **Product recommendations:**  
  Find pairs of products frequently bought together from a sales dataset.  
- **Data consistency checks:**  
  Identify mismatched records between two related tables.

---

### Preparation Tips
1. Master **window functions** (e.g., `ROW_NUMBER`, `RANK`, `LEAD`, `LAG`).
2. Practice with **recursive queries** and **CTEs** for hierarchical or graph-based problems.
3. Focus on **query optimization techniques**, including indexing and partitioning.
4. Familiarize yourself with **real-world datasets** to simulate complex scenarios.
5. Use platforms like **LeetCode**, **HackerRank**, and **StrataScratch** to practice SQL interview problems.

Would you like me to expand on any of these questions or concepts?