# Subqueries

[← All topics](../README.md)

## 57. Find the most expensive item

*easy* · Dialects: PostgreSQL, ClickHouse

The home page designer wants a «premium» card — the most expensive item in the catalogue. If several products share the top price, show them all. Return `id`, name and price, sort by `id`.

**Tables:**

- **customers**: `id` serial 🔑; `name` varchar(100); `country` varchar(2); `registered_at` date
- **products**: `id` serial 🔑; `name` varchar(100); `category` varchar(50); `price` numeric(10, 2)
- **orders**: `id` serial 🔑; `customer_id` int → customers.id; `status` varchar(20); `total` numeric(10, 2); `created_at` date
- **order_items**: `order_id` int 🔑; `product_id` int 🔑; `quantity` int

**Expected columns:** `id`, `name`, `price`

**Expected output (first rows):**

| id | name | price |
|---|---|---|
| 9 | Шкаф | 12000.00 |
| 10 | Диван | 12000.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/easy-subq-most-expensive-product?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 58. Pull orders from Russian customers only

*easy* · Dialects: PostgreSQL, ClickHouse

Accounting is closing the quarter and asks for orders from Russian customers only — for the RU legal-entity report. Return order `id`, `customer_id`, total — only for customers in Russia (country `'RU'`). Sort by order `id`.

**Tables:**

- **customers**: `id` serial 🔑; `name` varchar(100); `country` varchar(2); `registered_at` date
- **products**: `id` serial 🔑; `name` varchar(100); `category` varchar(50); `price` numeric(10, 2)
- **orders**: `id` serial 🔑; `customer_id` int → customers.id; `status` varchar(20); `total` numeric(10, 2); `created_at` date
- **order_items**: `order_id` int 🔑; `product_id` int 🔑; `quantity` int

**Expected columns:** `id`, `customer_id`, `total`

**Expected output (first rows):**

| id | customer_id | total |
|---|---|---|
| 1 | 1 | 350.00 |
| 2 | 1 | 2500.00 |
| 3 | 1 | 1200.00 |
| 5 | 3 | 450.00 |
| 6 | 3 | 990.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/easy-subq-orders-from-ru-customers?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 59. Find orders bigger than average

*easy* · Dialects: PostgreSQL, ClickHouse

The CFO wants to spot «big tickets» — orders whose total beats the average across paid orders (`status = 'paid'`). Cancelled orders don't go into the average, otherwise it'd be skewed. Return the `id` and total of such orders, sort by total descending.

**Tables:**

- **customers**: `id` serial 🔑; `name` varchar(100); `country` varchar(2); `registered_at` date
- **products**: `id` serial 🔑; `name` varchar(100); `category` varchar(50); `price` numeric(10, 2)
- **orders**: `id` serial 🔑; `customer_id` int → customers.id; `status` varchar(20); `total` numeric(10, 2); `created_at` date
- **order_items**: `order_id` int 🔑; `product_id` int 🔑; `quantity` int

**Expected columns:** `id`, `total`

**Expected output (first rows):**

| id | total |
|---|---|
| 4 | 8000.00 |
| 8 | 3900.00 |
| 2 | 2500.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/easy-subq-orders-above-avg?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 60. Customers who already ordered something

*easy* · Dialects: PostgreSQL, ClickHouse

Marketing wants to split the base into those who hit «checkout» at least once (even if they later cancelled) and those who only signed up. Return the `id` and name of customers with at least one order — status doesn't matter. Sort by `id`.

**Tables:**

- **customers**: `id` serial 🔑; `name` varchar(100); `country` varchar(2); `registered_at` date
- **products**: `id` serial 🔑; `name` varchar(100); `category` varchar(50); `price` numeric(10, 2)
- **orders**: `id` serial 🔑; `customer_id` int → customers.id; `status` varchar(20); `total` numeric(10, 2); `created_at` date
- **order_items**: `order_id` int 🔑; `product_id` int 🔑; `quantity` int

**Expected columns:** `id`, `name`

**Expected output (first rows):**

| id | name |
|---|---|
| 1 | Аня |
| 2 | Боб |
| 3 | Вера |
| 4 | Гриша |
| 5 | Дима |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/easy-subq-customers-with-orders?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 61. Products that nobody bought

*easy* · Dialects: PostgreSQL, ClickHouse

The merchandising manager is looking for products that were stocked but nobody ever bought. They go to clearance or get pulled. Return the `id` and name of such products, sort by `id`.

**Tables:**

- **customers**: `id` serial 🔑; `name` varchar(100); `country` varchar(2); `registered_at` date
- **products**: `id` serial 🔑; `name` varchar(100); `category` varchar(50); `price` numeric(10, 2)
- **orders**: `id` serial 🔑; `customer_id` int → customers.id; `status` varchar(20); `total` numeric(10, 2); `created_at` date
- **order_items**: `order_id` int 🔑; `product_id` int 🔑; `quantity` int

**Expected columns:** `id`, `name`

**Expected output (first rows):**

| id | name |
|---|---|
| 9 | Шкаф |
| 10 | Диван |
| 11 | Словарь |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/easy-subq-products-never-ordered?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 62. Show every customer's order count

*easy* · Dialects: PostgreSQL, ClickHouse

Support wants an order count next to every customer — to instantly tell regulars from those who just signed up. For each customer return `id`, name and the total number of their orders of any status (new customer — zero). Name the count column `orders_count`, sort by customer `id`.

**Tables:**

- **customers**: `id` serial 🔑; `name` varchar(100); `country` varchar(2); `registered_at` date
- **products**: `id` serial 🔑; `name` varchar(100); `category` varchar(50); `price` numeric(10, 2)
- **orders**: `id` serial 🔑; `customer_id` int → customers.id; `status` varchar(20); `total` numeric(10, 2); `created_at` date
- **order_items**: `order_id` int 🔑; `product_id` int 🔑; `quantity` int

**Expected columns:** `id`, `name`, `orders_count`

**Expected output (first rows):**

| id | name | orders_count |
|---|---|---|
| 1 | Аня | 3 |
| 2 | Боб | 1 |
| 3 | Вера | 2 |
| 4 | Гриша | 1 |
| 5 | Дима | 2 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/easy-subq-order-count-per-customer?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 63. Cheapest pick in every category

*easy* · Dialects: PostgreSQL, ClickHouse

Marketing is launching a «start cheap in every category» promo — they need one minimum-priced product per category. Return `id`, name, category and price of such products, sort by category.

**Tables:**

- **customers**: `id` serial 🔑; `name` varchar(100); `country` varchar(2); `registered_at` date
- **products**: `id` serial 🔑; `name` varchar(100); `category` varchar(50); `price` numeric(10, 2)
- **orders**: `id` serial 🔑; `customer_id` int → customers.id; `status` varchar(20); `total` numeric(10, 2); `created_at` date
- **order_items**: `order_id` int 🔑; `product_id` int 🔑; `quantity` int

**Expected columns:** `id`, `name`, `category`, `price`

**Expected output (first rows):**

| id | name | category | price |
|---|---|---|---|
| 4 | Книга | books | 450.00 |
| 11 | Словарь | books | 450.00 |
| 1 | Кружка | home | 350.00 |
| 8 | Йога-коврик | sport | 990.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/easy-subq-cheapest-per-category?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 64. Parcel scans after the watermark

*easy* · Dialects: PostgreSQL

You are a data engineer at a logistics platform. Every night an incremental pipeline picks up fresh parcel scans from the parcel_scans table and appends them to the warehouse. The position of the last successful load (the watermark) is stored in the etl_state table — in the row with source_name = `'parcel_scans'` (the table may hold rows for other sources too). Your job is to build the next increment: the scans the pipeline has not seen yet, i.e. those whose time is strictly greater than the watermark. Scans with an unknown time (scan_time IS NULL) are considered not ready and must not be included.

Return columns:
- `scan_id` — scan identifier;
- `parcel_code` — parcel code;
- `hub_code` — sorting hub code;
- `scan_time` — scan time (timestamp, as stored);
- `status` — parcel status (may be NULL — output as is).

Sorting: by scan_time ascending, ties broken by scan_id ascending. A scan whose time equals the watermark exactly is NOT part of the result.

**Tables:**

- **etl_state**: `source_name` text 🔑 — Data source name; `last_loaded_at` timestamp — Watermark: time of the last successful load
- **parcel_scans**: `scan_id` int 🔑 — Scan identifier; `parcel_code` text — Parcel code; `hub_code` text — Sorting hub code; `scan_time` timestamp — Scan time (may be NULL); `status` text — Parcel status at scan time

**Expected columns:** `scan_id`, `parcel_code`, `hub_code`, `scan_time`, `status`

**Expected output (first rows):**

| scan_id | parcel_code | hub_code | scan_time | status |
|---|---|---|---|---|
| 8 | PKG-1006 | HUB-MUC | 2025-06-10 12:00:01 | arrived |
| 9 | PKG-1003 | HUB-BER | 2025-06-10 15:20:00 | delivered |
| 10 | PKG-1007 | HUB-HAM | 2025-06-10 18:45:00 | arrived |
| 11 | PKG-1004 | HUB-MUC | 2025-06-11 05:10:00 | sorted |
| 12 | PKG-1008 | HUB-BER | 2025-06-11 08:00:00 | arrived |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/etl-watermark-parcel-scans?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 65. Documentary watchers

*easy* · Dialects: PostgreSQL

You work at the ReelFlow streaming service. The production team is launching a new documentary lineup and wants to send the announcement only to people who plausibly care: viewers who have already watched at least one title of the documentary genre. Watch events live in watch_history, profiles in viewers.

Build the mailing list using an EXISTS check: a viewer makes the list if they have at least one watch record with genre `'documentary'`. Each viewer must appear exactly once, no matter how many documentaries they watched.

Return columns:
- `viewer_id` — the viewer's id;
- `viewer_name` — their name.

Sort by viewer_id ascending.

**Tables:**

- **viewers**: `id` int 🔑 — Viewer id; `full_name` text — Viewer name; `country` text — Country
- **watch_history**: `id` int 🔑 — Watch event id; `viewer_id` int — Viewer id; `title` text — Title; `genre` text — Genre; `watched_on` date — Watch date

**Expected columns:** `viewer_id`, `viewer_name`

**Expected output (first rows):**

| viewer_id | viewer_name |
|---|---|
| 1 | Alice Morgan |
| 3 | Chloe Dubois |
| 5 | Emma Stone |
| 9 | Iris Vega |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/lsa-documentary-watchers?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**
