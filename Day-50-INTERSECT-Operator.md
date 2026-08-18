# SQL INTERSECT Clause

## Introduction

The `INTERSECT` operator in SQL is used to return only the records that appear in **both** of two `SELECT` query results. It acts like the intersection of two sets, showing only the common rows shared between them.

**Key Points:**
- Returns rows present in both `SELECT` statements
- Automatically removes duplicates
- Useful for finding overlapping or matching data across tables or queries
- Treats `NULL` values as equal when comparing rows
- Both `SELECT` queries must return the same number of columns, with compatible data types, in the same order

---

## Syntax

```sql
SELECT column1, column2, ...
FROM table1
WHERE condition
INTERSECT
SELECT column1, column2, ...
FROM table2
WHERE condition;
```

**Rules to remember:**
1. The number of columns and their order must match in both `SELECT` statements.
2. The data types of corresponding columns must be compatible.
3. Column names in the output are taken from the first `SELECT` statement.
4. `ORDER BY`, if used, should appear only once — at the end of the entire statement.

---

## Sample Tables

### students

![Students Table](./src/assets/Day-50-INTERSECT-Operator-Practice-images/Student-table.png)

### teaching_assistant

![Teaching Assistant Table](./src/assets/Day-50-INTERSECT-Operator-Practice-images/Teaching_Assistant-image.png)
---

## Example 1: Basic INTERSECT Query

Find students who are also teaching assistants.

**Query:**
```sql
SELECT Name FROM students
INTERSECT
SELECT Name FROM teaching_assistant;
```

**Output:**

![Students who are also teaching assistants](./src/assets/Day-50-INTERSECT-Operator-Practice-images/Intersect-basic-example-image.png)

**Explanation:**
- `Bob`, `Charlie`, and `Emma` appear in both `students` and `teaching_assistant`, so they are returned.
- `Alice` and `David` exist only in `students` — excluded.
- `Farah` exists only in `teaching_assistant` — excluded.
- Duplicate names, if any, are automatically removed from the result.

---

## Example 2: INTERSECT with WHERE / BETWEEN

Find students with `StudentID` between 1 and 4 who are also TAs.

**Query:**
```sql
SELECT Student_id, Name
FROM students
WHERE Student_id BETWEEN 1 AND 4
INTERSECT
SELECT s.Student_id, s.Name
FROM students s
JOIN teaching_assistant t ON s.Name = t.Name;
```

**Output:**

![Students with StudentID between 1 and 4 who are also TAs](./src/assets/Day-50-INTERSECT-Operator-Practice-images/Intersect-with-where-between.png)

**Explanation:**
- The first query filters students with `StudentID` between 1 and 4 (Alice, Bob, Charlie, David).
- The second query returns all students who also appear as TAs (Bob, Charlie, Emma).
- `INTERSECT` keeps only the rows common to both — Bob and Charlie. Emma is excluded because her `StudentID` (5) falls outside the range.

---

## Example 3: INTERSECT with LIKE Operator

Find students whose name starts with 'E' and who are also TAs.

**Query:**
```sql
SELECT Name FROM students
WHERE Name LIKE 'E%'
INTERSECT
SELECT Name FROM teaching_assistant;
```

**Output:**

![Students whose name starts with E and are also TAs](./src/assets/Day-50-INTERSECT-Operator-Practice-images/Intersect-with-like-operator.png)

**Explanation:**
- Only `Emma` starts with 'E' in the `students` table.
- She also exists in `teaching_assistant`, so she satisfies both conditions and is returned.

---

## Example 4: INTERSECT with Multiple Columns

`INTERSECT` can compare more than one column at a time — all columns must match for a row to be included.

**Query:**
```sql
SELECT StudentID, Name FROM students
INTERSECT
SELECT TA_ID, Name FROM teaching_assistant;
```

**Output:**

![No rows returned](./src/assets/Day-50-INTERSECT-Operator-Practice-images/Intersect-multiple-columns.png)

**Explanation:**
- Even though names match (Bob, Charlie, Emma), the ID columns (`StudentID` vs `TA_ID`) don't share any common values (1–5 vs 101–104).
- Since `INTERSECT` compares the **entire row**, not just individual columns, no rows are returned.
- This highlights why it's usually better to select only the columns you actually want compared (like `Name` alone, as in earlier examples).

---

## INTERSECT vs Other Set Operators

| Operator      | Description                                             |
|---------------|-----------------------------------------------------------|
| `UNION`       | Combines results from both queries, removing duplicates   |
| `UNION ALL`   | Combines results from both queries, keeping duplicates    |
| `INTERSECT`   | Returns only rows common to both queries                  |
| `EXCEPT` / `MINUS` | Returns rows from the first query not present in the second |

---

## INTERSECT vs INNER JOIN

`INTERSECT` and `INNER JOIN` can sometimes achieve similar results, but they work differently:

- `INTERSECT` compares entire result sets (row by row) and removes duplicates.
- `INNER JOIN` matches rows based on a specified join condition and can return multiple matching combinations, including duplicates, unless explicitly filtered.

**Equivalent using INNER JOIN:**
```sql
SELECT DISTINCT s.Name
FROM students s
INNER JOIN teaching_assistant t ON s.Name = t.Name;
```

**Output:**

![Students who are also teaching assistants](./src/assets/Day-50-INTERSECT-Operator-Practice-images/Intersect-vs-inner-join.png)

This produces the same result as Example 1, but `INTERSECT` is generally more concise for simple "common rows" comparisons.

---

## Database Support

| Database    | INTERSECT Support                     |
|-------------|----------------------------------------|
| PostgreSQL  | Supported                            |
| SQL Server  | Supported                            |
| Oracle      | Supported                            |
| SQLite      | Supported                            |
| MySQL       | Supported from version 8.0.31+ only  |

**MySQL Alternative (before 8.0.31):**
```sql
SELECT DISTINCT s.Name
FROM students s
INNER JOIN teaching_assistant t ON s.Name = t.Name;
```

**Output:**

![Students who are also teaching assistants](./src/assets/Day-50-INTERSECT-Operator-Practice-images/Intersect-vs-inner-join-another-example.png)

---

## Performance Notes

- `INTERSECT` involves comparing and de-duplicating full result sets, which can be slower on large datasets.
- Indexing the columns being compared (e.g., `Name`) can significantly improve performance.
- If duplicates aren't a concern and you only need matching rows based on a key, an `INNER JOIN` may perform better and offer more flexibility (e.g., selecting additional columns from either table).

---

## Summary

- `INTERSECT` returns only the rows that exist in **both** `SELECT` query results.
- Duplicates are automatically removed from the final output.
- Column count, order, and data types must match between the two queries.
- Useful for finding overlapping data — like students who are also teaching assistants.
- Not supported in older MySQL versions; use `INNER JOIN` with `DISTINCT` as a workaround.
- For large datasets, consider indexing and evaluate whether `INNER JOIN` might be more efficient.

---

[← Back to main README](./README.md) | [← Previous Day (Day 49)](./SQL-Special-Operators/Day-49-special_operator-except.md) | [Next Day (Day 51) →](./Day-51-EXISTS-Operator.md)