---
title: 06-Relational Algebra (Cartesian Product Operation)
---

# Cartesian Product Operation $ (\times) $ — Relational Algebra (Part #6)

## Definition

The **Cartesian Product Operation** (also known as **Cross Product** or **Cross Join**) is a fundamental binary operation in relational algebra that combines **every tuple** of the first relation with **every tuple** of the second relation. It produces all possible ordered pairs of tuples from the two relations — regardless of any matching condition.

> In simple terms, the Cartesian Product is equivalent to the `CROSS JOIN` keyword in SQL. If the first relation has $ m $ tuples and the second has $ n $ tuples, the result will always contain exactly $ m \times n $ tuples.

---

## Mathematical Formula

If $ P $ and $ Q $ are two relations, then the Cartesian Product of $ P $ and $ Q $ is defined as:

$$
R = P \times Q
$$

$$
R = \{ \, (t_1, t_2) \mid t_1 \in P \quad \text{AND} \quad t_2 \in Q \, \}
$$

Where:
- $ (t_1, t_2) $ — represents an **ordered pair** of tuples, one from each relation
- $ t_1 $ — is a tuple from the **first relation** $ P $
- $ t_2 $ — is a tuple from the **second relation** $ Q $
- $ R $ — is the **resulting relation** containing all possible combinations of tuples from $ P $ and $ Q $

> Every tuple from $ P $ is paired with **every** tuple from $ Q $. If $ P $ has $ m $ tuples and $ Q $ has $ n $ tuples, then $ R = P \times Q $ will have exactly $ m \times n $ tuples.

---

### Formula Example

**Relation P — Department:**

| dept\_id | dept\_name  |
| -------- | ----------- |
| D1       | CSE         |
| D2       | ECE         |

**Relation Q — Grade:**

| grade | remark    |
| ----- | --------- |
| A     | Excellent |
| B     | Good      |
| C     | Average   |

**Applying:** $ R = P \times Q $

> $ P $ has **2 tuples** and $ Q $ has **3 tuples** — so the result will have $ 2 \times 3 = $ **6 tuples**.

**Result Relation $ R = P \times Q $:**

| dept\_id | dept\_name | grade | remark    |
| -------- | ---------- | ----- | --------- |
| D1       | CSE        | A     | Excellent |
| D1       | CSE        | B     | Good      |
| D1       | CSE        | C     | Average   |
| D2       | ECE        | A     | Excellent |
| D2       | ECE        | B     | Good      |
| D2       | ECE        | C     | Average   |

> Each row of $ P $ (D1-CSE, D2-ECE) is combined with **every** row of $ Q $ (A, B, C) — producing all 6 possible combinations.

---

## Notation

$$
R = P \times Q
$$

$$
\text{Relation}\_1 \times \text{Relation}\_2
$$

Where:
- $ \times $ — denotes the **Cartesian product operation**
- $ P $ — is the **first relation** (table)
- $ Q $ — is the **second relation** (table)
- $ R $ — is the **resulting relation**

---

## Degree and Cardinality of Result

| Property      | Formula                        | Meaning                                              |
| ------------- | ------------------------------ | ---------------------------------------------------- |
| **Degree**    | $ \deg(P) + \deg(Q) $          | Number of columns = columns of $ P $ + columns of $ Q $ |
| **Cardinality** | $ \|P\| \times \|Q\| $       | Number of rows = rows of $ P $ × rows of $ Q $       |

> **Example:** If $ P $ has **3 columns and 4 rows**, and $ Q $ has **2 columns and 5 rows**, then $ P \times Q $ will have **5 columns** and **20 rows**.

---

## Difference Between Cartesian Product and Other Operations

| Feature             | Select $ (\sigma) $         | Project $ (\pi) $           | Union $ (\cup) $               | Cartesian Product $ (\times) $          |
| ------------------- | --------------------------- | --------------------------- | ------------------------------ | --------------------------------------- |
| Operation Type      | Unary                       | Unary                       | Binary                         | Binary                                  |
| Filters             | Rows                        | Columns                     | Combines rows                  | Combines all rows of two relations      |
| Condition Required  | Yes                         | No                          | No                             | No                                      |
| Union Compatible    | N/A                         | N/A                         | Yes (required)                 | No (not required)                       |
| Result Size         | $ \leq \|R\| $              | $ \leq \|R\| $              | $ \leq \|P\| + \|Q\| $        | Exactly $ \|P\| \times \|Q\| $          |
| SQL Equivalent      | `WHERE`                     | `SELECT col`                | `UNION`                        | `CROSS JOIN`                            |

---

## Properties of Cartesian Product

- **Commutative** (in terms of data, with column reordering):
$$
P \times Q \approx Q \times P
$$
> The tuples are the same but the **column order** differs — $ P \times Q $ places $ P $'s columns first, while $ Q \times P $ places $ Q $'s columns first.

- **Associative:**
$$
(P \times Q) \times T = P \times (Q \times T)
$$

- **NOT Union-Compatible Required:** Unlike Union and Set Difference, Cartesian Product does **not** require the two relations to have the same degree or compatible domains.

- **Cardinality:**
$$
|P \times Q| = |P| \times |Q|
$$

- **Degree:**
$$
\deg(P \times Q) = \deg(P) + \deg(Q)
$$

- **Combined with Select:** The Cartesian Product combined with a Select condition $ (\sigma) $ forms the basis of the **Join** operation:
$$
\sigma_{\text{condition}}(P \times Q) \equiv P \bowtie Q
$$

---

## Example Tables

Two separate relations are used throughout all examples below — a **Students** table and a **Courses** table — representing a university enrollment system.

### Relation — Students

| student\_id | student\_name  | dept |
| ----------- | -------------- | ---- |
| 101         | Aarav Sharma   | CSE  |
| 102         | Diya Mehta     | ECE  |
| 103         | Rohan Das      | IT   |
| 104         | Sneha Bose     | CSE  |

### Relation — Courses

| course\_id | course\_name        | credits |
| ---------- | ------------------- | ------- |
| C01        | Data Structures     | 4       |
| C02        | Digital Electronics | 3       |
| C03        | Database Systems    | 4       |

> **Key Observation:** Students has **4 tuples** and **3 columns**. Courses has **3 tuples** and **3 columns**. So $ \text{Students} \times \text{Courses} $ will produce $ 4 \times 3 = $ **12 tuples** with $ 3 + 3 = $ **6 columns**.

---

## Examples

---

### Example 1 — Basic Cartesian Product

**Question:** Find all possible combinations of students and courses — i.e., every student paired with every course.

**Relational Algebra Expression:**

$$
\text{Students} \times \text{Courses}
$$

**Solution:** Every tuple in Students is paired with every tuple in Courses. Student Aarav Sharma (101) gets combined with all 3 courses, then Diya Mehta (102) gets combined with all 3 courses, and so on — producing $ 4 \times 3 = 12 $ tuples.

**Students:**

| student\_id | student\_name | dept |
| ----------- | ------------- | ---- |
| 101         | Aarav Sharma  | CSE  |
| 102         | Diya Mehta    | ECE  |
| 103         | Rohan Das     | IT   |
| 104         | Sneha Bose    | CSE  |

**Courses:**

| course\_id | course\_name        | credits |
| ---------- | ------------------- | ------- |
| C01        | Data Structures     | 4       |
| C02        | Digital Electronics | 3       |
| C03        | Database Systems    | 4       |

**Output Relation $ \text{Students} \times \text{Courses} $ (12 tuples):**

| student\_id | student\_name | dept | course\_id | course\_name        | credits |
| ----------- | ------------- | ---- | ---------- | ------------------- | ------- |
| 101         | Aarav Sharma  | CSE  | C01        | Data Structures     | 4       |
| 101         | Aarav Sharma  | CSE  | C02        | Digital Electronics | 3       |
| 101         | Aarav Sharma  | CSE  | C03        | Database Systems    | 4       |
| 102         | Diya Mehta    | ECE  | C01        | Data Structures     | 4       |
| 102         | Diya Mehta    | ECE  | C02        | Digital Electronics | 3       |
| 102         | Diya Mehta    | ECE  | C03        | Database Systems    | 4       |
| 103         | Rohan Das     | IT   | C01        | Data Structures     | 4       |
| 103         | Rohan Das     | IT   | C02        | Digital Electronics | 3       |
| 103         | Rohan Das     | IT   | C03        | Database Systems    | 4       |
| 104         | Sneha Bose    | CSE  | C01        | Data Structures     | 4       |
| 104         | Sneha Bose    | CSE  | C02        | Digital Electronics | 3       |
| 104         | Sneha Bose    | CSE  | C03        | Database Systems    | 4       |

**Equivalent SQL Query:**

```sql
SELECT *
FROM Students
CROSS JOIN Courses;
```

---

### Example 2 — Cartesian Product + Select (Simulating a Join)

**Question:** From all possible student-course combinations, retrieve only the rows where the student is from the **CSE** department.

**Relational Algebra Expression:**

$$
\sigma_{\text{dept} = \text{'CSE'}}(\text{Students} \times \text{Courses})
$$

**Solution:**

**Step 1 — Cartesian Product:** Generate all $ 4 \times 3 = 12 $ combinations (same as Example 1).

**Step 2 — Apply Select:** Filter only those rows where `dept = 'CSE'`. Only Aarav Sharma (101) and Sneha Bose (104) are from CSE — each paired with 3 courses gives $ 2 \times 3 = 6 $ rows.

**Output Relation:**

| student\_id | student\_name | dept | course\_id | course\_name        | credits |
| ----------- | ------------- | ---- | ---------- | ------------------- | ------- |
| 101         | Aarav Sharma  | CSE  | C01        | Data Structures     | 4       |
| 101         | Aarav Sharma  | CSE  | C02        | Digital Electronics | 3       |
| 101         | Aarav Sharma  | CSE  | C03        | Database Systems    | 4       |
| 104         | Sneha Bose    | CSE  | C01        | Data Structures     | 4       |
| 104         | Sneha Bose    | CSE  | C02        | Digital Electronics | 3       |
| 104         | Sneha Bose    | CSE  | C03        | Database Systems    | 4       |

**Equivalent SQL Query:**

```sql
SELECT *
FROM Students
CROSS JOIN Courses
WHERE Students.dept = 'CSE';
```

---

### Example 3 — Cartesian Product + Select (Filtering by Credits)

**Question:** Retrieve all student-course combinations where the course has **4 credits**.

**Relational Algebra Expression:**

$$
\sigma_{\text{credits} = 4}(\text{Students} \times \text{Courses})
$$

**Solution:**

**Step 1 — Cartesian Product:** Generate all $ 4 \times 3 = 12 $ combinations.

**Step 2 — Apply Select:** Filter only rows where `credits = 4`. Only C01 (Data Structures) and C03 (Database Systems) have 4 credits — each paired with 4 students gives $ 4 \times 2 = 8 $ rows.

**Output Relation:**

| student\_id | student\_name | dept | course\_id | course\_name     | credits |
| ----------- | ------------- | ---- | ---------- | ---------------- | ------- |
| 101         | Aarav Sharma  | CSE  | C01        | Data Structures  | 4       |
| 101         | Aarav Sharma  | CSE  | C03        | Database Systems | 4       |
| 102         | Diya Mehta    | ECE  | C01        | Data Structures  | 4       |
| 102         | Diya Mehta    | ECE  | C03        | Database Systems | 4       |
| 103         | Rohan Das     | IT   | C01        | Data Structures  | 4       |
| 103         | Rohan Das     | IT   | C03        | Database Systems | 4       |
| 104         | Sneha Bose    | CSE  | C01        | Data Structures  | 4       |
| 104         | Sneha Bose    | CSE  | C03        | Database Systems | 4       |

**Equivalent SQL Query:**

```sql
SELECT *
FROM Students
CROSS JOIN Courses
WHERE Courses.credits = 4;
```

---

### Example 4 — Cartesian Product + Select + Project

**Question:** Retrieve only the **student name** and **course name** for all **CSE** students enrolled in courses with **4 credits**.

**Relational Algebra Expression:**

$$
\pi_{\text{student\_name, course\_name}} \left( \sigma_{\text{dept} = \text{'CSE'} \, \land \, \text{credits} = 4} (\text{Students} \times \text{Courses}) \right)
$$

**Solution:**

**Step 1 — Cartesian Product:** Generate all $ 4 \times 3 = 12 $ combinations.

**Step 2 — Apply Select:** Filter rows where `dept = 'CSE'` AND `credits = 4`.

| student\_id | student\_name | dept | course\_id | course\_name     | credits |
| ----------- | ------------- | ---- | ---------- | ---------------- | ------- |
| 101         | Aarav Sharma  | CSE  | C01        | Data Structures  | 4       |
| 101         | Aarav Sharma  | CSE  | C03        | Database Systems | 4       |
| 104         | Sneha Bose    | CSE  | C01        | Data Structures  | 4       |
| 104         | Sneha Bose    | CSE  | C03        | Database Systems | 4       |

**Step 3 — Apply Project:** Keep only `student_name` and `course_name` columns.

**Output Relation:**

| student\_name | course\_name     |
| ------------- | ---------------- |
| Aarav Sharma  | Data Structures  |
| Aarav Sharma  | Database Systems |
| Sneha Bose    | Data Structures  |
| Sneha Bose    | Database Systems |

**Equivalent SQL Query:**

```sql
SELECT Students.student_name, Courses.course_name
FROM Students
CROSS JOIN Courses
WHERE Students.dept = 'CSE' AND Courses.credits = 4;
```

---

### Example 5 — Cartesian Product Simulating a Natural Join

**Question:** From all student-course combinations, retrieve only those rows where the student is from **CSE** and the course is **Data Structures** — effectively simulating a meaningful join.

**Relational Algebra Expression:**

$$
\sigma_{\text{dept} = \text{'CSE'} \, \land \, \text{course\_name} = \text{'Data Structures'}}(\text{Students} \times \text{Courses})
$$

**Solution:**

**Step 1 — Cartesian Product:** Generate all $ 4 \times 3 = 12 $ combinations.

**Step 2 — Apply Select:** Filter rows where `dept = 'CSE'` AND `course_name = 'Data Structures'`. Only CSE students (Aarav, Sneha) paired with Data Structures (C01) satisfy both conditions.

**Output Relation:**

| student\_id | student\_name | dept | course\_id | course\_name    | credits |
| ----------- | ------------- | ---- | ---------- | --------------- | ------- |
| 101         | Aarav Sharma  | CSE  | C01        | Data Structures | 4       |
| 104         | Sneha Bose    | CSE  | C01        | Data Structures | 4       |

**Equivalent SQL Query:**

```sql
SELECT *
FROM Students
CROSS JOIN Courses
WHERE Students.dept = 'CSE'
  AND Courses.course_name = 'Data Structures';
```

---

### Example 6 — Verifying Degree and Cardinality

**Question:** Verify the degree and cardinality rules for $ \text{Students} \times \text{Courses} $.

**Relational Algebra Expression:**

$$
\text{Students} \times \text{Courses}
$$

**Verification:**

| Property      | Formula                              | Calculation           | Result    |
| ------------- | ------------------------------------ | --------------------- | --------- |
| Degree        | $ \deg(\text{Students}) + \deg(\text{Courses}) $ | $ 3 + 3 $ | **6 columns** |
| Cardinality   | $ \|\text{Students}\| \times \|\text{Courses}\| $ | $ 4 \times 3 $ | **12 tuples** |

**Students columns:** `student_id`, `student_name`, `dept` → **3 columns**

**Courses columns:** `course_id`, `course_name`, `credits` → **3 columns**

**Result columns:** `student_id`, `student_name`, `dept`, `course_id`, `course_name`, `credits` → **6 columns** ✓

**Result rows:** $ 4 \times 3 = $ **12 rows** ✓

**Output Relation (confirming 12 tuples and 6 columns):**

| student\_id | student\_name | dept | course\_id | course\_name        | credits |
| ----------- | ------------- | ---- | ---------- | ------------------- | ------- |
| 101         | Aarav Sharma  | CSE  | C01        | Data Structures     | 4       |
| 101         | Aarav Sharma  | CSE  | C02        | Digital Electronics | 3       |
| 101         | Aarav Sharma  | CSE  | C03        | Database Systems    | 4       |
| 102         | Diya Mehta    | ECE  | C01        | Data Structures     | 4       |
| 102         | Diya Mehta    | ECE  | C02        | Digital Electronics | 3       |
| 102         | Diya Mehta    | ECE  | C03        | Database Systems    | 4       |
| 103         | Rohan Das     | IT   | C01        | Data Structures     | 4       |
| 103         | Rohan Das     | IT   | C02        | Digital Electronics | 3       |
| 103         | Rohan Das     | IT   | C03        | Database Systems    | 4       |
| 104         | Sneha Bose    | CSE  | C01        | Data Structures     | 4       |
| 104         | Sneha Bose    | CSE  | C02        | Digital Electronics | 3       |
| 104         | Sneha Bose    | CSE  | C03        | Database Systems    | 4       |

**Equivalent SQL Query:**

```sql
SELECT *
FROM Students
CROSS JOIN Courses;
-- Returns 12 rows with 6 columns
```

---

## Cartesian Product vs Join

> The **Cartesian Product** is the foundation of all **Join** operations. A Join is simply a Cartesian Product followed by a Select condition.

| Operation          | Expression                                                                 | Meaning                                        |
| ------------------ | -------------------------------------------------------------------------- | ---------------------------------------------- |
| Cartesian Product  | $ P \times Q $                                                             | All possible tuple combinations                |
| Theta Join         | $ \sigma_{\theta}(P \times Q) $                                            | Pairs satisfying condition $ \theta $          |
| Equi Join          | $ \sigma_{P.A = Q.B}(P \times Q) $                                         | Pairs where attribute A of P equals B of Q     |
| Natural Join       | $ \pi_{\text{unique cols}}(\sigma_{P.A = Q.A}(P \times Q)) $              | Pairs on common attributes, duplicate cols removed |

---

## Summary

| Aspect                  | Detail                                                                   |
| ----------------------- | ------------------------------------------------------------------------ |
| Operation Type          | Binary                                                                   |
| Symbol                  | $ \times $                                                               |
| Also Known As           | Cross Product, Cross Join                                                |
| Input                   | Any two relations (union compatibility NOT required)                     |
| Output                  | All possible ordered pairs of tuples from both relations                 |
| Mathematical Formula    | $ R = \{ \, (t_1, t_2) \mid t_1 \in P \text{ AND } t_2 \in Q \, \} $   |
| Result Degree           | $ \deg(P) + \deg(Q) $                                                    |
| Result Cardinality      | $ \|P\| \times \|Q\| $                                                   |
| Removes Duplicates      | No                                                                       |
| Condition Required      | No                                                                       |
| Union Compatible        | Not required                                                             |
| Commutative             | Yes (data is same, column order differs)                                 |
| Associative             | Yes                                                                      |
| Basis of Join           | Yes — $ \sigma\_{\theta}(P \times Q) $ forms a Theta Join               |
| SQL Equivalent          | `CROSS JOIN`                                                             |