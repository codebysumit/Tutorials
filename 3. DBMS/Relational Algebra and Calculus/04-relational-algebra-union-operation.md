---
title: 04-Relational Algebra (Union Operation)
---

# Union Operation $ (\cup) $ — Relational Algebra (Part #4)

## Definition

The **Union Operation** is a fundamental binary operation in relational algebra that combines the tuples (rows) of **two relations** into a single relation. The result contains **all tuples** that appear in either the first relation, the second relation, or both — and **duplicate tuples are automatically removed**.

> In simple terms, the Union Operation is equivalent to the `UNION` keyword in SQL. It merges two relations and returns a result that includes every unique tuple from both.

---

## Mathematical Formula

If $ P $ and $ Q $ are two **union-compatible** relations, then the Union of $ P $ and $ Q $ is the **set-theoretic union** of $ P $ and $ Q $.

The resultant relation $ R $ is defined as:

$$
R = P \cup Q
$$

$$
R = \{ \, t \mid t \in P \quad \text{OR} \quad t \in Q \, \}
$$

Where:

- $ t $ — represents a **tuple** (a single row)
- $ P $ — is the **first relation**
- $ Q $ — is the **second relation**
- $ R $ — is the **resulting relation** containing all unique tuples from both $ P $ and $ Q $

> A tuple $ t $ is included in the result $ R $ if it belongs to **either** $ P $ or $ Q $ or **both**. Duplicate tuples (tuples appearing in both $ P $ and $ Q $) are included only **once** in the result.

---

### Formula Example

**Relation P:**

| id  | name      |
| --- | --------- |
| 101 | Sumit     |
| 107 | Rupam     |
| 110 | Anshumita |
| 102 | Priyanka  |
| 103 | Purbali   |

**Relation Q:**

| id  | name     |
| --- | -------- |
| 104 | Sayan    |
| 105 | Mondira  |
| 103 | Purbali  |
| 102 | Priyanka |

**Applying:** $ R = P \cup Q $

> **Duplicates detected:** Tuples `(103, Purbali)` and `(102, Priyanka)` appear in **both** $ P $ and $ Q $ — they will appear **only once** in the result.

**Result Relation $ R = P \cup Q $:**

| id  | name      |
| --- | --------- |
| 101 | Sumit     |
| 107 | Rupam     |
| 110 | Anshumita |
| 102 | Priyanka  |
| 103 | Purbali   |
| 104 | Sayan     |
| 105 | Mondira   |

> $ P $ contributes **5 tuples**, $ Q $ contributes **4 tuples**, but **2 are duplicates** — so the final result has $ 5 + 4 - 2 = $ **7 unique tuples**.

---

## Notation

$$
R = P \cup Q
$$

$$
\text{Relation}_1 \cup \text{Relation}_2
$$

Where:

- $ \cup $ — denotes the **union operation**
- $ P $ — is the **first relation** (table)
- $ Q $ — is the **second relation** (table)
- $ R $ — is the **resulting relation**

---

## Conditions for Union Operation (Union Compatibility)

For the Union operation to be valid, both relations **must be union-compatible**, meaning they must satisfy the following two conditions:

1. **Same Degree:** Both relations must have the **same number of attributes (columns)**.
2. **Compatible Domains:** The corresponding attributes must have **compatible domains** (same or compatible data types) — i.e., the $ i $-th attribute of $ P $ must have the same domain as the $ i $-th attribute of $ Q $.

> **Note:** The attribute **names** do not need to be the same — only the number of attributes and their domains must match. The result relation takes the attribute names from the **first relation** $ P $.

---

## Properties of Union Operation

- **Commutative:**
  $$
  P \cup Q = Q \cup P
  $$
- **Associative:**
  $$
  (P \cup Q) \cup T = P \cup (Q \cup T)
  $$
- **Duplicate Elimination:** All duplicate tuples are automatically removed from the result.
- **Idempotent:**
  $$
  P \cup P = P
  $$
- The **degree** of the result is the same as the degree of $ P $ and $ Q $.
- The **cardinality** of the result is:
  $$
  |P \cup Q| \leq |P| + |Q|
  $$

---

## Example Table — Students

The following **Students** relation is the base table used across all examples:

| student_id | name         | age | gender | department | marks |
| ---------- | ------------ | --- | ------ | ---------- | ----- |
| 101        | Sumit Das    | 21  | M      | CSE        | 85    |
| 102        | Sumana Das   | 26  | F      | ECE        | 72    |
| 103        | Ravi Kumar   | 22  | M      | CSE        | 90    |
| 104        | Priya Sharma | 24  | F      | IT         | 68    |
| 105        | Anik Ghosh   | 21  | M      | ECE        | 55    |
| 106        | Neha Singh   | 23  | F      | CSE        | 78    |

---

## Derived Relations Using Select

To demonstrate the Union operation using the same Students table, we first derive **sub-relations** using the Select operation $ (\sigma) $, and then apply Union on them.

### Relation A — CSE Students

$$
A = \sigma_{\text{department} = \text{'CSE'}}(\text{Students})
$$

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 101        | Sumit Das  | 21  | M      | CSE        | 85    |
| 103        | Ravi Kumar | 22  | M      | CSE        | 90    |
| 106        | Neha Singh | 23  | F      | CSE        | 78    |

### Relation B — ECE Students

$$
B = \sigma_{\text{department} = \text{'ECE'}}(\text{Students})
$$

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 102        | Sumana Das | 26  | F      | ECE        | 72    |
| 105        | Anik Ghosh | 21  | M      | ECE        | 55    |

### Relation C — Students with Marks Greater Than 80

$$
C = \sigma_{\text{marks} > 80}(\text{Students})
$$

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 101        | Sumit Das  | 21  | M      | CSE        | 85    |
| 103        | Ravi Kumar | 22  | M      | CSE        | 90    |

### Relation D — Female Students

$$
D = \sigma_{\text{gender} = \text{'F'}}(\text{Students})
$$

| student_id | name         | age | gender | department | marks |
| ---------- | ------------ | --- | ------ | ---------- | ----- |
| 102        | Sumana Das   | 26  | F      | ECE        | 72    |
| 104        | Priya Sharma | 24  | F      | IT         | 68    |
| 106        | Neha Singh   | 23  | F      | CSE        | 78    |

---

## Examples

---

### Example 1 — Union of Two Disjoint Sets

**Question:** Retrieve all students who are from either the **CSE** department or the **ECE** department.

**Relational Algebra Expression:**

$$
\sigma_{\text{department} = \text{'CSE'}}(\text{Students}) \cup \sigma_{\text{department} = \text{'ECE'}}(\text{Students})
$$

Or equivalently using derived relations:

$$
A \cup B
$$

**Solution:** Relation $ A $ has 3 tuples (CSE students) and Relation $ B $ has 2 tuples (ECE students). Since there are no common tuples between them, the union simply combines all 5 tuples with no duplicates to remove.

**Relation A (CSE Students):**

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 101        | Sumit Das  | 21  | M      | CSE        | 85    |
| 103        | Ravi Kumar | 22  | M      | CSE        | 90    |
| 106        | Neha Singh | 23  | F      | CSE        | 78    |

**Relation B (ECE Students):**

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 102        | Sumana Das | 26  | F      | ECE        | 72    |
| 105        | Anik Ghosh | 21  | M      | ECE        | 55    |

**Output Relation $ A \cup B $:**

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 101        | Sumit Das  | 21  | M      | CSE        | 85    |
| 103        | Ravi Kumar | 22  | M      | CSE        | 90    |
| 106        | Neha Singh | 23  | F      | CSE        | 78    |
| 102        | Sumana Das | 26  | F      | ECE        | 72    |
| 105        | Anik Ghosh | 21  | M      | ECE        | 55    |

**Equivalent SQL Query:**

```sql
SELECT * FROM Students WHERE department = 'CSE'
UNION
SELECT * FROM Students WHERE department = 'ECE';
```

---

### Example 2 — Union with Overlapping Tuples (Duplicate Elimination)

**Question:** Retrieve all students who are from the **CSE** department or have **marks greater than 80** (duplicates must be removed).

**Relational Algebra Expression:**

$$
\sigma_{\text{department} = \text{'CSE'}}(\text{Students}) \cup \sigma_{\text{marks} > 80}(\text{Students})
$$

Or equivalently:

$$
A \cup C
$$

**Solution:** Relation $ A $ has 3 CSE students and Relation $ C $ has 2 students with marks > 80. However, Sumit Das (101) and Ravi Kumar (103) appear in **both** $ A $ and $ C $. The union operation removes these duplicates and returns only unique tuples.

**Relation A (CSE Students):**

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 101        | Sumit Das  | 21  | M      | CSE        | 85    |
| 103        | Ravi Kumar | 22  | M      | CSE        | 90    |
| 106        | Neha Singh | 23  | F      | CSE        | 78    |

**Relation C (Marks > 80):**

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 101        | Sumit Das  | 21  | M      | CSE        | 85    |
| 103        | Ravi Kumar | 22  | M      | CSE        | 90    |

> **Duplicates detected:** Sumit Das (101) and Ravi Kumar (103) appear in both relations — they will appear **only once** in the result.

**Output Relation $ A \cup C $:**

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 101        | Sumit Das  | 21  | M      | CSE        | 85    |
| 103        | Ravi Kumar | 22  | M      | CSE        | 90    |
| 106        | Neha Singh | 23  | F      | CSE        | 78    |

**Equivalent SQL Query:**

```sql
SELECT * FROM Students WHERE department = 'CSE'
UNION
SELECT * FROM Students WHERE marks > 80;
```

---

### Example 3 — Union of CSE Students and Female Students

**Question:** Retrieve all students who are either from the **CSE** department or are **female**.

**Relational Algebra Expression:**

$$
\sigma_{\text{department} = \text{'CSE'}}(\text{Students}) \cup \sigma_{\text{gender} = \text{'F'}}(\text{Students})
$$

Or equivalently:

$$
A \cup D
$$

**Solution:** Relation $ A $ contains 3 CSE students and Relation $ D $ contains 3 female students. Neha Singh (106) appears in **both** $ A $ and $ D $ (she is female and from CSE), so she appears only once in the result.

**Relation A (CSE Students):**

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 101        | Sumit Das  | 21  | M      | CSE        | 85    |
| 103        | Ravi Kumar | 22  | M      | CSE        | 90    |
| 106        | Neha Singh | 23  | F      | CSE        | 78    |

**Relation D (Female Students):**

| student_id | name         | age | gender | department | marks |
| ---------- | ------------ | --- | ------ | ---------- | ----- |
| 102        | Sumana Das   | 26  | F      | ECE        | 72    |
| 104        | Priya Sharma | 24  | F      | IT         | 68    |
| 106        | Neha Singh   | 23  | F      | CSE        | 78    |

> **Duplicate detected:** Neha Singh (106) appears in both relations — she will appear **only once** in the result.

**Output Relation $ A \cup D $:**

| student_id | name         | age | gender | department | marks |
| ---------- | ------------ | --- | ------ | ---------- | ----- |
| 101        | Sumit Das    | 21  | M      | CSE        | 85    |
| 103        | Ravi Kumar   | 22  | M      | CSE        | 90    |
| 106        | Neha Singh   | 23  | F      | CSE        | 78    |
| 102        | Sumana Das   | 26  | F      | ECE        | 72    |
| 104        | Priya Sharma | 24  | F      | IT         | 68    |

**Equivalent SQL Query:**

```sql
SELECT * FROM Students WHERE department = 'CSE'
UNION
SELECT * FROM Students WHERE gender = 'F';
```

---

### Example 4 — Union with Project (Specific Columns)

**Question:** Retrieve the **name** and **department** of all students who are from **CSE** or **ECE**.

**Relational Algebra Expression:**

$$
\pi_{\text{name, department}}(\sigma_{\text{department} = \text{'CSE'}}(\text{Students})) \cup \pi_{\text{name, department}}(\sigma_{\text{department} = \text{'ECE'}}(\text{Students}))
$$

**Solution:**

**Step 1 — Project + Select on CSE:**

| name       | department |
| ---------- | ---------- |
| Sumit Das  | CSE        |
| Ravi Kumar | CSE        |
| Neha Singh | CSE        |

**Step 2 — Project + Select on ECE:**

| name       | department |
| ---------- | ---------- |
| Sumana Das | ECE        |
| Anik Ghosh | ECE        |

**Step 3 — Apply Union (no duplicates here):**

**Output Relation:**

| name       | department |
| ---------- | ---------- |
| Sumit Das  | CSE        |
| Ravi Kumar | CSE        |
| Neha Singh | CSE        |
| Sumana Das | ECE        |
| Anik Ghosh | ECE        |

**Equivalent SQL Query:**

```sql
SELECT name, department FROM Students WHERE department = 'CSE'
UNION
SELECT name, department FROM Students WHERE department = 'ECE';
```

---

### Example 5 — Union with Idempotent Property

**Question:** Retrieve all students from the **CSE** department — applied twice using Union — and verify the idempotent property.

**Relational Algebra Expression:**

$$
\sigma_{\text{department} = \text{'CSE'}}(\text{Students}) \cup \sigma_{\text{department} = \text{'CSE'}}(\text{Students})
$$

Or equivalently:

$$
A \cup A = A
$$

**Solution:** Both operands are identical, so every tuple is a duplicate. After duplicate elimination, the result is exactly the same as Relation $ A $ — demonstrating the **idempotent property** of Union.

**Output Relation $ A \cup A $:**

| student_id | name       | age | gender | department | marks |
| ---------- | ---------- | --- | ------ | ---------- | ----- |
| 101        | Sumit Das  | 21  | M      | CSE        | 85    |
| 103        | Ravi Kumar | 22  | M      | CSE        | 90    |
| 106        | Neha Singh | 23  | F      | CSE        | 78    |

> **Result:** $ A \cup A = A $ — confirmed. The union of a relation with itself returns the same relation.

**Equivalent SQL Query:**

```sql
SELECT * FROM Students WHERE department = 'CSE'
UNION
SELECT * FROM Students WHERE department = 'CSE';
```

---

## Summary

| Aspect                | Detail                                                     |
| --------------------- | ---------------------------------------------------------- |
| Operation Type        | Binary                                                     |
| Symbol                | $ \cup $                                                   |
| Input                 | Two union-compatible relations                             |
| Output                | All unique tuples from both relations (duplicates removed) |
| Mathematical Formula  | $ R = \{ \, t \mid t \in P \text{ OR } t \in Q \, \} $     |
| Union Compatibility   | Same number of attributes + compatible domains             |
| Removes Duplicates    | Yes                                                        |
| Commutative           | Yes — $ P \cup Q = Q \cup P $                              |
| Associative           | Yes — $ (P \cup Q) \cup T = P \cup (Q \cup T) $            |
| Idempotent            | Yes — $ P \cup P = P $                                     |
| Cardinality of Result | $ \leq \|P\| + \|Q\| $                                     |
| SQL Equivalent        | `UNION` keyword                                            |
