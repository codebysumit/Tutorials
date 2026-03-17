---
title: 02-Relational Algebra (Select Operation)
---

# Select Operation $ (\sigma) $ — Relational Algebra (Part #2)

## Definition

The **Select Operation** is a fundamental unary operation in relational algebra used to filter tuples (rows) from a relation (table) that satisfy a given condition or predicate. It works horizontally — meaning it selects specific **rows** while keeping **all columns** intact.

> In simple terms, the Select Operation is equivalent to the `WHERE` clause in SQL. It retrieves only those tuples from a relation that meet the specified condition.

---

## Notation

$$
\sigma_{p}(R)
$$

$$
\sigma_{\text{selection\_condition}}(\text{Relation})
$$

Where:

- **$ \sigma $ (sigma) :** denotes the **select operation**
- **$ p $ :** is the **selection predicate** (a condition or logical formula)
- **$ R $ :** is the **relation** (table) on which the operation is applied

---

## Properties of Select Operation

- The result of a select operation is always a **subset** of the original relation.
- The **degree** (number of columns/attributes) of the result is the **same** as the original relation.
- The **cardinality** (number of rows) of the result is **less than or equal to** the original relation.
- Select operation is **commutative**, meaning:
  $$
  \sigma_{p1}(\sigma_{p2}(R)) = \sigma_{p2}(\sigma_{p1}(R))
  $$
- A **cascade of selections** can be combined into a single selection using the AND ($\land$) operator:
  $$
  \sigma_{p1}(\sigma_{p2}(R)) = \sigma_{p1 \land p2}(R)
  $$

---

## Operators Used in Selection Predicate

The predicate $ p $ is a propositional logic formula that may use the following operators:

### Comparison Operators

| Operator | Meaning                  |
| -------- | ------------------------ |
| $ = $    | Equal to                 |
| $ \neq $ | Not equal to             |
| $ > $    | Greater than             |
| $ < $    | Less than                |
| $ \geq $ | Greater than or equal to |
| $ \leq $ | Less than or equal to    |

### Connective Operators (Logical Operators)

| Operator | Symbol    | Meaning                             |
| -------- | --------- | ----------------------------------- |
| AND      | $ \land $ | Both conditions must be true        |
| OR       | $ \lor $  | At least one condition must be true |
| NOT      | $ \neg $  | Negates (reverses) the condition    |

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

## Examples

---

### Example 1 — Simple Equality Condition

**Question:** Retrieve all students who belong to the **CSE** department.

**Relational Algebra Expression:**

$$
\sigma_{\text{department} = \text{'CSE'}}(\text{Students})
$$

**Solution:** The select operation scans every tuple in the Students relation and returns only those where the `department` attribute equals `'CSE'`.

**Output Relation:**

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 101        | Sumit Das  | 21  | M      | CSE        | 85    |
| 103        | Ravi Kumar | 22  | M      | CSE        | 90    |
| 106        | Neha Singh | 23  | F      | CSE        | 78    |

**Equivalent SQL Query:**

```sql
SELECT *
FROM Students
WHERE department = 'CSE';
```

---

### Example 2 — Comparison Condition

**Question:** Retrieve all students whose **marks are greater than 75**.

**Relational Algebra Expression:**

$$
\sigma_{\text{marks} > 75}(\text{Students})
$$

**Solution:** The select operation returns all tuples where the `marks` attribute holds a value strictly greater than 75.

**Output Relation:**

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 101        | Sumit Das  | 21  | M      | CSE        | 85    |
| 103        | Ravi Kumar | 22  | M      | CSE        | 90    |
| 106        | Neha Singh | 23  | F      | CSE        | 78    |

**Equivalent SQL Query:**

```sql
SELECT *
FROM Students
WHERE marks > 75;
```

---

### Example 3 — AND Condition ( $ \land $ )

**Question:** Retrieve all students who belong to the **CSE** department **AND** have **marks greater than 80**.

**Relational Algebra Expression:**

$$
\sigma_{\text{department} = \text{'CSE'} \land \text{marks} > 80}(\text{Students})
$$

**Solution:** Both conditions must be satisfied simultaneously. Only tuples where `department = 'CSE'` AND `marks > 80` are selected.

**Output Relation:**

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 101        | Sumit Das  | 21  | M      | CSE        | 85    |
| 103        | Ravi Kumar | 22  | M      | CSE        | 90    |

**Equivalent SQL Query:**

```sql
SELECT *
FROM Students
WHERE department = 'CSE' AND marks > 80;
```

---

### Example 4 — OR Condition ( $ \lor $ )

**Question:** Retrieve all students who belong to either the **CSE** or **ECE** department.

**Relational Algebra Expression:**

$$
\sigma_{\text{department} = \text{'CSE'} \lor \text{department} = \text{'ECE'}}(\text{Students})
$$

**Solution:** At least one of the two conditions must be true. Tuples where `department = 'CSE'` OR `department = 'ECE'` are returned.

**Output Relation:**

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 101        | Sumit Das  | 21  | M      | CSE        | 85    |
| 102        | Sumana Das | 26  | F      | ECE        | 72    |
| 103        | Ravi Kumar | 22  | M      | CSE        | 90    |
| 105        | Anik Ghosh | 21  | M      | ECE        | 55    |
| 106        | Neha Singh | 23  | F      | CSE        | 78    |

**Equivalent SQL Query:**

```sql
SELECT *
FROM Students
WHERE department = 'CSE' OR department = 'ECE';
```

---

### Example 5 — NOT Condition ( $ \neg $ )

**Question:** Retrieve all students who are **NOT** from the **IT** department.

**Relational Algebra Expression:**

$$
\sigma_{\neg(\text{department} = \text{'IT'})}(\text{Students})
$$

**Solution:** The NOT operator negates the condition. All tuples where `department` is anything other than `'IT'` are returned.

**Output Relation:**

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 101        | Sumit Das  | 21  | M      | CSE        | 85    |
| 102        | Sumana Das | 26  | F      | ECE        | 72    |
| 103        | Ravi Kumar | 22  | M      | CSE        | 90    |
| 105        | Anik Ghosh | 21  | M      | ECE        | 55    |
| 106        | Neha Singh | 23  | F      | CSE        | 78    |

**Equivalent SQL Query:**

```sql
SELECT *
FROM Students
WHERE department <> 'IT';
```

---

### Example 6 — Combined Condition (AND + Comparison)

**Question:** Retrieve all **female** students whose **age is less than or equal to 24**.

**Relational Algebra Expression:**

$$
\sigma_{\text{gender} = \text{'F'} \land \text{age} \leq 24}(\text{Students})
$$

**Solution:** Both conditions must hold. Female students (`gender = 'F'`) with an age of 24 or below are returned.

**Output Relation:**

| student_id | name         | age | gender | department | marks |
| ---------- | ------------ | --- | ------ | ---------- | ----- |
| 104        | Priya Sharma | 24  | F      | IT         | 68    |
| 106        | Neha Singh   | 23  | F      | CSE        | 78    |

**Equivalent SQL Query:**

```sql
SELECT *
FROM Students
WHERE gender = 'F' AND age <= 24;
```

---

## Summary

| Aspect            | Detail                                                              |
| ----------------- | ------------------------------------------------------------------- |
| Operation Type    | Unary                                                               |
| Symbol            | $ \sigma $                                                          |
| Input             | A relation (table)                                                  |
| Output            | A subset of tuples satisfying the predicate                         |
| Columns in Result | Same as the original relation (no columns are removed)              |
| SQL Equivalent    | `WHERE` clause                                                      |
| Commutative?      | Yes — $ \sigma*{p1}(\sigma*{p2}(R)) = \sigma*{p2}(\sigma*{p1}(R)) $ |
