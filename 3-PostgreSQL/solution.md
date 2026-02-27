## Table Creation and Data Insertion

I've used appropriate data types for PostgreSQL, such as `VARCHAR` for strings and `DECIMAL` for currency.

### Table: cust

```sql
CREATE TABLE cust (
    cust_id VARCHAR(5) PRIMARY KEY,
    lname VARCHAR(50),
    fname VARCHAR(50),
    area VARCHAR(10),
    phone_no BIGINT
);

INSERT INTO cust VALUES 
('a01', 'Bayross', 'Ivan', 'sa', 6125467),
('a02', 'Saitwal', 'Vandana', 'mu', 5560379),
('a03', 'Jaguste', 'Pramada', 'da', 4563891),
('a04', 'Navindgi', 'Basu', 'ba', 6125401),
('a05', 'Sreedharan', 'Ravi', 'va', NULL),
('a06', NULL, 'Rukmini', 'gh', 5125274);

```

### Table: movie

```sql
CREATE TABLE movie (
    mv_no INT PRIMARY KEY,
    title VARCHAR(100),
    type VARCHAR(20),
    star VARCHAR(50),
    price DECIMAL(10,2)
);

INSERT INTO movie VALUES 
(1, 'bloody vengeance', 'action', 'jackie chan', 180.95),
(2, 'the firm', 'thriller', 'tom cruise', 200.00),
(3, 'pretty woman', 'romance', 'richard gere', 150.55),
(4, 'home alone', 'comedy', 'macaulay culkin', 150.00),
(5, 'the fugitive', 'thriller', 'harisson ford', 200.00),
(6, 'coma', 'suspense', 'michael douglas', 100.00),
(7, 'dracula', 'horror', 'gary oldman', 150.25),
(8, 'quick change', 'comedy', 'bill muray', 100.00),
(9, 'gone with the wind', 'drama', 'clarke gable', 200.00),
(10, 'carry on doctor', 'comedy', 'leslie phillips', 100.00);

```

### Table: invoice

```sql
CREATE TABLE invoice (
    inv_no VARCHAR(5) PRIMARY KEY,
    mv_no INT REFERENCES movie(mv_no),
    cust_id VARCHAR(5) REFERENCES cust(cust_id),
    issue_date DATE,
    return_date DATE
);

INSERT INTO invoice VALUES 
('i01', 4, 'a01', '1993-07-23', '1993-07-25'),
('i02', 3, 'a02', '1993-08-12', '1993-08-15'),
('i03', 1, 'a02', '1993-08-15', '1993-08-18'),
('i04', 6, 'a03', '1993-09-10', '1993-09-13'),
('i05', 7, 'a04', '1993-08-05', '1993-08-08'),
('i06', 2, 'a06', '1993-09-18', '1993-09-21'),
('i07', 9, 'a05', '1993-07-07', '1993-07-10'),
('i08', 9, 'a01', '1993-08-11', '1993-08-14'),
('i09', 5, 'a03', '1993-07-06', '1993-07-09'),
('i10', 8, 'a06', '1993-09-03', '1993-09-06');

```

---

## Retrieval Queries 

1. **Find out the names of all the customers:**
```sql
SELECT fname, lname FROM cust;

```


2. **Print the entire customer table:**
```sql
SELECT * FROM cust;

```


3. **Retrieve the list of fname and the area of all the customers:**
```sql
SELECT fname, area FROM cust;

```


4. **List the various movie types available from the movie table:**
```sql
SELECT DISTINCT type FROM movie;

```


5. **Find the names of all customers having 'a' as the second letter in their fnames:**
```sql
SELECT fname FROM cust WHERE fname LIKE '_a%';

```


6. **Find the lnames of all customers that begin with 's' or 'j':**
```sql
SELECT lname FROM cust WHERE lname ILIKE 's%' OR lname ILIKE 'j%';

```


7. **Find out the customers who stay in an area whose second letter is 'a':**
```sql
SELECT * FROM cust WHERE area LIKE '_a%';

```


8. **Find the list of all customers who stay in area 'da' or area 'mu' or area 'gh':**
```sql
SELECT * FROM cust WHERE area IN ('da', 'mu', 'gh');

```


9. **Print the list of customers (labeled as employees in the prompt) whose phone numbers are greater than 5550000:**
```sql
SELECT * FROM cust WHERE phone_no > 5550000;

```


10. **Print information from invoice table for customers who have been issued movies in September:**
```sql
SELECT * FROM invoice WHERE EXTRACT(MONTH FROM issue_date) = 9;

```


11. **Display the invoice table information for cust_id 'a01' and 'a02':**
```sql
SELECT * FROM invoice WHERE cust_id IN ('a01', 'a02');

```
---

## Additional Single Table Retrieval

12. **Movies of type 'action' and 'comedy':**
```sql
SELECT * FROM movie WHERE type IN ('action', 'comedy');

```


13. **Price > 150 and <= 200:**
```sql
SELECT * FROM movie WHERE price > 150 AND price <= 200;

```


14. & 15. **Cost > 150 and calculate new cost (price * 15) as 'new_price':**
```sql
SELECT title, price, (price * 15) AS new_price 
FROM movie 
WHERE price > 150;

```


15. **Movies sorted by titles:**
```sql
SELECT * FROM movie ORDER BY title;

```


16. **Names and types of all movies except horror:**
```sql
SELECT title, type FROM movie WHERE type != 'horror';

```


17. **Square root of the price:**
```sql
SELECT title, SQRT(price) FROM movie;

```


18. **Divide cost of 'home alone' by (price - 100):**
```sql
SELECT (price / (price - 100)) FROM movie WHERE title = 'home alone';

```


19. **Customers without phone numbers:**
```sql
SELECT fname, lname, area, cust_id FROM cust WHERE phone_no IS NULL;

```


20. **Customers without lname:**
```sql
SELECT fname FROM cust WHERE lname IS NULL OR lname = '';

```


21. **Movies whose stars begin with 'm':**
```sql
SELECT mv_no, title, type FROM movie WHERE star ILIKE 'm%';

```


22. **Customers with inv_no less than 'i05':**
```sql
SELECT mv_no, inv_no FROM invoice WHERE inv_no < 'i05';

```



---

## 2. Set Functions and Concatenation (24-29)

24. **Count total customers:**
```sql
SELECT COUNT(*) FROM cust;

```


25. **Total price of all movies:**
```sql
SELECT SUM(price) FROM movie;

```


26. **Average price of all movies:**
```sql
SELECT AVG(price) FROM movie;

```


27. **Max and Min prices:**
```sql
SELECT MAX(price) AS max_price, MIN(price) AS min_price FROM movie;

```


28. **Count movies with price >= 150:**
```sql
SELECT COUNT(*) FROM movie WHERE price >= 150;

```

29. **Formatted output (Concatenation):**
```sql
-- A)
SELECT 'The Invoice No. of Customer Id. ' || cust_id || ' is ' || inv_no || ' and Movie No. is ' || mv_no FROM invoice;
-- B)
SELECT cust_id || ' has taken Movie No. ' || mv_no || ' on ' || issue_date || ' and will return on ' || return_date FROM invoice;

```

---
