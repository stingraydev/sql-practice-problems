# Aggregate functions and GROUP BY

[← All topics](../README.md)

## 21. Monthly Sales Pulse

*easy* · Dialects: PostgreSQL

You are an analyst at Bramble Market, a convenience store chain. The CFO is building next year's budget and wants to see the seasonality of 2025: which months sold more orders and how much revenue they brought. The `store_orders` table spans several years, but only 2025 matters here.

For every month of 2025 that has at least one order, count the orders and total the revenue. Months without orders must not appear.

Return columns:
- `month_num` — month number (integer 1 to 12);
- `orders_cnt` — number of orders in that month (integer);
- `revenue_total` — total revenue of the month, rounded to 2 decimals.

Sort by `month_num` ascending. Orders from other years are ignored entirely; the data contains no duplicate orders.

**Tables:**

- **store_orders**: `order_id` bigint 🔑 — Order identifier; `ordered_on` date — Order date; `amount` numeric(10,2) — Order amount

**Expected columns:** `month_num`, `orders_cnt`, `revenue_total`

**Expected output (first rows):**

| month_num | orders_cnt | revenue_total |
|---|---|---|
| 1 | 2 | 200.50 |
| 2 | 3 | 256.00 |
| 3 | 1 | 99.99 |
| 4 | 2 | 245.50 |
| 5 | 1 | 75.25 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/dtm-monthly-sales-pulse?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 22. Listening Hours by Month

*easy* · Dialects: PostgreSQL

You are a product analyst at Wavelane, a music streaming service. The growth team tracks engagement and wants a monthly view: how many plays users started and how many total hours of music they listened to. In `play_events` each row is a single playback with its exact start time and duration in seconds.

Group the plays by calendar month and compute totals. A month must be represented by its first day. A play belongs to the month of its start moment, even if it lasted into the next month.

Return columns:
- `month_start` — first day of the month (date, YYYY-MM-DD);
- `plays_cnt` — number of plays in the month (integer);
- `hours_listened` — total listening hours, rounded to 1 decimal.

Sort by `month_start` ascending. Zero-length plays count towards `plays_cnt` but add 0 hours. Months without events must not appear.

**Tables:**

- **play_events**: `play_id` bigint 🔑 — Playback identifier; `user_id` bigint — Listener identifier; `played_at` timestamp — Playback start moment; `seconds_played` int — Listening duration in seconds

**Expected columns:** `month_start`, `plays_cnt`, `hours_listened`

**Expected output (first rows):**

| month_start | plays_cnt | hours_listened |
|---|---|---|
| 2026-01-01 | 3 | 0.7 |
| 2026-02-01 | 4 | 0.9 |
| 2026-03-01 | 4 | 1.1 |
| 2026-04-01 | 5 | 1.3 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/dtm-streaming-monthly-hours?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 23. Store delivery scorecard

*easy* · Dialects: PostgreSQL

You are a data analyst at a convenience store chain. The head of operations is preparing a weekly summary of online orders and wants a per-store picture: how many orders were placed in total, how many reached the customer, how many were cancelled, and how much revenue came from delivered orders only. The data lives in the orders table: one row per order, status is one of `'delivered'`, `'cancelled'`, `'returned'`, and the order amount is always present (never NULL).

Conditional metrics are computed with conditional aggregation: a CASE expression inside an aggregate function.

Return columns:
- `store` — store name (text);
- `total_orders` — total number of the store's orders (integer);
- `delivered_cnt` — number of orders with status `'delivered'` (integer);
- `cancelled_cnt` — number of orders with status `'cancelled'` (integer);
- `delivered_revenue` — sum of amount over delivered orders only, rounded to 2 decimals; 0 if the store has no delivered orders.

Sorting: by store ascending. Every store present in the table appears exactly once; the `'returned'` status only contributes to total_orders.

**Tables:**

- **orders**: `order_id` integer 🔑 — Order id; `store` text — Store name; `status` text — Order status: 'delivered', 'cancelled' or 'returned'; `amount` numeric(10,2) — Order amount

**Expected columns:** `store`, `total_orders`, `delivered_cnt`, `cancelled_cnt`, `delivered_revenue`

**Expected output (first rows):**

| store | total_orders | delivered_cnt | cancelled_cnt | delivered_revenue |
|---|---|---|---|---|
| downtown | 5 | 3 | 1 | 245.50 |
| harbor | 4 | 2 | 2 | 259.50 |
| uptown | 6 | 3 | 1 | 206.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/aag-store-delivery-scorecard?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 24. A Customer's First Digital Footprint

*easy* · Dialects: PostgreSQL

You are a product analyst at Northstar, a mobile banking startup. The onboarding team wants to know when each customer first became active in the app so future acquisition campaigns can be compared by activation speed.

The `app_events` table stores customer actions. A customer may generate several events on the same day, including events with identical timestamps. Rows where `occurred_at IS NULL` are incomplete technical records and must be ignored. Customers with no event that has a valid timestamp must not appear in the result.

Find the calendar date of each customer's earliest activity.

Return:
- `user_id` — customer identifier;
- `first_activity_date` — earliest activity date in `YYYY-MM-DD` format.

Sort by `user_id` ascending. Duplicate events must not create extra rows.

**Tables:**

- **app_events**: `event_id` bigint 🔑 — Unique event identifier; `user_id` bigint — Customer identifier; `event_type` text — Type of in-app action; `occurred_at` timestamp — Event timestamp; may be NULL

**Expected columns:** `user_id`, `first_activity_date`

**Expected output (first rows):**

| user_id | first_activity_date |
|---|---|
| 101 | 2026-01-05 |
| 102 | 2026-01-03 |
| 103 | 2026-01-08 |
| 104 | 2026-01-12 |
| 105 | 2025-12-31 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ret-first-banking-activity?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 25. Duplicate Parcel Registrations

*easy* · Dialects: PostgreSQL

You are the data quality analyst for a last-mile delivery platform. Warehouses upload parcel registrations in batches, and retrying a file can create several rows for the same physical parcel. Before carrier compensation is calculated, the billing team needs a duplicate audit so one parcel is not charged more than once.

A registration's business key is the pair `carrier_code` + `tracking_number`. Consider only rows where both key components are present: the value is not `NULL` and is not empty after trimming leading and trailing spaces. Find business keys that occur more than once, count all rows in each duplicate group, and identify the first and last registration times.

Business-key comparison is exact and case-sensitive. Count every row in a matching group, even when all non-key fields are identical.

**Return columns:**
- `carrier_code` — carrier code, text;
- `tracking_number` — tracking number, text;
- `duplicate_count` — number of rows with this business key, integer;
- `first_registered_at` — earliest registration time, timestamp with time zone;
- `last_registered_at` — latest registration time, timestamp with time zone.

Sort by `duplicate_count` descending, then by `carrier_code` and `tracking_number` ascending. No rounding is required. Rows with an incomplete business key must be excluded. Resolve count ties with the stated secondary sort fields.

**Tables:**

- **parcel_registrations**: `registration_id` bigint 🔑 — Unique registration row identifier; `carrier_code` text — Carrier code; `tracking_number` text — Parcel tracking number; `warehouse_code` text — Source warehouse code; `registered_at` timestamptz — Parcel registration time; `registration_status` text — Registration processing status

**Expected columns:** `carrier_code`, `tracking_number`, `duplicate_count`, `first_registered_at`, `last_registered_at`

**Expected output (first rows):**

| carrier_code | tracking_number | duplicate_count | first_registered_at | last_registered_at |
|---|---|---|---|---|
| FEDEX | FX3002 | 3 | 2026-05-01 11:20:00+00 | 2026-05-01 11:45:00+00 |
| DHL | TRK1001 | 2 | 2026-05-01 09:00:00+00 | 2026-05-01 09:05:00+00 |
| UPS | UP2001 | 2 | 2026-05-01 10:10:00+00 | 2026-05-01 11:00:00+00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/dqa-duplicate-parcel-business-keys?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 26. Purchase Frequency in an Audio App

*easy* · Dialects: PostgreSQL

You analyze monetization for an audiobook app. The subscription team wants to compare every listener by the number of completed purchases in Q2 2026, including people who bought nothing. Each purchase record counts separately, even when the same listener made two purchases at the exact same second.

**Return columns:**
- `listener_id` — listener identifier, integer
- `listener_name` — listener name
- `purchase_frequency` — number of completed purchases from `2026-04-01` inclusive to `2026-07-01` exclusive, integer

**Rules:**
- Return every listener from `listeners`, including those with frequency `0`.
- Count only rows with status `completed` and a non-NULL `completed_at` inside the specified half-open interval.
- Different `purchase_id` values are separate purchases; identical timestamps are not duplicates.
- Sort by `purchase_frequency` descending, then `listener_id` ascending.
- No rounding is needed; `purchase_frequency` must not be `NULL`.

**Tables:**

- **listeners**: `listener_id` integer 🔑 — Listener identifier; `listener_name` varchar(100) — Listener name; `plan_name` varchar(30) — Current plan
- **purchases**: `purchase_id` integer 🔑 — Purchase identifier; `listener_id` integer — Listener identifier; `product_type` varchar(30) — Purchased product type; `status` varchar(20) — Purchase status; `completed_at` timestamp — Purchase completion timestamp; `amount` numeric(10,2) — Purchase amount

**Expected columns:** `listener_id`, `listener_name`, `purchase_frequency`

**Expected output (first rows):**

| listener_id | listener_name | purchase_frequency |
|---|---|---|
| 1 | Avery Stone | 3 |
| 4 | Devon Lake | 3 |
| 3 | Casey Moon | 2 |
| 7 | Gray Cole | 2 |
| 10 | Jordan Pike | 2 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/rfm-quarterly-purchase-frequency?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 27. Which Customers Need a Win-Back Campaign?

*easy* · Dialects: PostgreSQL

You are a product analyst at a B2B marketplace. The CRM team is preparing a win-back campaign and needs to know how many days have passed since each active buyer's most recent genuinely paid purchase as of **July 1, 2026**. Cancelled, refunded, unfinished orders and records without a payment timestamp must not affect the metric. Customers with no qualifying order must be excluded.

**Return columns:**
- `customer_id` — customer identifier, integer
- `customer_name` — customer name
- `last_paid_date` — date of the latest paid order in `YYYY-MM-DD` format
- `recency_days` — calendar days from `last_paid_date` to `2026-07-01`, integer

**Rules:**
- Use only orders with status `paid` and a non-NULL `paid_at`.
- Ignore orders after `2026-07-01`.
- If a customer has several payments on the same latest date, return one customer row.
- Sort by `recency_days` ascending, then `customer_id` ascending.
- No rounding is needed; the result must contain no `NULL` values.

**Tables:**

- **customers**: `customer_id` integer 🔑 — Customer identifier; `customer_name` varchar(100) — Customer name; `segment` varchar(30) — Customer business segment
- **orders**: `order_id` integer 🔑 — Order identifier; `customer_id` integer — Customer identifier; `status` varchar(20) — Order status; `paid_at` timestamp — Order payment timestamp; `total_amount` numeric(10,2) — Order total amount

**Expected columns:** `customer_id`, `customer_name`, `last_paid_date`, `recency_days`

**Expected output (first rows):**

| customer_id | customer_name | last_paid_date | recency_days |
|---|---|---|---|
| 4 | Delta Foods | 2026-06-30 | 1 |
| 8 | Harbor Tools | 2026-06-30 | 1 |
| 1 | Acorn Labs | 2026-06-28 | 3 |
| 11 | Kite Travel | 2026-06-28 | 3 |
| 2 | Bright Cart | 2026-06-15 | 16 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/rfm-client-recency-as-of-date?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 28. From KYC Submission to Approval

*easy* · Dialects: PostgreSQL

You are the product analyst at a fintech startup that opens digital accounts for small businesses. The acquisition team wants to know which signup channels bring customers who actually complete identity verification, not just registrations. Build one report row for every signup channel.

A customer starts the funnel when they have at least one `application_submitted` event with a non-null timestamp. Their start time is the earliest such timestamp. A customer is approved when they have at least one non-null `application_approved` event at or after that start time. An approval recorded before the first submission does not count. Repeated events from the same customer must not inflate any count.

Include every channel present in `kyc_customers`, even when nobody in that channel started an application. Display a `NULL` `signup_channel` as `unknown`.

**Return columns:**
- `channel` — signup channel, text.
- `total_customers` — registered customers in the channel, integer.
- `started_customers` — customers who submitted an application, integer.
- `approved_customers` — started customers who were later approved, integer.
- `conversion_rate_pct` — approved customers as a percentage of started customers, `numeric`, rounded to 2 decimal places. Return `0.00` when there are no started customers.

Sort by `channel` ascending. Ignore events whose `event_time` is `NULL`. An approval at exactly the submission timestamp counts.

**Tables:**

- **kyc_customers**: `customer_id` integer 🔑 — Customer identifier; `signup_channel` text — Customer signup channel; `registered_at` timestamp — Registration timestamp
- **kyc_events**: `event_id` integer 🔑 — Event identifier; `customer_id` integer — Customer identifier; `event_name` text — Verification event type; `event_time` timestamp — Event timestamp

**Expected columns:** `channel`, `total_customers`, `started_customers`, `approved_customers`, `conversion_rate_pct`

**Expected output (first rows):**

| channel | total_customers | started_customers | approved_customers | conversion_rate_pct |
|---|---|---|---|---|
| offline | 2 | 1 | 0 | 0.00 |
| organic | 2 | 2 | 2 | 100.00 |
| paid_search | 2 | 2 | 1 | 50.00 |
| partner | 2 | 1 | 1 | 100.00 |
| referral | 2 | 1 | 1 | 100.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/fun-kyc-submit-to-approval?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 29. Most Read Books Lookup

*easy* · Dialects: PostgreSQL, ClickHouse

In a library system, there are tables for books and book loans to readers. Find all books that have been borrowed more than 2 times, and sort them by number of loans in descending order. Display book title, author, and loan count.

**Tables:**

- **books**: `id` serial 🔑; `title` varchar(100); `author` varchar(100); `isbn` varchar(20)
- **loans**: `id` serial 🔑; `book_id` integer → books.id; `reader_name` varchar(100); `loan_date` date; `return_date` date

**Expected columns:** `title`, `author`, `loan_count`

**Expected output (first rows):**

| title | author | loan_count |
|---|---|---|
| War and Peace | Leo Tolstoy | 4 |
| Crime and Punishment | Fyodor Dostoevsky | 3 |
| The Master and Margarita | Michael Bulgakov | 3 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1775636066836-hemq?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 30. Kotomarket monthly orders report

*medium* · Dialects: PostgreSQL

In the cats-only online store Kotomarket every purchase lands in a single `orders` table — each order has an `id`, an `order_date`, and an `amount`.

Marketing asked for a **monthly report**: for every month that has at least one order, count **how many orders** were placed and **the total amount** spent.

Write a query that returns one row per month with orders, with columns:

- `month` — the month as text in `'YYYY-MM'` format (e.g. `'2024-01'`);
- `orders_count` — the number of orders that month;
- `total_amount` — the total order amount for the month.

Sort the result by month in chronological order (earliest first).

Hint: collapse the date to the first day of the month with `DATE_TRUNC('month', order_date)` — group and order by that expression, and produce the `'YYYY-MM'` text label with `TO_CHAR` only for display. No window functions, CTEs, or JOINs — everything is computed from one table.

**Tables:**

- **orders**: `id` int 🔑; `order_date` date; `amount` numeric(10,2)

**Expected columns:** `month`, `orders_count`, `total_amount`

**Expected output (first rows):**

| month | orders_count | total_amount |
|---|---|---|
| 2024-01 | 3 | 3840.50 |
| 2024-02 | 2 | 2299.99 |
| 2024-03 | 4 | 3750.75 |
| 2024-04 | 2 | 2650.00 |
| 2024-06 | 1 | 1750.25 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/gen-g6l5-monthly-orders-report?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 31. Top 3 categories by revenue

*medium* · Dialects: PostgreSQL, ClickHouse

Calculate total revenue per product category. Show only top 3. Output: category, total_revenue. Sort the result by `total_revenue` (descending).

**Tables:**

- **products**: `id` int 🔑; `name` varchar; `category` varchar; `price` decimal
- **order_items**: `id` int 🔑; `product_id` int → products.id; `quantity` int; `price` decimal

**Expected columns:** `category`, `total_revenue`

**Expected output (first rows):**

| category | total_revenue |
|---|---|
| Electronics | 9082.00 |
| Furniture | 2167.00 |
| Books | 770.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1777187603534-aok0?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 32. Average Salary of Employees by Departments for 2023

*medium* · Dialects: PostgreSQL, ClickHouse

HR analytics compares salaries across departments among employees hired in 2023. Find the average salary for each department, counting only employees whose hire date (`hire_date`) falls in 2023. Include only departments where the average salary exceeds `60000`. The `attendance` table is not needed for this task.

**Tables:**

- **departments**: `id` serial 🔑; `name` varchar(100)
- **employees**: `id` serial 🔑; `name` varchar(100); `department_id` integer → departments.id; `hire_date` date; `salary` decimal(10, 2)
- **attendance**: `id` serial 🔑; `employee_id` integer → employees.id; `attendance_date` date

**Expected columns:** `department_name`, `average_salary`

**Expected output (first rows):**

| department_name | average_salary |
|---|---|
| Finance | 66000.000000000000 |
| IT | 76666.666666666667 |
| Sales | 70000.000000000000 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1777187735180-c7kf?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 33. Book Sales Split by Genre

*medium* · Dialects: PostgreSQL, ClickHouse

A bookstore database contains information about books, authors, genres, and sales. Find genres that generated revenue of more than 10,000 rubles, and for each such genre show: genre name, total number of books sold in this genre, total revenue from sales, and average book price in the genre — the average book price over all of the genre's sales rows, rounded to `2` decimal places. Sort results by total revenue in descending order.

**Tables:**

- **authors**: `author_id` serial 🔑; `name` varchar(100); `country` varchar(50)
- **genres**: `genre_id` serial 🔑; `genre_name` varchar(50)
- **books**: `book_id` serial 🔑; `title` varchar(200); `author_id` integer → authors.author_id; `genre_id` integer → genres.genre_id; `price` decimal(10,2)
- **sales**: `sale_id` serial 🔑; `book_id` integer → books.book_id; `quantity` integer; `sale_date` date

**Expected columns:** `genre_name`, `total_books_sold`, `total_revenue`, `average_price`

**Expected output (first rows):**

| genre_name | total_books_sold | total_revenue | average_price |
|---|---|---|---|
| Detective | 112 | 44858.88 | 405.99 |
| Fantasy | 75 | 40309.25 | 536.66 |
| Classic Literature | 35 | 29699.65 | 849.99 |
| Sci-Fi | 42 | 17639.58 | 424.99 |
| Horror | 18 | 11799.82 | 649.99 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1775635279697-f1bp?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 34. Analysis of courier performance by delivered packages

*medium* · Dialects: PostgreSQL

In a delivery service, you need to find couriers who delivered packages with a total amount exceeding 50,000 rubles. For each courier, display their name, the count of delivered packages, the total cost of deliveries, and the average cost per package. Sort results by total cost in descending order.

**Tables:**

- **couriers**: `courier_id` serial 🔑; `courier_name` varchar(100)
- **packages**: `package_id` serial 🔑; `courier_id` integer → couriers.courier_id; `package_weight` decimal(8,2); `delivery_cost` decimal(10,2)
- **deliveries**: `delivery_id` serial 🔑; `package_id` integer → packages.package_id; `delivery_date` date; `status` varchar(50)

**Expected columns:** `courier_name`, `packages_count`, `total_cost`, `avg_cost`

**Expected output (first rows):**

| courier_name | packages_count | total_cost | avg_cost |
|---|---|---|---|
| Ivan Petrov | 3 | 55000.00 | 18333.333333333333 |
| Elena Sokolov | 2 | 53000.00 | 26500.000000000000 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1781871231464-fsst?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 35. Client Buying Behavior Study

*medium* · Dialects: PostgreSQL, ClickHouse

Purchasing-behaviour analytics is looking for customers who have already made a noticeable volume of purchases. For each customer, compute the total amount of their purchases and keep only those whose total is greater than 500 units. Return the customer names and the total purchase amount. Use a join of the tables, grouping and filtering on the resulting total.

**Tables:**

- **customers**: `id` serial 🔑; `name` varchar(100)
- **purchases**: `id` serial 🔑; `customer_id` integer → customers.id; `amount` decimal(10, 2); `purchase_date` timestamp
- **products**: `id` serial 🔑; `name` varchar(100); `price` decimal(10, 2)

**Expected columns:** `name`, `total_amount`

**Expected output (first rows):**

| name | total_amount |
|---|---|
| Maria Peterson | 650.00 |
| Alex Brown | 700.00 |
| Ivan Johnson | 550.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1775670901436-66td?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 36. Sales Split by Product Category

*medium* · Dialects: PostgreSQL, ClickHouse

Find product categories where total sales amount exceeds 50000 rubles, and for each such category show the category name, total sales amount, and count of unique products that were sold. Sort the result by total sales amount in descending order.

**Tables:**

- **categories**: `category_id` serial 🔑; `category_name` varchar(100)
- **products**: `product_id` serial 🔑; `product_name` varchar(100); `category_id` integer → categories.category_id; `price` decimal(10,2)
- **sales**: `sale_id` serial 🔑; `product_id` integer → products.product_id; `quantity` integer; `sale_date` date
- **customers**: `customer_id` serial 🔑; `customer_name` varchar(100); `city` varchar(50)

**Expected columns:** `category_name`, `total_sales`, `unique_products_count`

**Expected output (first rows):**

| category_name | total_sales | unique_products_count |
|---|---|---|
| Electronics | 488000.00 | 3 |
| Sports | 126000.00 | 2 |
| Home & Garden | 125000.00 | 2 |
| Clothing | 84000.00 | 2 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1775641700820-h25c?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 37. Box Office Revenue by Popular Genres

*medium* · Dialects: PostgreSQL

A cinema chain is analyzing profitability by genre. Find genres where ticket sales exceeded 5000 rubles, showing for each genre the total revenue, number of tickets sold, and average ticket price. Sort results by revenue in descending order. Round `avg_price` to 2 decimal places.

**Tables:**

- **genres**: `genre_id` serial 🔑; `genre_name` varchar(100)
- **films**: `film_id` serial 🔑; `title` varchar(255); `genre_id` integer → genres.genre_id
- **showtimes**: `showtime_id` serial 🔑; `film_id` integer → films.film_id; `show_date` date
- **tickets**: `ticket_id` serial 🔑; `showtime_id` integer → showtimes.showtime_id; `price` decimal(7,2)

**Expected columns:** `genre_name`, `total_revenue`, `tickets_sold`, `avg_price`

**Expected output (first rows):**

| genre_name | total_revenue | tickets_sold | avg_price |
|---|---|---|---|
| Action | 7420.00 | 15 | 494.67 |
| Drama | 5150.00 | 12 | 429.17 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1784269947391-uk7v?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 38. Most prolific authors with high ratings

*medium* · Dialects: PostgreSQL

The library system needs to find authors who have written at least 3 books and whose works have an average rating above 4.0 stars. Output the author's name, the count of their books, and the average rating of their works, sorted in descending order by average rating. Consider only books published in 2015 or later.

**Tables:**

- **authors**: `author_id` serial 🔑; `name` varchar(100)
- **books**: `book_id` serial 🔑; `title` varchar(150); `author_id` integer → authors.author_id; `publication_year` integer
- **reviews**: `review_id` serial 🔑; `book_id` integer → books.book_id; `rating` decimal(3,1)

**Expected columns:** `name`, `book_count`, `avg_rating`

**Expected output (first rows):**

| name | book_count | avg_rating |
|---|---|---|
| George Orwell | 4 | 4.7500000000000000 |
| Virginia Woolf | 6 | 4.5166666666666667 |
| Leo Tolstoy | 5 | 4.5000000000000000 |
| Jane Austen | 6 | 4.2833333333333333 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1783004573963-aiwb?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**
