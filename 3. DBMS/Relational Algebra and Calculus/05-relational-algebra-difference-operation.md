---
title: 05-Relational Algebra (Difference Operation)
---

# Set Difference Operation $ (-) $ — Relational Algebra (Part #5)

## Definition

The **Set Difference Operation** is a fundamental binary operation in relational algebra that returns all tuples (rows) that are present in the **first relation** but **NOT present** in the **second relation**. It effectively subtracts one relation from another.

> In simple terms, the Set Difference Operation is equivalent to the `EXCEPT` (or `MINUS`) keyword in SQL. It returns only those tuples that belong **exclusively** to the first relation and do **not** appear in the second relation.

---

## Mathematical Formula

If $ P $ and $ Q $ are two **union-compatible** relations, then the Set Difference of $ P $ and $ Q $ is defined as:

$$
R = P - Q
$$

$$
R = \{ \, t \mid t \in P \quad \text{AND} \quad t \notin Q \, \}
$$

Where:
- $ t $ — represents a **tuple** (a single row)
- $ P $ — is the **first relation** (the relation being subtracted **from**)
- $ Q $ — is the **second relation** (the relation being **subtracted**)
- $ R $ — is the **resulting relation** containing only tuples in $ P $ that do not appear in $ Q $

> A tuple $ t $ is included in the result $ R $ **only if** it belongs to $ P $ **and** does **not** belong to $ Q $. Tuples that appear in **both** relations are **excluded** from the result.

---

### Formula Example

**Relation P — Students Enrolled in Mathematics:**

| student\_id | name      |
| ----------- | --------- |
| 101         | Sumit     |
| 102         | Priyanka  |
| 103         | Purbali   |
| 107         | Rupam     |
| 110         | Anshumita |

**Relation Q — Students Enrolled in Physics:**

| student\_id | name     |
| ----------- | -------- |
| 102         | Priyanka |
| 103         | Purbali  |
| 104         | Sayan    |
| 105         | Mondira  |

**Applying:** $ R = P - Q $

> **Common tuples found:** `(102, Priyanka)` and `(103, Purbali)` appear in **both** $ P $ and $ Q $ — they will be **removed** from the result because we only want students who are in Mathematics but **NOT** in Physics.

**Result Relation $ R = P - Q $ — Students in Mathematics but NOT in Physics:**

| student\_id | name      |
| ----------- | --------- |
| 101         | Sumit     |
| 107         | Rupam     |
| 110         | Anshumita |

> $ P $ has **5 tuples**, $ Q $ has **4 tuples**, **2 are common** — so the final result has $ 5 - 2 = $ **3 tuples** (only students exclusively in Mathematics).

---

## Notation

$$
R = P - Q
$$

$$
\text{Relation}_1 - \text{Relation}_2
$$

Where:
- $ - $ — denotes the **set difference operation**
- $ P $ — is the **first relation** (table)
- $ Q $ — is the **second relation** (table)
- $ R $ — is the **resulting relation**

---

## Conditions for Set Difference Operation

Just like the Union operation, Set Difference also requires both relations to be **union-compatible**:

1. **Same Degree:** Both relations must have the **same number of attributes (columns)**.
2. **Compatible Domains:** The corresponding attributes must have **compatible domains** (same or compatible data types) — i.e., the $ i $-th attribute of $ P $ must have the same domain as the $ i $-th attribute of $ Q $.

> **Note:** The result relation takes the attribute names from the **first relation** $ P $.

---

## Difference Between Union and Set Difference

| Feature              | Union $ (\cup) $                  | Set Difference $ (-) $                |
| -------------------- | --------------------------------- | ------------------------------------- |
| Returns              | All tuples from both relations    | Only tuples exclusive to $ P $        |
| Handles Common Tuples| Keeps once (removes duplicates)   | Removes them entirely                 |
| Commutative          | Yes — $ P \cup Q = Q \cup P $     | No — $ P - Q \neq Q - P $            |
| SQL Equivalent       | `UNION`                           | `EXCEPT` / `MINUS`                    |
| Result Size          | $ \leq \|P\| + \|Q\| $            | $ \leq \|P\| $                        |

---

## Properties of Set Difference Operation

- **NOT Commutative:**
$$
P - Q \neq Q - P
$$
- **NOT Associative** in general:
$$
(P - Q) - T \neq P - (Q - T)
$$
- **Identity:**
$$
P - \emptyset = P
$$
- **Annihilation:**
$$
P - P = \emptyset
$$
- The **degree** of the result is the same as the degree of $ P $.
- The **cardinality** of the result satisfies:
$$
|P - Q| \leq |P|
$$

---

## Example Tables

Two separate relations are used throughout all examples below. These represent **two different university departments** and their student records.

### Relation — CS\_Students (Computer Science Department)

| student\_id | name           | age | gender | course          | cgpa |
| ----------- | -------------- | --- | ------ | --------------- | ---- |
| 101         | Aarav Sharma   | 20  | M      | Data Structures | 8.5  |
| 102         | Diya Mehta     | 22  | F      | Algorithms      | 9.1  |
| 103         | Rohan Das      | 21  | M      | Database        | 7.8  |
| 104         | Sneha Bose     | 23  | F      | Networking      | 8.0  |
| 105         | Kabir Roy      | 20  | M      | Data Structures | 6.5  |
| 106         | Tanya Gupta    | 22  | F      | Algorithms      | 9.4  |

### Relation — IT\_Students (Information Technology Department)

| student\_id | name           | age | gender | course          | cgpa |
| ----------- | -------------- | --- | ------ | --------------- | ---- |
| 103         | Rohan Das      | 21  | M      | Database        | 7.8  |
| 104         | Sneha Bose     | 23  | F      | Networking      | 8.0  |
| 107         | Arjun Verma    | 24  | M      | Cloud Computing | 7.2  |
| 108         | Pooja Nair     | 21  | F      | Web Development | 8.8  |
| 109         | Nikhil Sen     | 22  | M      | Database        | 7.5  |

> **Key Observation:** Rohan Das (103) and Sneha Bose (104) appear in **both** CS\_Students and IT\_Students — these are students registered in both departments. This overlap makes the Set Difference examples meaningful and clear.

---

## Derived Relations Using Select

Some examples also use the following filtered sub-relations derived from CS\_Students and IT\_Students:

### Relation A — CS Students with CGPA ≥ 8.0

$$
A = \sigma_{\text{cgpa} \geq 8.0}(\text{CS\_Students})
$$

| student\_id | name        | age | gender | course          | cgpa |
| ----------- | ----------- | --- | ------ | --------------- | ---- |
| 101         | Aarav Sharma| 20  | M      | Data Structures | 8.5  |
| 102         | Diya Mehta  | 22  | F      | Algorithms      | 9.1  |
| 104         | Sneha Bose  | 23  | F      | Networking      | 8.0  |
| 106         | Tanya Gupta | 22  | F      | Algorithms      | 9.4  |

### Relation B — IT Students with CGPA ≥ 8.0

$$
B = \sigma_{\text{cgpa} \geq 8.0}(\text{IT\_Students})
$$

| student\_id | name       | age | gender | course          | cgpa |
| ----------- | ---------- | --- | ------ | --------------- | ---- |
| 104         | Sneha Bose | 23  | F      | Networking      | 8.0  |
| 108         | Pooja Nair | 21  | F      | Web Development | 8.8  |

### Relation C — CS Female Students

$$
C = \sigma_{\text{gender} = \text{'F'}}(\text{CS\_Students})
$$

| student\_id | name        | age | gender | course     | cgpa |
| ----------- | ----------- | --- | ------ | ---------- | ---- |
| 102         | Diya Mehta  | 22  | F      | Algorithms | 9.1  |
| 104         | Sneha Bose  | 23  | F      | Networking | 8.0  |
| 106         | Tanya Gupta | 22  | F      | Algorithms | 9.4  |

### Relation D — IT Female Students

$$
D = \sigma_{\text{gender} = \text{'F'}}(\text{IT\_Students})
$$

| student\_id | name       | age | gender | course          | cgpa |
| ----------- | ---------- | --- | ------ | --------------- | ---- |
| 104         | Sneha Bose | 23  | F      | Networking      | 8.0  |
| 108         | Pooja Nair | 21  | F      | Web Development | 8.8  |

---

## Examples

---

### Example 1 — Basic Set Difference (No Overlap)

**Question:** Retrieve all students who are **only in CS** department and have **NO enrollment** in the IT department.

**Relational Algebra Expression:**

$$
\text{CS\_Students} - \text{IT\_Students}
$$

**Solution:** The operation scans every tuple in CS\_Students and removes any tuple that also exists in IT\_Students. Rohan Das (103) and Sneha Bose (104) appear in **both** tables, so they are excluded. The remaining 4 students are exclusive to CS.

**CS\_Students:**

| student\_id | name           | age | gender | course          | cgpa |
| ----------- | -------------- | --- | ------ | --------------- | ---- |
| 101         | Aarav Sharma   | 20  | M      | Data Structures | 8.5  |
| 102         | Diya Mehta     | 22  | F      | Algorithms      | 9.1  |
| **103**     | **Rohan Das**  | 21  | M      | Database        | 7.8  |
| **104**     | **Sneha Bose** | 23  | F      | Networking      | 8.0  |
| 105         | Kabir Roy      | 20  | M      | Data Structures | 6.5  |
| 106         | Tanya Gupta    | 22  | F      | Algorithms      | 9.4  |

**IT\_Students:**

| student\_id | name           | age | gender | course          | cgpa |
| ----------- | -------------- | --- | ------ | --------------- | ---- |
| **103**     | **Rohan Das**  | 21  | M      | Database        | 7.8  |
| **104**     | **Sneha Bose** | 23  | F      | Networking      | 8.0  |
| 107         | Arjun Verma    | 24  | M      | Cloud Computing | 7.2  |
| 108         | Pooja Nair     | 21  | F      | Web Development | 8.8  |
| 109         | Nikhil Sen     | 22  | M      | Database        | 7.5  |

> **Common tuples removed:** Rohan Das (103) and Sneha Bose (104) — highlighted in bold above — are subtracted.

**Output Relation $ \text{CS\_Students} - \text{IT\_Students} $:**

| student\_id | name        | age | gender | course          | cgpa |
| ----------- | ----------- | --- | ------ | --------------- | ---- |
| 101         | Aarav Sharma| 20  | M      | Data Structures | 8.5  |
| 102         | Diya Mehta  | 22  | F      | Algorithms      | 9.1  |
| 105         | Kabir Roy   | 20  | M      | Data Structures | 6.5  |
| 106         | Tanya Gupta | 22  | F      | Algorithms      | 9.4  |

**Equivalent SQL Query:**

```sql
SELECT * FROM CS_Students
EXCEPT
SELECT * FROM IT_Students;
```

---

### Example 2 — Reverse Set Difference (Proving Non-Commutativity)

**Question:** Retrieve all students who are **only in IT** department and have **NO enrollment** in the CS department. Compare with Example 1 to prove non-commutativity.

**Relational Algebra Expression:**

$$
\text{IT\_Students} - \text{CS\_Students}
$$

**Solution:** Now we subtract CS\_Students from IT\_Students. The same common tuples — Rohan Das (103) and Sneha Bose (104) — are removed from IT\_Students, leaving only the 3 students exclusive to IT.

**Output Relation $ \text{IT\_Students} - \text{CS\_Students} $:**

| student\_id | name        | age | gender | course          | cgpa |
| ----------- | ----------- | --- | ------ | --------------- | ---- |
| 107         | Arjun Verma | 24  | M      | Cloud Computing | 7.2  |
| 108         | Pooja Nair  | 21  | F      | Web Development | 8.8  |
| 109         | Nikhil Sen  | 22  | M      | Database        | 7.5  |

**Comparison:**

| Expression                                    | Result Tuples            |
| --------------------------------------------- | ------------------------ |
| $ \text{CS\_Students} - \text{IT\_Students} $ | Aarav, Diya, Kabir, Tanya |
| $ \text{IT\_Students} - \text{CS\_Students} $ | Arjun, Pooja, Nikhil     |

> **Conclusion:** The two results are completely different — confirming that Set Difference is **NOT commutative**: $ P - Q \neq Q - P $.

**Equivalent SQL Query:**

```sql
SELECT * FROM IT_Students
EXCEPT
SELECT * FROM CS_Students;
```

---

### Example 3 — Set Difference on Filtered Relations (CGPA ≥ 8.0)

**Question:** Retrieve students with **CGPA ≥ 8.0 in CS** who do **NOT** have a CGPA ≥ 8.0 in IT (i.e., high-performing CS-only students).

**Relational Algebra Expression:**

$$
\sigma_{\text{cgpa} \geq 8.0}(\text{CS\_Students}) - \sigma_{\text{cgpa} \geq 8.0}(\text{IT\_Students})
$$

Or equivalently:

$$
A - B
$$

**Solution:** Relation $ A $ has 4 high-CGPA CS students. Relation $ B $ has 2 high-CGPA IT students. Sneha Bose (104) appears in **both** $ A $ and $ B $ — she is subtracted. The remaining 3 are exclusive high-performers in CS only.

**Relation A — CS Students with CGPA ≥ 8.0:**

| student\_id | name        | age | gender | course          | cgpa |
| ----------- | ----------- | --- | ------ | --------------- | ---- |
| 101         | Aarav Sharma| 20  | M      | Data Structures | 8.5  |
| 102         | Diya Mehta  | 22  | F      | Algorithms      | 9.1  |
| **104**     | **Sneha Bose**| 23 | F     | Networking      | 8.0  |
| 106         | Tanya Gupta | 22  | F      | Algorithms      | 9.4  |

**Relation B — IT Students with CGPA ≥ 8.0:**

| student\_id | name       | age | gender | course          | cgpa |
| ----------- | ---------- | --- | ------ | --------------- | ---- |
| **104**     | **Sneha Bose** | 23 | F   | Networking      | 8.0  |
| 108         | Pooja Nair | 21  | F      | Web Development | 8.8  |

> **Common tuple removed:** Sneha Bose (104) — highlighted in bold — is subtracted.

**Output Relation $ A - B $:**

| student\_id | name        | age | gender | course          | cgpa |
| ----------- | ----------- | --- | ------ | --------------- | ---- |
| 101         | Aarav Sharma| 20  | M      | Data Structures | 8.5  |
| 102         | Diya Mehta  | 22  | F      | Algorithms      | 9.1  |
| 106         | Tanya Gupta | 22  | F      | Algorithms      | 9.4  |

**Equivalent SQL Query:**

```sql
SELECT * FROM CS_Students WHERE cgpa >= 8.0
EXCEPT
SELECT * FROM IT_Students WHERE cgpa >= 8.0;
```

---

### Example 4 — Set Difference on Female Students

**Question:** Retrieve **female CS students** who are **NOT** enrolled in the IT department as female students.

**Relational Algebra Expression:**

$$
\sigma_{\text{gender} = \text{'F'}}(\text{CS\_Students}) - \sigma_{\text{gender} = \text{'F'}}(\text{IT\_Students})
$$

Or equivalently:

$$
C - D
$$

**Solution:** Relation $ C $ has 3 female CS students. Relation $ D $ has 2 female IT students. Sneha Bose (104) appears in **both** $ C $ and $ D $ — she is subtracted. The remaining 2 females are exclusive to CS.

**Relation C — CS Female Students:**

| student\_id | name        | age | gender | course     | cgpa |
| ----------- | ----------- | --- | ------ | ---------- | ---- |
| 102         | Diya Mehta  | 22  | F      | Algorithms | 9.1  |
| **104**     | **Sneha Bose**| 23 | F     | Networking | 8.0  |
| 106         | Tanya Gupta | 22  | F      | Algorithms | 9.4  |

**Relation D — IT Female Students:**

| student\_id | name       | age | gender | course          | cgpa |
| ----------- | ---------- | --- | ------ | --------------- | ---- |
| **104**     | **Sneha Bose** | 23 | F   | Networking      | 8.0  |
| 108         | Pooja Nair | 21  | F      | Web Development | 8.8  |

> **Common tuple removed:** Sneha Bose (104) — highlighted in bold — is subtracted.

**Output Relation $ C - D $:**

| student\_id | name        | age | gender | course     | cgpa |
| ----------- | ----------- | --- | ------ | ---------- | ---- |
| 102         | Diya Mehta  | 22  | F      | Algorithms | 9.1  |
| 106         | Tanya Gupta | 22  | F      | Algorithms | 9.4  |

**Equivalent SQL Query:**

```sql
SELECT * FROM CS_Students WHERE gender = 'F'
EXCEPT
SELECT * FROM IT_Students WHERE gender = 'F';
```

---

### Example 5 — Set Difference with Project (Specific Columns)

**Question:** Retrieve the **name** and **course** of CS students whose name and course combination does **NOT** appear among IT students.

**Relational Algebra Expression:**

$$
\pi_{\text{name, course}}(\text{CS\_Students}) - \pi_{\text{name, course}}(\text{IT\_Students})
$$

**Solution:**

**Step 1 — Project CS\_Students (name, course):**

| name        | course          |
| ----------- | --------------- |
| Aarav Sharma| Data Structures |
| Diya Mehta  | Algorithms      |
| Rohan Das   | Database        |
| Sneha Bose  | Networking      |
| Kabir Roy   | Data Structures |
| Tanya Gupta | Algorithms      |

**Step 2 — Project IT\_Students (name, course):**

| name        | course          |
| ----------- | --------------- |
| Rohan Das   | Database        |
| Sneha Bose  | Networking      |
| Arjun Verma | Cloud Computing |
| Pooja Nair  | Web Development |
| Nikhil Sen  | Database        |

**Step 3 — Apply Set Difference:**

> **Common tuples removed:** `(Rohan Das, Database)` and `(Sneha Bose, Networking)` appear in both — they are subtracted.

**Output Relation:**

| name        | course          |
| ----------- | --------------- |
| Aarav Sharma| Data Structures |
| Diya Mehta  | Algorithms      |
| Kabir Roy   | Data Structures |
| Tanya Gupta | Algorithms      |

**Equivalent SQL Query:**

```sql
SELECT name, course FROM CS_Students
EXCEPT
SELECT name, course FROM IT_Students;
```

---

### Example 6 — Annihilation Property

**Question:** Subtract the CS department from itself and verify the annihilation property.

**Relational Algebra Expression:**

$$
\text{CS\_Students} - \text{CS\_Students} = \emptyset
$$

**Solution:** Both operands are the **same relation**. Every tuple in CS\_Students is also present in the second CS\_Students — so **every tuple is subtracted**, leaving a completely empty relation.

**Output Relation:**

| student\_id | name | age | gender | course | cgpa |
| ----------- | ---- | --- | ------ | ------ | ---- |
| *(empty — no tuples)* | | | | | |

> **Result:** $ \text{CS\_Students} - \text{CS\_Students} = \emptyset $ — confirmed. A relation subtracted from itself **always yields an empty relation**, regardless of how many tuples it contains.

**Equivalent SQL Query:**

```sql
SELECT * FROM CS_Students
EXCEPT
SELECT * FROM CS_Students;
```

---

## Summary

| Aspect                | Detail                                                               |
| --------------------- | -------------------------------------------------------------------- |
| Operation Type        | Binary                                                               |
| Symbol                | $ - $                                                                |
| Input                 | Two union-compatible relations                                        |
| Output                | Tuples in $ P $ that do **not** appear in $ Q $                      |
| Mathematical Formula  | $ R = \{ \, t \mid t \in P \text{ AND } t \notin Q \, \} $          |
| Union Compatibility   | Same number of attributes + compatible domains                        |
| Removes Common Tuples | Yes — tuples in both $ P $ and $ Q $ are excluded from the result    |
| Commutative           | **No** — $ P - Q \neq Q - P $                                        |
| Associative           | **No** — $ (P - Q) - T \neq P - (Q - T) $                           |
| Identity              | $ P - \emptyset = P $                                                |
| Annihilation          | $ P - P = \emptyset $                                                |
| Cardinality of Result | $ \leq \|P\| $                                                       |
| SQL Equivalent        | `EXCEPT` / `MINUS` keyword                                           |