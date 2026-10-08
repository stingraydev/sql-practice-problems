# CREATE and ALTER TABLE — table design

[← All topics](../README.md)

## 94. Drop the Departments Table

*easy* · Dialects: PostgreSQL, MySQL

Drop the departments table from the database.

**Tables:**

- **departments**: `id` int 🔑; `name` varchar(50)
- **employees**: `id` int 🔑; `name` varchar(100); `salary` int; `dept_id` int; `is_active` boolean

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ddl-drop-departments?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 95. Add Email Column

*easy* · Dialects: PostgreSQL, MySQL

Add a new column email with type VARCHAR(255) to the employees table.

**Tables:**

- **departments**: `id` int 🔑; `name` varchar(50)
- **employees**: `id` int 🔑; `name` varchar(100); `salary` int; `dept_id` int; `is_active` boolean

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ddl-add-email-column?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 96. Drop Salary Column

*easy* · Dialects: PostgreSQL, MySQL

Drop the salary column from the employees table.

**Tables:**

- **departments**: `id` int 🔑; `name` varchar(50)
- **employees**: `id` int 🔑; `name` varchar(100); `salary` int; `dept_id` int; `is_active` boolean

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ddl-drop-salary-column?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 97. Rename Column name

*easy* · Dialects: PostgreSQL, MySQL

In the employees table, rename the column name to full_name.

**Tables:**

- **departments**: `id` int 🔑; `name` varchar(50)
- **employees**: `id` int 🔑; `name` varchar(100); `salary` int; `dept_id` int; `is_active` boolean

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ddl-rename-name-column?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 98. Normalization: split a flat book catalog into authors + books (PK/FK)

*medium* · Dialects: PostgreSQL

In the book department of "Kotomarket", the catalog is stored as a single flat table: each row holds a book title and the **author's full name as plain text**. For prolific authors the name is duplicated across dozens of rows, a typo silently splits one author into two, and there is no standalone "author" entity at all. This violates **Third Normal Form (3NF)**.

Design a replacement schema of **two related tables** so that an author is stored exactly once and every book references it by key.

Create (only `CREATE TABLE`, **no** `DROP` / `IF EXISTS` / `CASCADE`):

1. **`authors`** — author reference table:
   - `author_id` — integer **PRIMARY KEY**;
   - `name` — author name, text, NOT NULL.

2. **`books`** — book catalog:
   - `book_id` — integer **PRIMARY KEY**;
   - `title` — book title, text, NOT NULL;
   - `author_id` — integer, NOT NULL, **FOREIGN KEY** referencing `authors(author_id)`.

Create `authors` **before** `books`, otherwise the foreign key would point to a table that does not exist yet.

No inserts or selects are needed — only the schema structure is checked (a PK on both tables and an FK from `books` to `authors`).

**Tables:**

- **authors**: `author_id` integer 🔑; `name` varchar(100)
- **books**: `book_id` integer 🔑; `title` varchar(200); `author_id` integer

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/gen-m9l5-normalize-books-authors?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 99. Kotomarket: split an order into 3NF

*medium* · Dialects: PostgreSQL

Purchase history is stored in a single table, causing customer and order details to be repeated for every line item. Split the data into three related tables.

Create a `customers` table:

- `customer_id` — an integer primary key;
- `full_name` — a required text field;
- `city` — a nullable text field.

Create an `orders` table:

- `order_id` — an integer primary key;
- `customer_id` — a required integer referencing a customer in the `customers` table;
- `ordered_at` — the required order date.

Create an `order_items` table:

- `item_id` — an integer primary key;
- `order_id` — a required integer referencing an order in the `orders` table;
- `product_name` — a required text field;
- `qty` — a required integer greater than zero.

Link the tables with primary and foreign keys so that an order cannot reference a nonexistent customer and a line item cannot reference a nonexistent order.

Use only `CREATE TABLE` statements. Do not use `DROP`, `IF EXISTS`, or `INSERT`.

**Tables:**

- **customers**: `customer_id` int 🔑; `full_name` text; `city` text
- **orders**: `order_id` int 🔑; `customer_id` int; `ordered_at` date
- **order_items**: `item_id` int 🔑; `order_id` int; `product_name` text; `qty` int

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/gen-ddll5-orders-3nf-split?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**
