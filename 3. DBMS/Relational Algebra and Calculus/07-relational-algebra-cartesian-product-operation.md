---
title: 07-Relational Algebra (Cartesian Product Operation)
---

# Rename Operation $ (\rho) $ — Relational Algebra

## Definition

The **Rename Operation** is a fundamental unary operation in relational algebra used to **rename** a relation, its attributes, or both. It does not change the data or structure of the relation — it simply assigns a new name to the relation and/or its columns.

> In simple terms, the Rename Operation is equivalent to the `AS` keyword (alias) in SQL. It is especially useful when performing operations like Cartesian Product or Self-Join, where two copies of the same relation are involved and column names would otherwise conflict.

---

## Why Rename is Needed

Consider the following situations where Rename becomes essential:

1. **Cartesian Product of a relation with itself (Self-Join):** If we compute $ \text{Students} \times \text{Students} $, both copies have the same attribute names — causing **ambiguity**. Rename resolves this by giving each copy a distinct name.

2. **Long or complex expressions:** When a relational algebra expression is long, we can rename intermediate results to make the expression **simpler and more readable**.

3. **Standardizing attribute names:** When combining results from different expressions, Rename ensures **attribute names are consistent** for further operations like Union.

4. **Result labeling:** When the final result of an expression needs a **meaningful name** for reporting or further processing.

---

## Mathematical Formula

If $ R $ is a relation with attributes $ (A_1, A_2, \dots, A_n) $, then the Rename operation is defined as:

### Case 1 — Rename Relation Only

$$
\rho_{S}(R)
$$

Renames the relation $ R $ to $ S $. Attribute names remain unchanged.

### Case 2 — Rename Relation and All Attributes

$$
\rho_{S(B_1,\, B_2,\, \dots,\, B_n)}(R)
$$

Renames the relation $ R $ to $ S $ and simultaneously renames attributes $ A_1, A_2, \dots, A_n $ to $ B_1, B_2, \dots, B_n $.

### Case 3 — Rename for Assignment (Storing Result)

$$
S \leftarrow \rho_{S}(R)
$$

Used to store the result of a relational algebra expression into a named relation $ S $ for later use.

Where:
- $ \rho $ (rho) — denotes the **rename operation**
- $ R $ — is the **original relation** (input)
- $ S $ — is the **new name** assigned to the relation
- $ A_1, A_2, \dots, A_n $ — are the **original attribute names**
- $ B_1, B_2, \dots, B_n $ — are the **new attribute names**

> The Rename operation returns a relation that is **identical in data** to $ R $, but with a new name and/or new attribute names.

---

### Formula Example

**Original Relation — Students:**

| student\_id | student\_name | dept |
| ----------- | ------------- | ---- |
| 101         | Aarav Sharma  | CSE  |
| 102         | Diya Mehta    | ECE  |
| 103         | Rohan Das     | IT   |

**Applying Rename — relation only:**

$$
\rho_{\text{Learners}}(\text{Students})
$$

**Result Relation — Learners (data unchanged, only name changed):**

| student\_id | student\_name | dept |
| ----------- | ------------- | ---- |
| 101         | Aarav Sharma  | CSE  |
| 102         | Diya Mehta    | ECE  |
| 103         | Rohan Das     | IT   |

**Applying Rename — relation and all attributes:**

$$
\rho_{\text{Learners}(\text{id},\, \text{name},\, \text{department})}(\text{Students})
$$

**Result Relation — Learners (relation and all attribute names changed):**

| id  | name         | department |
| --- | ------------ | ---------- |
| 101 | Aarav Sharma | CSE        |
| 102 | Diya Mehta   | ECE        |
| 103 | Rohan Das    | IT         |

> The **data is exactly the same** — only the relation name changed from `Students` to `Learners`, and the attribute names changed from `student_id`, `student_name`, `dept` to `id`, `name`, `department`.

---

## Notation

$$
\rho_{S}(R)
$$

$$
\rho_{S(B_1,\, B_2,\, \dots,\, B_n)}(R)
$$

Where:
- $ \rho $ — denotes the **rename operation**
- $ S $ — is the **new relation name**
- $ B_1, B_2, \dots, B_n $ — are the **new attribute names** (optional)
- $ R $ — is the **input relation**

---

## Properties of Rename Operation

- **Unary Operation:** Takes exactly **one relation** as input.
- **No Data Change:** Rename does **not** modify any tuples — the data remains identical.
- **Same Degree and Cardinality:** The result has the **same number of columns and rows** as the input.
- **Idempotent in Data:** $ \rho_{S}(R) $ contains exactly the same tuples as $ R $.
- **Reversible:** A renamed relation can always be renamed back to the original name.
- **Used for Disambiguation:** Essential when the same relation appears **more than once** in an expression (e.g., Self-Join).
- **Composable:** Rename can be **combined with any other operation** — Select, Project, Cartesian Product, etc.

---

## Difference Between Rename and Other Operations

| Feature             | Select $ (\sigma) $       | Project $ (\pi) $         | Rename $ (\rho) $                   |
| ------------------- | ------------------------- | ------------------------- | ----------------------------------- |
| Operation Type      | Unary                     | Unary                     | Unary                               |
| Changes Data        | No (filters rows)         | No (filters columns)      | No (changes names only)             |
| Changes Structure   | No                        | Yes (fewer columns)       | No (same columns, new names)        |
| Removes Duplicates  | No                        | Yes                       | No                                  |
| SQL Equivalent      | `WHERE`                   | `SELECT col`              | `AS` (alias)                        |
| Primary Purpose     | Filter rows by condition  | Select specific columns   | Assign new name to relation/columns |

---

## Example Tables

Two separate relations are used throughout all examples below — a **Students** table and an **Alumni** table — both representing people associated with a university.

### Relation — Students

| student\_id | student\_name  | age | dept | cgpa |
| ----------- | -------------- | --- | ---- | ---- |
| 101         | Aarav Sharma   | 20  | CSE  | 8.5  |
| 102         | Diya Mehta     | 22  | ECE  | 9.1  |
| 103         | Rohan Das      | 21  | IT   | 7.8  |
| 104         | Sneha Bose     | 23  | CSE  | 8.0  |
| 105         | Kabir Roy      | 20  | ECE  | 6.5  |

### Relation — Alumni

| alumni\_id | alumni\_name   | age | dept | cgpa |
| ---------- | -------------- | --- | ---- | ---- |
| 201        | Priya Sen      | 25  | CSE  | 8.9  |
| 202        | Arjun Verma    | 27  | IT   | 7.5  |
| 203        | Pooja Nair     | 24  | ECE  | 9.0  |

> **Key Observation:** Students and Alumni have **different attribute names** (`student_id` vs `alumni_id`, `student_name` vs `alumni_name`) but **same domains**. To apply Union between them, we must first use Rename to make them union-compatible.

---

## Examples

---

### Example 1 — Rename a Relation Only

**Question:** Rename the **Students** relation to **Enrollees**, keeping all attribute names unchanged.

**Relational Algebra Expression:**

$$
\rho_{\text{Enrollees}}(\text{Students})
$$

**Solution:** The Rename operation simply assigns the new name `Enrollees` to the `Students` relation. No data is changed — every tuple and every attribute name remains exactly the same.

**Output Relation — Enrollees:**

| student\_id | student\_name | age | dept | cgpa |
| ----------- | ------------- | --- | ---- | ---- |
| 101         | Aarav Sharma  | 20  | CSE  | 8.5  |
| 102         | Diya Mehta    | 22  | ECE  | 9.1  |
| 103         | Rohan Das     | 21  | IT   | 7.8  |
| 104         | Sneha Bose    | 23  | CSE  | 8.0  |
| 105         | Kabir Roy     | 20  | ECE  | 6.5  |

**Equivalent SQL Query:**

```sql
SELECT *
FROM Students AS Enrollees;
```

---

### Example 2 — Rename a Relation and All Its Attributes

**Question:** Rename the **Students** relation to **Persons** and rename its attributes to `id`, `name`, `years`, `branch`, `gpa`.

**Relational Algebra Expression:**

$$
\rho_{\text{Persons}(\text{id},\, \text{name},\, \text{years},\, \text{branch},\, \text{gpa})}(\text{Students})
$$

**Solution:** The Rename operation assigns the new relation name `Persons` and simultaneously renames all 5 attributes. The data in every tuple remains unchanged — only the column headers are replaced.

**Original Attribute Names → New Attribute Names:**

| Original Name   | New Name  |
| --------------- | --------- |
| `student_id`    | `id`      |
| `student_name`  | `name`    |
| `age`           | `years`   |
| `dept`          | `branch`  |
| `cgpa`          | `gpa`     |

**Output Relation — Persons:**

| id  | name         | years | branch | gpa |
| --- | ------------ | ----- | ------ | --- |
| 101 | Aarav Sharma | 20    | CSE    | 8.5 |
| 102 | Diya Mehta   | 22    | ECE    | 9.1 |
| 103 | Rohan Das    | 21    | IT     | 7.8 |
| 104 | Sneha Bose   | 23    | CSE    | 8.0 |
| 105 | Kabir Roy    | 20    | ECE    | 6.5 |

**Equivalent SQL Query:**

```sql
SELECT
  student_id   AS id,
  student_name AS name,
  age          AS years,
  dept         AS branch,
  cgpa         AS gpa
FROM Students AS Persons;
```

---

### Example 3 — Rename to Enable Union

**Question:** Combine the **Students** and **Alumni** relations using Union. Since their attribute names differ, use Rename first to make them union-compatible, then retrieve all people from **CSE**.

**Problem:** Students has `student_id`, `student_name` while Alumni has `alumni_id`, `alumni_name` — they are **not union-compatible** as-is.

**Relational Algebra Expression:**

**Step 1 — Rename Alumni to match Students' attribute names:**

$$
\rho_{\text{Alumni}(\text{student\_id},\, \text{student\_name},\, \text{age},\, \text{dept},\, \text{cgpa})}(\text{Alumni})
$$

**Step 2 — Apply Union:**

$$
\text{Students} \cup \rho_{\text{Alumni}(\text{student\_id},\, \text{student\_name},\, \text{age},\, \text{dept},\, \text{cgpa})}(\text{Alumni})
$$

**Step 3 — Apply Select to get CSE members only:**

$$
\sigma_{\text{dept} = \text{'CSE'}} \left( \text{Students} \cup \rho_{\text{Alumni}(\text{student\_id},\, \text{student\_name},\, \text{age},\, \text{dept},\, \text{cgpa})}(\text{Alumni}) \right)
$$

**Solution:**

**Step 1 — Renamed Alumni (attribute names now match Students):**

| student\_id | student\_name | age | dept | cgpa |
| ----------- | ------------- | --- | ---- | ---- |
| 201         | Priya Sen     | 25  | CSE  | 8.9  |
| 202         | Arjun Verma   | 27  | IT   | 7.5  |
| 203         | Pooja Nair    | 24  | ECE  | 9.0  |

**Step 2 — Union of Students and Renamed Alumni (8 tuples total):**

| student\_id | student\_name | age | dept | cgpa |
| ----------- | ------------- | --- | ---- | ---- |
| 101         | Aarav Sharma  | 20  | CSE  | 8.5  |
| 102         | Diya Mehta    | 22  | ECE  | 9.1  |
| 103         | Rohan Das     | 21  | IT   | 7.8  |
| 104         | Sneha Bose    | 23  | CSE  | 8.0  |
| 105         | Kabir Roy     | 20  | ECE  | 6.5  |
| 201         | Priya Sen     | 25  | CSE  | 8.9  |
| 202         | Arjun Verma   | 27  | IT   | 7.5  |
| 203         | Pooja Nair    | 24  | ECE  | 9.0  |

**Step 3 — Select CSE only:**

**Output Relation:**

| student\_id | student\_name | age | dept | cgpa |
| ----------- | ------------- | --- | ---- | ---- |
| 101         | Aarav Sharma  | 20  | CSE  | 8.5  |
| 104         | Sneha Bose    | 23  | CSE  | 8.0  |
| 201         | Priya Sen     | 25  | CSE  | 8.9  |

**Equivalent SQL Query:**

```sql
SELECT *
FROM (
  SELECT student_id, student_name, age, dept, cgpa FROM Students
  UNION
  SELECT alumni_id AS student_id, alumni_name AS student_name, age, dept, cgpa FROM Alumni
) AS All_People
WHERE dept = 'CSE';
```

---

### Example 4 — Rename to Enable Self-Join (Cartesian Product with Itself)

**Question:** Find all pairs of students who are in the **same department** — using a Self-Join via Cartesian Product and Rename.

**Problem:** We cannot write $ \text{Students} \times \text{Students} $ directly because both copies share the same attribute names, causing **ambiguity**. We rename one copy first.

**Relational Algebra Expression:**

**Step 1 — Rename one copy of Students:**

$$
\rho_{\text{S2}(\text{id2},\, \text{name2},\, \text{age2},\, \text{dept2},\, \text{cgpa2})}(\text{Students})
$$

**Step 2 — Cartesian Product with original Students:**

$$
\text{Students} \times \rho_{\text{S2}(\text{id2},\, \text{name2},\, \text{age2},\, \text{dept2},\, \text{cgpa2})}(\text{Students})
$$

**Step 3 — Select rows where dept matches and student IDs are different (avoid pairing a student with themselves):**

$$
\sigma_{\text{dept} = \text{dept2} \, \land \, \text{student\_id} < \text{id2}} \left( \text{Students} \times \rho_{\text{S2}(\text{id2},\, \text{name2},\, \text{age2},\, \text{dept2},\, \text{cgpa2})}(\text{Students}) \right)
$$

**Step 4 — Project only the relevant columns:**

$$
\pi_{\text{student\_name},\, \text{name2},\, \text{dept}} \left( \sigma_{\text{dept} = \text{dept2} \, \land \, \text{student\_id} < \text{id2}} \left( \text{Students} \times \rho_{\text{S2}(\text{id2},\, \text{name2},\, \text{age2},\, \text{dept2},\, \text{cgpa2})}(\text{Students}) \right) \right)
$$

**Solution:**

**Step 1 — Renamed copy S2:**

| id2 | name2      | age2 | dept2 | cgpa2 |
| --- | ---------- | ---- | ----- | ----- |
| 101 | Aarav Sharma | 20 | CSE   | 8.5   |
| 102 | Diya Mehta   | 22 | ECE   | 9.1   |
| 103 | Rohan Das    | 21 | IT    | 7.8   |
| 104 | Sneha Bose   | 23 | CSE   | 8.0   |
| 105 | Kabir Roy    | 20 | ECE   | 6.5   |

**Step 2 — Cartesian Product** produces $ 5 \times 5 = 25 $ tuples.

**Step 3 — After Select** (same dept AND student\_id < id2 to avoid duplicates and self-pairs):

| student\_id | student\_name | dept | id2 | name2      | dept2 |
| ----------- | ------------- | ---- | --- | ---------- | ----- |
| 101         | Aarav Sharma  | CSE  | 104 | Sneha Bose | CSE   |
| 102         | Diya Mehta    | ECE  | 105 | Kabir Roy  | ECE   |

**Step 4 — After Project:**

**Output Relation (Student pairs in the same department):**

| student\_name | name2      | dept |
| ------------- | ---------- | ---- |
| Aarav Sharma  | Sneha Bose | CSE  |
| Diya Mehta    | Kabir Roy  | ECE  |

**Equivalent SQL Query:**

```sql
SELECT S1.student_name, S2.student_name AS name2, S1.dept
FROM Students AS S1
CROSS JOIN Students AS S2
WHERE S1.dept = S2.dept
  AND S1.student_id < S2.student_id;
```

---

### Example 5 — Rename to Simplify a Complex Expression

**Question:** Find all students with **cgpa > 8.0** from the **CSE** department and store the result as a named relation **TopCSE** for further use.

**Relational Algebra Expression:**

$$
\rho_{\text{TopCSE}} \left( \sigma_{\text{dept} = \text{'CSE'} \, \land \, \text{cgpa} > 8.0}(\text{Students}) \right)
$$

**Solution:** The inner expression first applies Select to filter CSE students with cgpa > 8.0. The outer Rename then assigns the meaningful name `TopCSE` to this intermediate result — making it reusable in further expressions.

**Inner Select Result:**

| student\_id | student\_name | age | dept | cgpa |
| ----------- | ------------- | --- | ---- | ---- |
| 101         | Aarav Sharma  | 20  | CSE  | 8.5  |

**Output Relation — TopCSE:**

| student\_id | student\_name | age | dept | cgpa |
| ----------- | ------------- | --- | ---- | ---- |
| 101         | Aarav Sharma  | 20  | CSE  | 8.5  |

> **Note:** Sneha Bose (104) has cgpa = 8.0 which is **NOT** greater than 8.0, so she is excluded.

**Equivalent SQL Query:**

```sql
SELECT *
FROM Students AS TopCSE
WHERE dept = 'CSE' AND cgpa > 8.0;
```

---

### Example 6 — Rename with Project

**Question:** Retrieve only the **name** and **department** of all students, and rename the result relation to **StudentSummary** with attributes renamed to `full_name` and `branch`.

**Relational Algebra Expression:**

$$
\rho_{\text{StudentSummary}(\text{full\_name},\, \text{branch})} \left( \pi_{\text{student\_name},\, \text{dept}}(\text{Students}) \right)
$$

**Solution:**

**Step 1 — Apply Project:** Extract only `student_name` and `dept` columns.

| student\_name | dept |
| ------------- | ---- |
| Aarav Sharma  | CSE  |
| Diya Mehta    | ECE  |
| Rohan Das     | IT   |
| Sneha Bose    | CSE  |
| Kabir Roy     | ECE  |

**Step 2 — Apply Rename:** Rename the relation to `StudentSummary` and attributes to `full_name` and `branch`.

**Output Relation — StudentSummary:**

| full\_name    | branch |
| ------------- | ------ |
| Aarav Sharma  | CSE    |
| Diya Mehta    | ECE    |
| Rohan Das     | IT     |
| Sneha Bose    | CSE    |
| Kabir Roy     | ECE    |

**Equivalent SQL Query:**

```sql
SELECT
  student_name AS full_name,
  dept         AS branch
FROM Students AS StudentSummary;
```

---

## Summary

| Aspect                  | Detail                                                                              |
| ----------------------- | ----------------------------------------------------------------------------------- |
| Operation Type          | Unary                                                                               |
| Symbol                  | $ \rho $                                                                            |
| Input                   | Any relation                                                                        |
| Output                  | Same relation with a new name and/or new attribute names                            |
| Formula (relation only) | $ \rho_{S}(R) $                                                                    |
| Formula (relation + attributes) | $ \rho_{S(B_1,\, B_2,\, \dots,\, B_n)}(R) $                              |
| Changes Data            | No — data is identical to the input                                                 |
| Changes Degree          | No — same number of columns                                                         |
| Changes Cardinality     | No — same number of rows                                                            |
| Removes Duplicates      | No                                                                                  |
| Commutative             | N/A (unary operation)                                                               |
| Primary Uses            | Self-Join disambiguation, Union compatibility, expression simplification, labeling  |
| SQL Equivalent          | `AS` keyword (alias)                                                                |