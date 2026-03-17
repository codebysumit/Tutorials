---
title: 03-Relational Algebra (Project Operation)
---

# Project Operation $ (\pi) $ — Relational Algebra (Part #3)

## Definition

The **Project Operation** is a fundamental unary operation in relational algebra used to select specific **columns (attributes)** from a relation while eliminating all other columns. It works vertically — meaning it filters specific **columns** while keeping **all rows** (after removing duplicates).

> In simple terms, the Project Operation is equivalent to the `SELECT column_name` clause in SQL. It retrieves only the specified attributes from a relation and automatically removes **duplicate tuples** from the result.

---

## Notation

$$
\pi_{A_1, A_2, \dots, A_n}(R)
$$

$$
\pi_{\text{attribute\_list}}(\text{Relation})
$$

Where:

- $ \pi $ (pi) — denotes the **project operation**
- $ A_1, A_2, \dots, A_n $ — are the **attributes (columns)** to be selected
- $ R $ — is the **relation** (table) on which the operation is applied

---

## Properties of Project Operation

- The result of a project operation contains **only the specified columns** from the original relation.
- The **degree** (number of columns) of the result is **less than or equal to** the original relation.
- The **cardinality** (number of rows) of the result may be **less than or equal to** the original relation, because **duplicate tuples are automatically removed**.
- Project operation is **NOT commutative** in general:
  $$
  \pi_{A}(\pi_{B}(R)) \neq \pi_{B}(\pi_{A}(R))
  $$
- However, a **cascade of projections** simplifies to the last (innermost) projection — provided attributes are a subset:
  $$
  \pi_{A}(\pi_{A,B}(R)) = \pi_{A}(R)
  $$
- Project operation can be **combined with Select** to filter both rows and columns simultaneously.

---

## Difference Between Select and Project

| Feature            | Select $ (\sigma) $ | Project $ (\pi) $           |
| ------------------ | ------------------- | --------------------------- |
| Filters            | Rows (tuples)       | Columns (attributes)        |
| Direction          | Horizontal          | Vertical                    |
| Condition Required | Yes (predicate)     | No (only attribute list)    |
| Removes Duplicates | No                  | Yes                         |
| SQL Equivalent     | `WHERE` clause      | `SELECT column_name` clause |

---

## Example Table — Students

The following **Students** relation will be used for all examples below:

| student_id | name         | age | gender | department | marks |
| ---------- | ------------ | --- | ------ | ---------- | ----- |
| 101        | Sumit Das    | 21  | M      | CSE        | 85    |
| 102        | Sumana Das   | 26  | F      | ECE        | 72    |
| 103        | Ravi Kumar   | 22  | M      | CSE        | 90    |
| 104        | Priya Sharma | 24  | F      | IT         | 68    |
| 105        | Anik Ghosh   | 21  | M      | ECE        | 55    |
| 106        | Neha Singh   | 23  | F      | CSE        | 78    |

---

## Part 1 — Project Operation Examples

---

### Example 1 — Single Attribute Projection

**Question:** Retrieve only the **name** of all students.

**Relational Algebra Expression:**

$$
\pi_{\text{name}}(\text{Students})
$$

**Solution:** The project operation scans every tuple in the Students relation and returns only the `name` column. All other columns are discarded.

**Output Relation:**

| name         |
| ------------ |
| Sumit Das    |
| Sumana Das   |
| Ravi Kumar   |
| Priya Sharma |
| Anik Ghosh   |
| Neha Singh   |

**Equivalent SQL Query:**

```sql
SELECT name
FROM Students;
```

---

### Example 2 — Multiple Attribute Projection

**Question:** Retrieve the **name**, **department**, and **marks** of all students.

**Relational Algebra Expression:**

$$
\pi_{\text{name, department, marks}}(\text{Students})
$$

**Solution:** The project operation returns only the three specified columns — `name`, `department`, and `marks` — for every tuple in the relation.

**Output Relation:**

| name         | department | marks |
| ------------ | ---------- | ----- |
| Sumit Das    | CSE        | 85    |
| Sumana Das   | ECE        | 72    |
| Ravi Kumar   | CSE        | 90    |
| Priya Sharma | IT         | 68    |
| Anik Ghosh   | ECE        | 55    |
| Neha Singh   | CSE        | 78    |

**Equivalent SQL Query:**

```sql
SELECT name, department, marks
FROM Students;
```

---

### Example 3 — Projection with Duplicate Elimination

**Question:** Retrieve the **department** values of all students (duplicates must be removed).

**Relational Algebra Expression:**

$$
\pi_{\text{department}}(\text{Students})
$$

**Solution:** The project operation returns the `department` column. Since relational algebra automatically removes duplicate tuples, repeated department names such as `CSE` and `ECE` appear only once in the result.

**Output Relation:**

| department |
| ---------- |
| CSE        |
| ECE        |
| IT         |

> **Note:** Without duplicate elimination, there would be 6 rows (CSE appears 3 times, ECE appears 2 times). Relational algebra reduces these to 3 distinct rows.

**Equivalent SQL Query:**

```sql
SELECT DISTINCT department
FROM Students;
```

---

### Example 4 — Projection of Two Attributes with Duplicates

**Question:** Retrieve the **gender** and **department** of all students (duplicates removed).

**Relational Algebra Expression:**

$$
\pi_{\text{gender, department}}(\text{Students})
$$

**Solution:** The project operation returns only `gender` and `department`. The combination of `(M, CSE)` appears for both Sumit Das (101) and Ravi Kumar (103), so it appears only once after duplicate removal.

**Output Relation:**

| gender | department |
| ------ | ---------- |
| M      | CSE        |
| F      | ECE        |
| F      | IT         |
| M      | ECE        |
| F      | CSE        |

**Equivalent SQL Query:**

```sql
SELECT DISTINCT gender, department
FROM Students;
```

---

## Part 2 — Project + Select (Combined Operation) Examples

When **Select** $ (\sigma) $ and **Project** $ (\pi) $ are combined, the Select is applied **first** (inner operation) to filter rows, and then Project is applied (outer operation) to filter columns. This is the most practical and commonly used combination in relational algebra.

**General Form:**

$$
\pi_{\text{attribute\_list}}(\sigma_{\text{condition}}(\text{Relation}))
$$

---

### Example 5 — Project + Select (Single Condition)

**Question:** Retrieve the **name** and **marks** of all students who belong to the **CSE** department.

**Relational Algebra Expression:**

$$
\pi_{\text{name, marks}}(\sigma_{\text{department} = \text{'CSE'}}(\text{Students}))
$$

**Solution:**

**Step 1 — Apply Select:** Filter tuples where `department = 'CSE'`.

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 101        | Sumit Das  | 21  | M      | CSE        | 85    |
| 103        | Ravi Kumar | 22  | M      | CSE        | 90    |
| 106        | Neha Singh | 23  | F      | CSE        | 78    |

**Step 2 — Apply Project:** Keep only `name` and `marks` columns.

**Output Relation:**

| name       | marks |
| ---------- | ----- |
| Sumit Das  | 85    |
| Ravi Kumar | 90    |
| Neha Singh | 78    |

**Equivalent SQL Query:**

```sql
SELECT name, marks
FROM Students
WHERE department = 'CSE';
```

---

### Example 6 — Project + Select (Comparison Condition)

**Question:** Retrieve the **name**, **age**, and **department** of all students whose **marks are greater than or equal to 72**.

**Relational Algebra Expression:**

$$
\pi_{\text{name, age, department}}(\sigma_{\text{marks} \geq 72}(\text{Students}))
$$

**Solution:**

**Step 1 — Apply Select:** Filter tuples where `marks >= 72`.

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 101        | Sumit Das  | 21  | M      | CSE        | 85    |
| 102        | Sumana Das | 26  | F      | ECE        | 72    |
| 103        | Ravi Kumar | 22  | M      | CSE        | 90    |
| 106        | Neha Singh | 23  | F      | CSE        | 78    |

**Step 2 — Apply Project:** Keep only `name`, `age`, and `department` columns.

**Output Relation:**

| name       | age | department |
| ---------- | --- | ---------- |
| Sumit Das  | 21  | CSE        |
| Sumana Das | 26  | ECE        |
| Ravi Kumar | 22  | CSE        |
| Neha Singh | 23  | CSE        |

**Equivalent SQL Query:**

```sql
SELECT name, age, department
FROM Students
WHERE marks >= 72;
```

---

### Example 7 — Project + Select (AND Condition)

**Question:** Retrieve the **student_id**, **name**, and **marks** of all **female** students with **marks greater than 70**.

**Relational Algebra Expression:**

$$
\pi_{\text{student\_id, name, marks}}(\sigma_{\text{gender} = \text{'F'} \land \text{marks} > 70}(\text{Students}))
$$

**Solution:**

**Step 1 — Apply Select:** Filter tuples where `gender = 'F'` AND `marks > 70`.

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 102        | Sumana Das | 26  | F      | ECE        | 72    |
| 106        | Neha Singh | 23  | F      | CSE        | 78    |

**Step 2 — Apply Project:** Keep only `student_id`, `name`, and `marks` columns.

**Output Relation:**

| student_id | name       | marks |
| ---------- | ---------- | ----- |
| 102        | Sumana Das | 72    |
| 106        | Neha Singh | 78    |

**Equivalent SQL Query:**

```sql
SELECT student_id, name, marks
FROM Students
WHERE gender = 'F' AND marks > 70;
```

---

### Example 8 — Project + Select (OR Condition)

**Question:** Retrieve the **name** and **department** of all students who are either from the **IT** department or have **marks less than 60**.

**Relational Algebra Expression:**

$$
\pi_{\text{name, department}}(\sigma_{\text{department} = \text{'IT'} \lor \text{marks} < 60}(\text{Students}))
$$

**Solution:**

**Step 1 — Apply Select:** Filter tuples where `department = 'IT'` OR `marks < 60`.

| student_id | name         | age | gender | department | marks |
| ---------- | ------------ | --- | ------ | ---------- | ----- |
| 104        | Priya Sharma | 24  | F      | IT         | 68    |
| 105        | Anik Ghosh   | 21  | M      | ECE        | 55    |

**Step 2 — Apply Project:** Keep only `name` and `department` columns.

**Output Relation:**

| name         | department |
| ------------ | ---------- |
| Priya Sharma | IT         |
| Anik Ghosh   | ECE        |

**Equivalent SQL Query:**

```sql
SELECT name, department
FROM Students
WHERE department = 'IT' OR marks < 60;
```

---

### Example 9 — Project + Select (NOT Condition)

**Question:** Retrieve the **name**, **gender**, and **marks** of all students who are **NOT** from the **ECE** department.

**Relational Algebra Expression:**

$$
\pi_{\text{name, gender, marks}}(\sigma_{\neg(\text{department} = \text{'ECE'})}(\text{Students}))
$$

**Solution:**

**Step 1 — Apply Select:** Filter tuples where `department ≠ 'ECE'`.

| student_id | name         | age | gender | department | marks |
| ---------- | ------------ | --- | ------ | ---------- | ----- |
| 101        | Sumit Das    | 21  | M      | CSE        | 85    |
| 103        | Ravi Kumar   | 22  | M      | CSE        | 90    |
| 104        | Priya Sharma | 24  | F      | IT         | 68    |
| 106        | Neha Singh   | 23  | F      | CSE        | 78    |

**Step 2 — Apply Project:** Keep only `name`, `gender`, and `marks` columns.

**Output Relation:**

| name         | gender | marks |
| ------------ | ------ | ----- |
| Sumit Das    | M      | 85    |
| Ravi Kumar   | M      | 90    |
| Priya Sharma | F      | 68    |
| Neha Singh   | F      | 78    |

**Equivalent SQL Query:**

```sql
SELECT name, gender, marks
FROM Students
WHERE department <> 'ECE';
```

---

## Summary

| Aspect               | Detail                                                                            |
| -------------------- | --------------------------------------------------------------------------------- |
| Operation Type       | Unary                                                                             |
| Symbol               | $ \pi $                                                                           |
| Input                | A relation (table)                                                                |
| Output               | A relation with only the specified columns (duplicates removed)                   |
| Rows in Result       | Less than or equal to original (due to duplicate elimination)                     |
| Columns in Result    | Only the specified attributes                                                     |
| SQL Equivalent       | `SELECT DISTINCT column_name` clause                                              |
| Commutative?         | No                                                                                |
| Combined with Select | $ \pi*{\text{attrs}}(\sigma*{\text{condition}}(R)) $ — Select first, then Project |
