# CTEs (WITH clause)

[← All topics](../README.md)

## 66. Top Bank Clients by Transaction Amount

*hard* · Dialects: PostgreSQL

A bank ranks active clients by their transaction total over the last 12 months. Find clients whose total transaction amount across their accounts in that period (`SUM(transactions.amount)`) exceeds `10000`. For each, output `client_id`, the client name (`client_name`), the total amount (`total_amount`) and an activity category (`activity_category`): `high` if the total is over `20000`, otherwise `medium`. Sort by total descending, breaking ties by `client_id`.

**Tables:**

- **clients**: `id` serial 🔑; `name` varchar(100); `registration_date` date
- **accounts**: `id` serial 🔑; `client_id` integer → clients.id; `balance` decimal(15,2)
- **transactions**: `id` serial 🔑; `account_id` integer → accounts.id; `transaction_date` timestamp; `amount` decimal(15,2); `transaction_type` varchar(50)

**Expected columns:** `client_id`, `client_name`, `total_amount`, `activity_category`

**Expected output (first rows):**

| client_id | client_name | total_amount | activity_category |
|---|---|---|---|
| 2 | Светлана Петрова | 27000.00 | high |
| 5 | Николай Сидоров | 27000.00 | high |
| 1 | Иван Иванов | 13000.00 | medium |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1777242925149-2xrk?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 67. Quarterly Performance of Sales Managers

*hard* · Dialects: PostgreSQL

Company management is preparing a quarterly performance report for managers in the `Sales` department (`departments.name = 'Sales'`). Consider only employees of that department: for each manager and each quarter (by `EXTRACT(QUARTER FROM sales.sale_date)`) compute the total amount of their sales for the quarter (`SUM(sales.amount)`) and keep only managers whose quarterly total is greater than `50000`. These qualified `Sales` managers form the result set, and every calculation is performed within it. For each row, output: the manager name (`first_name || ' ' || last_name`), the quarter, their quarterly sales amount, the percentage `percentage_of_total` — the share of the manager's quarterly amount relative to the combined sales of all qualified `Sales` managers in that same quarter (i.e. relative to the total of the selected set, NOT relative to all company sales), rounded to 2 decimals, the manager's rank in the quarterly leaderboard by sales volume (`RANK()` partitioned by quarter and ordered by amount descending, where `1` is the best result), and the sales amount of the top manager in that same quarter (`top_manager_sales`). Sort the result by quarter, then by the manager's rank.

**Tables:**

- **departments**: `id` serial 🔑; `name` varchar(100)
- **employees**: `id` serial 🔑; `first_name` varchar(50); `last_name` varchar(50); `department_id` integer → departments.id; `hire_date` date
- **customers**: `id` serial 🔑; `company_name` varchar(100); `contact_person` varchar(100); `registration_date` date
- **sales**: `id` serial 🔑; `employee_id` integer → employees.id; `customer_id` integer → customers.id; `sale_date` date; `amount` decimal(10,2)

**Expected columns:** `manager_name`, `quarter`, `quarterly_amount`, `percentage_of_total`, `manager_rank`, `top_manager_sales`

**Expected output (first rows):**

| manager_name | quarter | quarterly_amount | percentage_of_total | manager_rank | top_manager_sales |
|---|---|---|---|---|---|
| Michael Smith | 1 | 131000.00 | 43.23 | 1 | 131000.00 |
| Anna Peterson | 1 | 120000.00 | 39.60 | 2 | 131000.00 |
| Daniel Wolf | 1 | 52000.00 | 17.16 | 3 | 131000.00 |
| Anna Peterson | 2 | 120000.00 | 34.19 | 1 | 120000.00 |
| Michael Smith | 2 | 84000.00 | 23.93 | 2 | 120000.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1775635598933-m421?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 68. Top Couriers by Deliveries with Urgency Priority

*hard* · Dialects: PostgreSQL

The logistics team is reviewing courier performance and wants the couriers who handled both urgent and regular deliveries. Count only deliveries with `delivery_time` on or after `2024-12-01`, and only couriers with more than one such delivery. First assign each of those couriers a place by delivery count: the largest count takes first place, and tied couriers share a place while the next place is skipped (1, 1, 3). Places are computed across ALL couriers with more than one delivery, even those that will not appear in the final list. Then keep only the couriers who have at least one urgent (`is_urgent = true`) and at least one regular delivery — their places are not recomputed. Output five columns: `courier_name` — the courier's name, `total_deliveries` — their delivery count, `urgent_deliveries` — how many of those were urgent, `urgent_percentage` — the share of urgent ones in percent rounded to one decimal place, and `delivery_rank` — that place. Sort the result by place.

**Tables:**

- **regions**: `region_id` serial 🔑; `region_name` varchar(100); `region_code` varchar(10)
- **warehouses**: `warehouse_id` serial 🔑; `warehouse_name` varchar(100); `region_id` integer → regions.region_id; `address` varchar(200)
- **customers**: `customer_id` serial 🔑; `customer_name` varchar(100); `phone` varchar(20); `email` varchar(100); `region_id` integer → regions.region_id
- **couriers**: `courier_id` serial 🔑; `courier_name` varchar(100); `phone` varchar(20); `hire_date` date; `region_id` integer → regions.region_id
- **vehicles**: `vehicle_id` serial 🔑; `courier_id` integer → couriers.courier_id; `vehicle_type` varchar(50); `license_plate` varchar(20)
- **package_types**: `type_id` serial 🔑; `type_name` varchar(50); `base_cost` decimal(8,2)
- **orders**: `order_id` serial 🔑; `customer_id` integer → customers.customer_id; `warehouse_id` integer → warehouses.warehouse_id; `order_date` timestamp; `is_urgent` boolean; `total_amount` decimal(10,2)
- **packages**: `package_id` serial 🔑; `order_id` integer → orders.order_id; `type_id` integer → package_types.type_id; `weight` decimal(6,2); `dimensions` varchar(50)
- **deliveries**: `delivery_id` serial 🔑; `order_id` integer → orders.order_id; `courier_id` integer → couriers.courier_id; `pickup_time` timestamp; `delivery_time` timestamp; `status` varchar(20)
- **delivery_routes**: `route_id` serial 🔑; `courier_id` integer → couriers.courier_id; `route_date` date; `total_distance` decimal(8,2)

**Expected columns:** `courier_name`, `total_deliveries`, `urgent_deliveries`, `urgent_percentage`, `delivery_rank`

**Expected output (first rows):**

| courier_name | total_deliveries | urgent_deliveries | urgent_percentage | delivery_rank |
|---|---|---|---|---|
| Олег Кузнецов | 2 | 1 | 50.0 | 1 |
| Сергей Николаев | 2 | 1 | 50.0 | 1 |
| Игорь Сидоров | 2 | 1 | 50.0 | 1 |
| Александр Петров | 2 | 1 | 50.0 | 1 |
| Максим Федоров | 2 | 1 | 50.0 | 1 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1777263423404-9c2a?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 69. Employee Earnings Breakdown

*hard* · Dialects: PostgreSQL

Using `employees` / `departments` / `bonuses` / `sales` / `deductions`, compute each employee's total income as `salary + SUM(bonus) + SUM(sales.amount) - SUM(deductions.amount)`. For each department return the top-3 employees by total income. Columns: `department_name`, `employee_name`, `total_revenue`. Sort by `department_name`, then `total_revenue` descending.

**Tables:**

- **departments**: `id` serial 🔑; `name` varchar(100)
- **employees**: `id` serial 🔑; `name` varchar(100); `department_id` integer → departments.id; `salary` decimal(10, 2)
- **bonuses**: `id` serial 🔑; `employee_id` integer → employees.id; `bonus` decimal(10, 2); `date` date
- **sales**: `id` serial 🔑; `employee_id` integer → employees.id; `amount` decimal(10, 2); `sale_date` date
- **deductions**: `id` serial 🔑; `employee_id` integer → employees.id; `amount` decimal(10, 2); `date` date

**Expected columns:** `department_name`, `employee_name`, `total_revenue`

**Expected output (first rows):**

| department_name | employee_name | total_revenue |
|---|---|---|
| Finance | Heidi | 70000.00 |
| Finance | Grace | 65000.00 |
| Finance | Frank | 60000.00 |
| HR | Dave | 61500.00 |
| HR | Eve | 51000.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1775671119763-2ukv?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 70. Monthly Top Tracks in Playlists

*hard* · Dialects: PostgreSQL

The music team is reviewing recent additions to playlists and wants to know which of them have the most plays of all time. Take the tracks that were added to playlists during the last month (that is, `playlist_tracks.added_at >= NOW() - INTERVAL '1 month'`), and for each such track count the total number of its plays from the `track_plays` table over its entire history (not just plays within the last month). For each track output its title (`tracks.title`), the artist name (`artists.name` as `artist_name`), and the total number of plays (`play_count`). Sort the result by `play_count` in descending order and keep the top 10 tracks.

**Tables:**

- **tracks**: `id` serial 🔑; `title` varchar(100); `artist_id` integer → artists.id; `duration` integer
- **artists**: `id` serial 🔑; `name` varchar(100)
- **playlists**: `id` serial 🔑; `name` varchar(100); `created_at` timestamp
- **playlist_tracks**: `playlist_id` integer → playlists.id; `track_id` integer → tracks.id; `added_at` timestamp
- **track_plays**: `track_id` integer → tracks.id; `play_date` timestamp

**Expected columns:** `title`, `artist_name`, `play_count`

**Expected output (first rows):**

| title | artist_name | play_count |
|---|---|---|
| Track 1 | Artist 1 | 3 |
| Track 2 | Artist 2 | 3 |
| Track 3 | Artist 3 | 1 |
| Track 4 | Artist 1 | 1 |
| Track 5 | Artist 2 | 1 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1775675622104-qs7d?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 71. Most-Played Artists Across Playlists

*hard* · Dialects: PostgreSQL

A music service measures which artists are heard most in playlists. Each playlist play (`plays`) counts for every artist whose tracks are in that playlist. Consider only playlists created more than 30 days ago (`playlists.created_at`) and plays from the last month (`plays.play_date`). Find the top 5 artists by the number of such plays: output the artist name (`name`) and the play count (`total_plays`), ordered descending, breaking ties by name.

**Tables:**

- **artists**: `id` serial 🔑; `name` varchar(100)
- **tracks**: `id` serial 🔑; `artist_id` integer → artists.id; `title` varchar(100)
- **playlists**: `id` serial 🔑; `name` varchar(100); `created_at` timestamp
- **playlist_tracks**: `playlist_id` integer → playlists.id; `track_id` integer → tracks.id
- **plays**: `playlist_id` integer → playlists.id; `play_date` timestamp

**Expected columns:** `name`, `total_plays`

**Expected output (first rows):**

| name | total_plays |
|---|---|
| Artist A | 2 |
| Artist C | 2 |
| Artist D | 2 |
| Artist B | 1 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1775675459674-b6li?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 72. Student Performance Ranking by Department with Grade Dynamics

*hard* · Dialects: PostgreSQL

A university needs to identify top-performing students in each department who improved their grades in the latest semester. Find students whose average grade in the current semester exceeds their previous semester average, and determine for each student: their name, department, average grade in the current semester, grade improvement (difference), and their ranking within their department by improvement magnitude (from largest to smallest improvement). Include only students whose improvement is at least 0.5 points, sorted by department, then by ranking within the department.

**Tables:**

- **departments**: `dept_id` serial 🔑; `dept_name` varchar(100)
- **students**: `student_id` serial 🔑; `student_name` varchar(100); `dept_id` integer → departments.dept_id
- **semesters**: `semester_id` serial 🔑; `semester_name` varchar(50); `year` integer
- **grades**: `grade_id` serial 🔑; `student_id` integer → students.student_id; `semester_id` integer → semesters.semester_id; `grade_value` decimal(3, 2)

**Expected columns:** `student_name`, `dept_name`, `current_avg`, `improvement`, `dept_rank`

**Expected output (first rows):**

| student_name | dept_name | current_avg | improvement | dept_rank |
|---|---|---|---|---|
| Alice Johnson | Computer Science | 4.10 | 0.60 | 1 |
| Charlie Brown | Mathematics | 4.20 | 0.60 | 1 |
| Eve Wilson | Physics | 4.10 | 0.80 | 1 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1788857992408-sa5x?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 73. Revenue Month-on-Month Growth

*hard* · Dialects: PostgreSQL

The finance team tracks revenue dynamics by month. For each month, calculate the monthly revenue, the previous month's revenue and the growth percentage relative to the previous month. Output `month`, `revenue`, `prev_revenue` and `growth_pct`, rounding `growth_pct` to 2 decimal places.

**Tables:**

- **transactions**: `id` int 🔑; `amount` decimal; `created_at` date

**Expected columns:** `month`, `revenue`, `prev_revenue`, `growth_pct`

**Expected output (first rows):**

| month | revenue | prev_revenue | growth_pct |
|---|---|---|---|
| 2024-01-01 | 450.00 | NULL | NULL |
| 2024-02-01 | 550.00 | 450.00 | 22.22 |
| 2024-03-01 | 700.00 | 550.00 | 27.27 |
| 2024-04-01 | 850.00 | 700.00 | 21.43 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1775673452252-fuqx?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**
