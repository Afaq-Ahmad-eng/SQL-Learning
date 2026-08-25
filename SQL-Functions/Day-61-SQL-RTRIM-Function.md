# SQL RTRIM() Function:

The `RTRIM()` function is used in SQL to remove trailing spaces from the right end of a string. It helps clean and standardize text data for better storage and comparison.

- Does not remove leading (left-side) spaces.

- Supported by MySQL and MariaDB (and, with the same name, by several other major databases such as SQL Server and Oracle).

---

## Syntax:

```sql
RTRIM(input_text);
```

- `RTRIM(input_text)` removes trailing spaces from a string or expression.

- `RTRIM(column_name)` removes trailing spaces from a column's values, the same way it works on a literal string.

---

**Query:**

```sql
SELECT RTRIM('Hello World     ') AS trimmed_text;
```

**Output:**

![RTRIM](../src/assets/Day-61-SQL-RTRIM-Function-Practice-images/RTRIM()-Output.png)

- Removes extra spaces from the right side of the text.

- Returns the cleaned result as `trimmed_text`.

---

> **Important:** In MySQL and MariaDB, `RTRIM()` takes **only one argument** and removes **whitespace only** — there is no `trim_characters` parameter. To strip a specific trailing character or substring instead of spaces, use `TRIM(TRAILING 'characters' FROM string)`:

 ```sql
 SELECT TRIM(TRAILING '-' FROM 'Afaq Ahmad----') AS trimmed_text;
```

---

## Examples:

Let's look at a few examples of the `RTRIM()` function to understand how it works.

### Example 1: Remove Trailing Spaces from a String:

**Query:**

```sql
SELECT CONCAT('[', 'Afaq Ahmad Khan          ', ']') AS before_rtrim,
       CONCAT('[', RTRIM('Afaq Ahmad Khan          '), ']') AS after_rtrim;
```

**Output:**

![CONCAT and RTRIM](../src/assets/Day-61-SQL-RTRIM-Function-Practice-images/CONCAT-&-RTRIM()-Output.png)

- Displays the original string with trailing spaces as `before_rtrim`.

- Removes only the right-side (trailing) spaces and shows the result as `after_rtrim`.

> Note: the square brackets are just a visual trick to make trailing spaces visible in the output — they have nothing to do with `RTRIM()` itself. Also note this example uses `CONCAT()` rather than the `||` operator: in both MySQL and MariaDB, `||` means logical OR by default (not string concatenation), so `'a' || 'b'` normally evaluates to `0`/`1`, not `'ab'`. `CONCAT()` is the safe, portable way to join strings on both engines.

### Example 2: Combine RTRIM() with Other String Functions:

`RTRIM()` is commonly chained with other string functions when cleaning up free-form text — for example, trimming trailing spaces before appending a suffix:

**Query:**

```sql
SELECT CONCAT(RTRIM('Hello          '), ' World') AS result;
```

**Output:**

![RTRIM and CONCAT](../src/assets/Day-61-SQL-RTRIM-Function-Practice-images/CONCAT-&-RTRIM()-1-Output.png)

- `RTRIM()` removes the trailing spaces from `'Hello          '` first.

- `CONCAT()` then appends `' World'` to the trimmed result, producing a single clean value instead of `'Hello           World'` (with the leftover gap baked in).

### Example 3: Using RTRIM() Inside a Stored Procedure:

This example shows `RTRIM()` used with a local variable inside a stored procedure to clean up a value before using it further:

**Query:**

```sql
DELIMITER //

CREATE PROCEDURE rtrim_example()
BEGIN
    DECLARE input_string VARCHAR(15);

    SET input_string = 'Hello          ';

    SELECT CONCAT(RTRIM(input_string), ' World') AS result;
END //

DELIMITER;

CALL rtrim_example();
```

**Output:**

![DELIMITER with CONCAT and RTRIM](../src/assets/Day-61-SQL-RTRIM-Function-Practice-images/DELIMITER-With-CONCAT-RTRIM()-Output.png)

- Creates a stored procedure that trims trailing spaces from a local variable using `RTRIM()`.

- Uses `CONCAT()` to append `' World'` to the trimmed string.

- Changes the delimiter to `//` so the entire procedure body which itself contains semicolons is sent to the server as a single statement, then restores the delimiter to `;` afterward.

- Executes the procedure with `CALL rtrim_example();`.

---

## Related Functions

| Function | Purpose |
|---|---|
| `RTRIM(str)` | Removes trailing (right-side) spaces only |
| `LTRIM(str)` | Removes leading (left-side) spaces only |
| `TRIM(str)` | Removes both leading and trailing spaces |
| `TRIM(TRAILING remstr FROM str)` | Removes a specific character/substring from the end |
| `TRIM(LEADING remstr FROM str)` | Removes a specific character/substring from the start |
| `TRIM(BOTH remstr FROM str)` | Removes a specific character/substring from both ends |

`RTRIM()` is supported identically in MySQL and MariaDB.

---

## References:

- [GEEKS FOR GEEKS](https://www.geeksforgeeks.org/sql/rtrim-function-in-sql)

- [MySQL RTRIM() Function](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_rtrim)

- [MariaDB RTRIM Function](https://mariadb.com/docs/server/reference/sql-functions/string-functions/rtrim)

- [MariaDB TRIM Function](https://mariadb.com/docs/server/reference/sql-functions/string-functions/trim)

---

[← Back to main README](./README.md) | [← Previous Day (Day 60)](./Day-60-SQL-UPPER-Function.md) | [Next Day (Day 62) →](./Day-62-Regular-Expressions-in-SQL.md)