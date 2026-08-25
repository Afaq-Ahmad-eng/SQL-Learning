# SQL LTRIM() Function

The `LTRIM()` function in SQL is a built-in string function used to remove leading spaces from the left side of a string.

- `LTRIM()` is used to clean data in databases.
- It removes unnecessary leading whitespace from text values.
- Data administrators use it to streamline data-cleaning tasks efficiently in one go.

---

## Syntax:

```sql
LTRIM(String)
```

- `String`: the string (or column) from which you want to remove leading spaces.

> **Important:** In MySQL and MariaDB, `LTRIM()` takes **only one argument** and removes **whitespace only** — it does not accept a second "characters to remove" argument. (Some other databases, such as Oracle, support a two-argument `LTRIM(string, trim_set)` form; that syntax is not valid in MySQL or MariaDB and will raise a syntax error.) To strip specific characters rather than spaces, use `TRIM(LEADING 'characters' FROM string)` instead — shown in Example 1 below.

**Query:**

```sql
SELECT LTRIM('     GeeksforGeeks.') AS trimmedString;
```

**Output:**

![LTRIM](../src/assets/Day-59-SQL-LTRIM()-Function-Practice-images/LTRIM()-Output.png)

---

## Examples of SQL LTRIM():

Let's look at a few examples to understand how `LTRIM()` and its related function `TRIM()` work in practice.

### Example 1: Remove Specific Characters (Not Just Spaces):

`LTRIM()` itself only strips leading spaces. To remove a specific leading character or set of characters in MySQL/MariaDB, use `TRIM(LEADING ... FROM ...)`:

**Query:**

```sql
SELECT TRIM(LEADING '-' FROM '----Afaq Ahmad') AS TrimmedString;
```

**Output:**

![TRIM and LEADING](../src/assets/Day-59-SQL-LTRIM()-Function-Practice-images/TRIM-&-LEADING()-Output.png)

- Removes the `-` characters from the left side of the string.
- Returns the cleaned result as `TrimmedString`.

### Example 2: Remove a Leading Substring:

`TRIM(LEADING ...)` removes complete occurrences of the given substring from the start of the string it strips it only if it actually appears at the beginning:

**Query:**

```sql
SELECT TRIM(LEADING 'Khan' FROM 'Khan Afaq Ahmad') AS TrimmedString;
```

**Output:**

![TRIM and LEADING Name](../src/assets/Day-59-SQL-LTRIM()-Function-Practice-images/TRIM-&-LEADING()-Name-Output.png)

- Removes the leading occurrence of `'Geeks'` from the string.
- The trailing `'Geeks'` is left untouched, since `TRIM(LEADING ...)` only strips from the start.

### Example 3: Combine LTRIM() with Other String Functions:

`LTRIM()` is commonly combined with other string functions when cleaning free-form text. For example, trimming leading spaces and then converting the result to uppercase:

**Query:**

```sql
SELECT UPPER(LTRIM('   hello world')) AS CleanedString;
```

**Output:**

![UPPER and LTRIM](../src/assets/Day-59-SQL-LTRIM()-Function-Practice-images/UPPER-LTRIM()-Output.png)

- `LTRIM()` removes the leading spaces first.
- `UPPER()` then converts the trimmed result to uppercase.
- This pattern is common in data-cleaning pipelines where several transformations are chained together in a single expression.

---

## Related Functions

| Function | Purpose |
|---|---|
| `LTRIM(str)` | Removes leading (left-side) spaces only |
| `RTRIM(str)` | Removes trailing (right-side) spaces only |
| `TRIM(str)` | Removes both leading and trailing spaces |
| `TRIM(LEADING remstr FROM str)` | Removes a specific character/substring from the start |
| `TRIM(TRAILING remstr FROM str)` | Removes a specific character/substring from the end |
| `TRIM(BOTH remstr FROM str)` | Removes a specific character/substring from both ends |

Both `LTRIM()` and `TRIM()` are supported identically in MySQL and MariaDB.

---

## References:

- [GEEKS FOR GEEKS](https://www.geeksforgeeks.org/sql/sql-conversion-function)

- [MySQL TRIM() Function](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_trim)

- [MariaDB LTRIM Function](https://mariadb.com/docs/server/reference/sql-functions/string-functions/ltrim)

- [MariaDB TRIM Function](https://mariadb.com/docs/server/reference/sql-functions/string-functions/trim)


---

[← Back to main README](./README.md) | [← Previous Day (Day 58)](./Day-58-Conversion-Function-in-SQL.md) | [Next Day (Day 60) →](./Day-60-SQL-UPPER()-Function.md)