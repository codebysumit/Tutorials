# Relational Algebra (Part #1)

Relational algebra is a <mark>procedural query language</mark>, which takes instances of relations as input and yields instances of relations as output. It uses operators to perform queries. An operator can be either unary or binary. They accept relations as their input and yield relations as their output. Relational algebra is performed recursively on a relation, and intermediate results are also considered relations.

## Key Concepts in Relational Algebra

Before explaining relational algebra operations, let's define some fundamental concepts:

- **Relations:** In relational algebra, a relation is a table that consists of rows and columns, representing data in a structured format. Each relation has a unique name and is made up of tuples.

  ### Students Table

  | id  | name       | age | gender |
  | --- | ---------- | --- | ------ |
  | 1   | Sumit Das  | 21  | M      |
  | 2   | Sumana Das | 26  | F      |

- **Tuples:** A tuple is a single row in a relation, which contains a set of values for each attribute. It represents a single data entry or record in a relational table.

  | id  | name      | age | gender |
  | --- | --------- | --- | ------ |
  | 1   | Sumit Das | 21  | M      |

- **Attributes:** Attributes are the columns in a relation, each representing a specific characteristic or property of the data. For example, in a "Students" relation, attributes could be "Id", "Name", "Age", and "Grade".

- **Domains:** A domain is the set of possible values that an attribute can have. It defines the type of data that can be stored in each column of a relation, such as integers, strings, or dates.

  **Example:** The domain of a "Gender" attribute is: Male (M), Female (F), Others (O).

## Operations of Relational Algebra

![Types of Operators in Relational Algebra](https://media.geeksforgeeks.org/wp-content/uploads/20251029174238856656/types_of_operators_in_relational_algebra.webp)

The fundamental operations of relational algebra are as follows −

- Select $ (\sigma) $
- Project $ (\pi) $
- Union $ (\cup) $
- Difference $ (-) $
- Cartesian Product $ (\times) $
- Rename $ (\rho) $

The additional operations of relational algebra are as follows −

- Intersection $ (\cap) $
- Assignment $ (:=) $
- Division $ (\div) $
- Join $ (\bowtie) $
  - Inner Join
    - Equi Join
    - Conditional Join
    - Natural Join
  - Outer Join
    - Left Outer Join $ (⟕) $
    - Right Outer Join $ (⟖) $
    - Full Outer Join $ (⟗) $
