# INSERT, UPDATE, DELETE — modifying data

[← All topics](../README.md)

## 88. Discount on Action games

*easy* · Dialects: PostgreSQL, MySQL

The store is launching a weekend promotion: 10% off all games in the `Action` genre. Update the catalog prices of those games so that each such price is multiplied by `0.9`.

**Tables:**

- **players**: `id` int 🔑; `name` varchar(100); `email` varchar(255); `city` varchar(100); `registered_at` date
- **games**: `id` int 🔑; `title` varchar(200); `genre` varchar(100); `price` decimal(10,2); `stock` int
- **orders**: `id` int 🔑; `player_id` int → players.id; `created_at` timestamp; `status` varchar(20)
- **order_items**: `id` int 🔑; `order_id` int → orders.id; `game_id` int → games.id; `quantity` int; `price` decimal(10,2)

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/discount-action-games?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 89. Seed a batch of test orders

*easy* · Dialects: PostgreSQL, MySQL

To run a scenario across multiple order statuses you need fixture data.

Insert into `orders` in a single statement three rows for `user_id = 1`:

| id  | status     | amount |
|-----|------------|--------|
| 501 | PAID       | 100.00 |
| 502 | PENDING    | 250.00 |
| 503 | CANCELLED  | 75.50  |

`created_at` = `CURRENT_TIMESTAMP`.

**Tables:**

- **users**: `id` int 🔑; `email` varchar(255)
- **orders**: `id` int 🔑; `user_id` int → users.id; `status` varchar(20); `amount` decimal(10,2); `created_at` timestamp

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/qa-seed-test-orders?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 90. Spring cleaning — drop everything unpinned

*easy* · Dialects: PostgreSQL

Twice a year you do a spring clean of your journal: anything you didn't pin manually counts as noise and goes. From `notes` delete every row where `is_pinned = FALSE`. Pinned notes (`is_pinned = TRUE`) survive.

**Tables:**

- **notes**: `id` serial 🔑; `title` varchar(120); `body` text; `is_pinned` boolean; `created_at` date

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/easy-dml-delete-unpinned?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 91. Save your first journal entry

*easy* · Dialects: PostgreSQL

You're building a Notion-style journal app and want to verify that saving a new entry works. Insert one row into `notes`: put `Привет SQL` into `title` and `Первая запись через INSERT` into `body` — the journal keeps its notes in Russian, so copy both values exactly as written. Leave `id`, `is_pinned`, and `created_at` alone — they fill in from defaults.

**Tables:**

- **notes**: `id` serial 🔑; `title` varchar(120); `body` text; `is_pinned` boolean; `created_at` date

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/easy-dml-insert-note?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 92. Pin every January note for the new year

*easy* · Dialects: PostgreSQL

For the new year you decided to surface every January note — they turned out to be the most useful of the year. In `notes` set `is_pinned = TRUE` for every row whose `created_at` falls in January 2024 inclusive — both January 1 and January 31 should be included. Leave the rest as they are.

**Tables:**

- **notes**: `id` serial 🔑; `title` varchar(120); `body` text; `is_pinned` boolean; `created_at` date

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/easy-dml-pin-old-notes?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 93. Add a test user

*easy* · Dialects: PostgreSQL, MySQL

In the bug-tracker test environment you need to create a QA account.

Insert into `users` a new row with:
- `id` = 101
- `email` = `qa.test@example.com`
- `role_id` = 1 (tester role)
- `is_active` = true
- `created_at` = current timestamp (`CURRENT_TIMESTAMP`)

**Tables:**

- **roles**: `id` int 🔑; `name` varchar(50)
- **users**: `id` int 🔑; `email` varchar(255); `role_id` int → roles.id; `is_active` boolean; `created_at` timestamp

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/qa-insert-test-user?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**
