# Window functions

[← All topics](../README.md)

## 74. Gaps between plays

*easy* · Dialects: PostgreSQL

You are a product analyst at the music streaming service TuneWave. The recommendations team wants to know how densely listeners consume tracks: short pauses mean continuous playlist listening, long ones mean the person re-opened the app. You have the track-start log play_events: who pressed Play and when.

For every event, compute how many minutes passed since the previous event of the same user. Skip the very first event of each user — there is nothing to compare it with.

Return columns:
- `user_id` — listener identifier;
- `played_at` — track start time (timestamp, as stored);
- `minutes_since_prev` — whole number of minutes since the user's previous event (all gaps in the data are exact minutes).

Sort by user_id ascending, then played_at ascending. Users with a single event do not appear in the output. Timestamps never repeat within one user.

**Tables:**

- **play_events**: `event_id` integer 🔑 — Unique event id; `user_id` integer — Listener id; `played_at` timestamp — Track start time

**Expected columns:** `user_id`, `played_at`, `minutes_since_prev`

**Expected output (first rows):**

| user_id | played_at | minutes_since_prev |
|---|---|---|
| 1 | 2026-05-01 09:03:00 | 3 |
| 1 | 2026-05-01 09:10:00 | 7 |
| 1 | 2026-05-01 10:00:00 | 50 |
| 2 | 2026-05-01 12:45:00 | 45 |
| 2 | 2026-05-01 12:50:00 | 5 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ses-stream-play-gaps?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 75. Session-start flag in an online store

*easy* · Dialects: PostgreSQL

You are an analyst at the online hypermarket FreshCart. Marketing is preparing per-session conversion metrics, and step one is to label the page-view stream: where one customer visit ends and the next begins. The agreed rule: if STRICTLY more than 30 minutes passed since the same customer's previous view, a new session starts; exactly 30 minutes still belongs to the same session. A customer's very first view always opens a new session.

Label every view in page_views with this flag.

Return columns:
- `customer_id` — customer identifier;
- `viewed_at` — view time (timestamp, as stored);
- `is_new_session` — boolean: true if this view starts a new session, false otherwise.

Sort by customer_id ascending, then viewed_at ascending. ALL views are included, first ones too. Timestamps never repeat within one customer.

**Tables:**

- **page_views**: `view_id` integer 🔑 — Unique view id; `customer_id` integer — Customer id; `viewed_at` timestamp — Page view time

**Expected columns:** `customer_id`, `viewed_at`, `is_new_session`

**Expected output (first rows):**

| customer_id | viewed_at | is_new_session |
|---|---|---|
| 1 | 2026-05-03 09:00:00 | True |
| 1 | 2026-05-03 09:10:00 | False |
| 1 | 2026-05-03 09:41:00 | True |
| 1 | 2026-05-03 09:50:00 | False |
| 2 | 2026-05-03 12:00:00 | True |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ses-shop-session-flag?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 76. Neobank Operating Balance

*easy* · Dialects: PostgreSQL

You are a treasury analyst at a mobile neobank. The finance team is reviewing how the operating cash position changed during a control period. `ledger_entries` stores individual credits and debits, while `report_days` defines every date that must appear in the report. Management needs both each day's net movement and the balance accumulated since the start of the period.

For every date in `report_days`, calculate the net movement: a `credit` increases the amount and a `debit` decreases it. Ignore entries outside the reporting calendar. The balance immediately before the first report date is `0.00`.

**Return these columns:**
- `report_date` — reporting date in `YYYY-MM-DD` format;
- `daily_net_usd` — net movement for the date in USD, numeric with 2 decimal places;
- `running_balance_usd` — cumulative balance from the first report date through the current date, inclusive, numeric with 2 decimal places.

Return exactly one row for every date in `report_days`. Sort by `report_date` ascending. A `NULL` `amount_usd` contributes nothing; when a date has no entry with a known amount, `daily_net_usd` must be `0.00`. Count every separate entry on the same date even when amounts are equal; the final output must contain no duplicate dates.

**Tables:**

- **report_days**: `report_date` date 🔑 — Date required in the report
- **ledger_entries**: `entry_id` bigint 🔑 — Ledger entry identifier; `posted_date` date — Posting date; `entry_type` varchar(10) — Entry type: credit or debit; `amount_usd` numeric(10, 2) — entry amount, USD

**Expected columns:** `report_date`, `daily_net_usd`, `running_balance_usd`

**Expected output (first rows):**

| report_date | daily_net_usd | running_balance_usd |
|---|---|---|
| 2026-04-01 | 1120.00 | 1120.00 |
| 2026-04-02 | -91.00 | 1029.00 |
| 2026-04-03 | 300.00 | 1329.00 |
| 2026-04-04 | -75.00 | 1254.00 |
| 2026-04-05 | -210.00 | 1044.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/wfr-neobank-running-balance?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 77. Each Product's Share of Total Revenue via SUM() OVER ()

*medium* · Dialects: PostgreSQL

In the "Kotomarket" store an analyst wants to see each product's revenue next to the **grand total** and its **percentage share** — without collapsing rows into one (as `GROUP BY` would). Every row of `sales` must stay in place.

The `sales` table holds individual product sales (one row = one sale).

Write a query that, for **each** sale, returns:

- `product` — product name;
- `revenue` — revenue of this sale;
- `total_revenue` — total revenue over all sales (the same number in every row);
- `pct_of_total` — this sale's share of total revenue in percent, rounded to 2 decimals: `revenue * 100.0 / total_revenue`.

Hint: this is the classic "window vs `GROUP BY`" contrast. The grand total is needed in **every** row without aggregating the set — use the window aggregate `SUM(revenue) OVER ()` (empty parentheses, no `PARTITION BY`, no `ORDER BY`).

Sort the result by `revenue` descending, ties broken by `product` ascending.

**Tables:**

- **sales**: `sale_id` integer 🔑; `product` text; `category` text; `revenue` numeric(10,2)

**Expected columns:** `product`, `revenue`, `total_revenue`, `pct_of_total`

**Expected output (first rows):**

| product | revenue | total_revenue | pct_of_total |
|---|---|---|---|
| Когтеточка Башня | 12000.00 | 40000.00 | 30.00 |
| Корм Премиум 5кг | 8000.00 | 40000.00 | 20.00 |
| Лежанка Облако | 6000.00 | 40000.00 | 15.00 |
| Туннель Радуга | 5000.00 | 40000.00 | 12.50 |
| Корм Диета 2кг | 4000.00 | 40000.00 | 10.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/gen-m7l1-window-share-of-total?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 78. Staff Salaries: How Far From the Average

*medium* · Dialects: PostgreSQL

At "Kotomarket" the HR team analyzes the shop employees' salaries. The `staff` table holds employees: `id`, `full_name`, `position`, `salary` (in rubles).

For **every** employee you need to see their salary next to the average salary **across the whole staff**, and how far their pay deviates from that average.

Output one row per employee with columns:

- `full_name` — name;
- `position` — job title;
- `salary` — the employee's salary;
- `avg_salary` — the average salary over the **entire** table, rounded to 2 decimals (`ROUND(..., 2)`); this value must be **the same in every row**;
- `diff_from_avg` — the difference `salary - avg_salary`, also rounded to 2 decimals (positive if the employee earns above average, negative if below).

Important: the rows must **not collapse** — the result has as many rows as there are employees. Compute the average with the window aggregate `AVG(salary) OVER ()` — **without** `PARTITION BY` and **without** `GROUP BY`.

Sort the result by `salary` descending, breaking ties by `id` ascending.

**Tables:**

- **staff**: `id` integer 🔑; `full_name` text; `position` text; `salary` numeric(10,2)

**Expected columns:** `full_name`, `position`, `salary`, `avg_salary`, `diff_from_avg`

**Expected output (first rows):**

| full_name | position | salary | avg_salary | diff_from_avg |
|---|---|---|---|---|
| Дарья Пушистова | менеджер | 92000.00 | 57000.00 | 35000.00 |
| Игорь Лапкин | продавец | 61000.00 | 57000.00 | 4000.00 |
| Анна Котова | продавец | 58000.00 | 57000.00 | 1000.00 |
| Светлана Барсикова | продавец | 57000.00 | 57000.00 | 0.00 |
| Павел Когтев | кладовщик | 52000.00 | 57000.00 | -5000.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/gen-m7l1b-staff-salary-vs-average?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 79. Student Rating by Average Grade with Group Position

*medium* · Dialects: PostgreSQL, ClickHouse

The academic office wants to rank the strongest students within each major. For every student compute the average grade as `ROUND(AVG(grades.grade_value), 2)` (column `avg_grade`) and keep only those whose average grade is strictly greater than `3.5`. Within each major (`majors.major_id`) assign every student a unique sequential number `rank_in_major`: use the `ROW_NUMBER()` window function with `PARTITION BY majors.major_id`, ordering students by their average grade in descending order. This must be a continuous numbering (1, 2, 3, ...), not a shared rank: students with equal average grades still receive distinct consecutive numbers. To make the result deterministic when average grades tie, add a tie-break by `students.student_id` ascending in the window's `ORDER BY`. Output the columns `student_id`, `student_name`, `major_name`, `avg_grade`, `rank_in_major` and sort the final result by `major_name`, and within each major by `avg_grade` in descending order.

**Tables:**

- **majors**: `major_id` serial 🔑; `major_name` varchar(100)
- **students**: `student_id` serial 🔑; `student_name` varchar(100); `major_id` integer → majors.major_id
- **courses**: `course_id` serial 🔑; `course_name` varchar(100)
- **grades**: `grade_id` serial 🔑; `student_id` integer → students.student_id; `course_id` integer → courses.course_id; `grade_value` decimal(3,2)

**Expected columns:** `student_id`, `student_name`, `major_name`, `avg_grade`, `rank_in_major`

**Expected output (first rows):**

| student_id | student_name | major_name | avg_grade | rank_in_major |
|---|---|---|---|---|
| 1 | Alice Johnson | Computer Science | 4.25 | 1 |
| 2 | Bob Smith | Computer Science | 3.65 | 2 |
| 3 | Carol White | Mathematics | 4.05 | 1 |
| 5 | Elena Petrova | Physics | 4.05 | 1 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1778004364778-0tho?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 80. Crop Variety Yield Rankings by Plot

*medium* · Dialects: PostgreSQL

An agricultural company wants to analyze the effectiveness of different crop varieties. Find all crop varieties that are grown on multiple plots (at least 2) and return for each variety the total sowing area, average harvest across all plots of that variety, total number of plots, and the rank of each variety by average yield (harvest per unit area in kilograms per hectare). Sort results by average yield per hectare in descending order, then by variety name alphabetically.

**Tables:**

- **crop_varieties**: `variety_id` serial 🔑; `variety_name` varchar(100); `crop_type` varchar(50)
- **farm_plots**: `plot_id` serial 🔑; `plot_name` varchar(100); `area_hectares` decimal(10,2); `variety_id` integer → crop_varieties.variety_id
- **harvest_records**: `record_id` serial 🔑; `plot_id` integer → farm_plots.plot_id; `harvest_year` integer; `harvest_kg` decimal(12,2)
- **weather_data**: `weather_id` serial 🔑; `plot_id` integer → farm_plots.plot_id; `weather_year` integer; `rainfall_mm` decimal(8,2)

**Expected columns:** `variety_name`, `total_area_hectares`, `avg_harvest_kg`, `plot_count`, `yield_rank`

**Expected output (first rows):**

| variety_name | total_area_hectares | avg_harvest_kg | plot_count | yield_rank |
|---|---|---|---|---|
| Amber Barley | 33.20 | 2952.3333333333333333 | 3 | 1 |
| Golden Wheat | 46.55 | 3103.6666666666666667 | 3 | 2 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1786790300439-tv0i?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 81. Genre Champions Among Library Readers

*hard* · Dialects: PostgreSQL

A library network wants to analyze reader activity by book genre to find the most notable visitors in each direction.

Only loans that have already been completed with a return (return date is filled in) should be considered. For each genre, compute the total number of pages loaned to each reader (the sum of page_count for every book they borrowed in that genre).

Within each genre, rank readers by this total in descending order, using standard ranking where ties share the same rank and the next rank is not skipped (dense ranking behavior with ties keeping the same place, and the rank after ties continuing consecutively). Keep only the readers who ended up in first place within their genre, and output the genre, the reader's name (reader_name), and the total number of pages (total_pages). Sort the result alphabetically by genre, and for rows with the same genre, by total_pages descending.

**Tables:**

- **authors**: `author_id` serial 🔑; `full_name` varchar(100)
- **genres**: `genre_id` serial 🔑; `genre_name` varchar(50)
- **books**: `book_id` serial 🔑; `title` varchar(150); `author_id` integer → authors.author_id; `genre_id` integer → genres.genre_id; `page_count` integer
- **readers**: `reader_id` serial 🔑; `full_name` varchar(100); `city` varchar(50)
- **library_branches**: `branch_id` serial 🔑; `branch_name` varchar(100); `address` varchar(150)
- **loans**: `loan_id` serial 🔑; `book_id` integer → books.book_id; `reader_id` integer → readers.reader_id; `branch_id` integer → library_branches.branch_id; `loan_date` date; `return_date` date

**Expected columns:** `genre`, `reader_name`, `total_pages`

**Expected output (first rows):**

| genre | reader_name | total_pages |
|---|---|---|
| Classic Literature | Elena Petrova | 1200 |
| Fantasy | Ivan Sokolov | 820 |
| Mystery | Olga Volkova | 380 |
| Science Fiction | Sarah Connor | 600 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1790350306207-8sq5?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 82. Payout Trends Across Insurance Policies

*hard* · Dialects: PostgreSQL

An insurance company stores data on client policies and the claims filed against them. Analyze only claims with status 'approved' and a payout amount greater than 0.

**Tables:**

- **policies**: `policy_id` serial 🔑; `policy_holder` varchar(100); `policy_type` varchar(50); `start_date` date; `monthly_premium` decimal(10,2)
- **claims**: `claim_id` serial 🔑; `policy_id` integer → policies.policy_id; `claim_date` date; `status` varchar(20); `payout_amount` decimal(10,2)

**Expected columns:** `policy_holder`, `policy_type`, `claim_date`, `payout_amount`, `claim_seq`, `prev_payout`, `running_total`

**Expected output (first rows):**

| policy_holder | policy_type | claim_date | payout_amount | claim_seq | prev_payout | running_total |
|---|---|---|---|---|---|---|
| Anna Kowalski | Auto | 2022-02-14 | 700.00 | 1 | NULL | 700.00 |
| Anna Kowalski | Auto | 2022-11-11 | 950.00 | 2 | 700.00 | 1650.00 |
| Carlos Mendez | Health | 2023-01-20 | 4500.00 | 1 | NULL | 4500.00 |
| David Chen | Home | 2021-10-05 | 1800.00 | 1 | NULL | 1800.00 |
| David Chen | Home | 2022-12-25 | 600.00 | 2 | 1800.00 | 2400.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1790535919225-byut?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 83. Gym Member Payment Momentum

*hard* · Dialects: PostgreSQL

A fitness club chain wants to understand how recurring clients' payments change from one payment to the next, in order to spot members who are cutting back on their subscription spending.

**Tables:**

- **clubs**: `club_id` serial 🔑; `club_name` varchar(100); `city` varchar(100)
- **trainers**: `trainer_id` serial 🔑; `full_name` varchar(100); `club_id` integer → clubs.club_id
- **membership_plans**: `plan_id` serial 🔑; `plan_name` varchar(100); `monthly_price` decimal(10,2)
- **members**: `member_id` serial 🔑; `full_name` varchar(100); `club_id` integer → clubs.club_id; `trainer_id` integer → trainers.trainer_id; `join_date` date
- **subscriptions**: `subscription_id` serial 🔑; `member_id` integer → members.member_id; `plan_id` integer → membership_plans.plan_id; `start_date` date; `end_date` date
- **payments**: `payment_id` serial 🔑; `subscription_id` integer → subscriptions.subscription_id; `payment_date` date; `amount` decimal(10,2)

**Expected columns:** `member_name`, `payment_date`, `payment_amount`, `previous_amount`, `amount_change`

**Expected output (first rows):**

| member_name | payment_date | payment_amount | previous_amount | amount_change |
|---|---|---|---|---|
| Natalia Belova | 2023-07-01 | 40.00 | 70.00 | -30.00 |
| Oleg Titov | 2023-03-01 | 20.00 | 45.00 | -25.00 |
| Ivan Sokolov | 2023-05-01 | 50.00 | 70.00 | -20.00 |
| Elena Petrova | 2023-04-01 | 30.00 | 45.00 | -15.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1790360193402-040t?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 84. Fleet Revenue Growth by Month

*hard* · Dialects: PostgreSQL

A car rental network wants to understand how revenue changes month over month at each location.

**Tables:**

- **locations**: `location_id` serial 🔑; `city` varchar(100); `branch_name` varchar(100)
- **cars**: `car_id` serial 🔑; `location_id` integer → locations.location_id; `make` varchar(50); `model` varchar(50); `daily_rate` decimal(10,2)
- **customers**: `customer_id` serial 🔑; `full_name` varchar(100); `email` varchar(100); `phone` varchar(30)
- **employees**: `employee_id` serial 🔑; `location_id` integer → locations.location_id; `full_name` varchar(100); `position` varchar(50)
- **bookings**: `booking_id` serial 🔑; `customer_id` integer → customers.customer_id; `car_id` integer → cars.car_id; `employee_id` integer → employees.employee_id; `start_date` date; `end_date` date; `status` varchar(20)
- **payments**: `payment_id` serial 🔑; `booking_id` integer → bookings.booking_id; `amount` decimal(10,2); `payment_date` date; `method` varchar(30)

**Expected columns:** `branch_name`, `revenue_month`, `total_revenue`, `revenue_change`

**Expected output (first rows):**

| branch_name | revenue_month | total_revenue | revenue_change |
|---|---|---|---|
| Almaty Central | 2024-01-01 | 330.00 | 0.00 |
| Almaty Central | 2024-02-01 | 400.00 | 70.00 |
| Almaty Central | 2024-03-01 | 360.00 | -40.00 |
| Astana North | 2024-01-01 | 360.00 | 0.00 |
| Astana North | 2024-02-01 | 352.00 | -8.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1790361107661-qhhp?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 85. Monthly Box Office Peaks by Film

*hard* · Dialects: PostgreSQL

A cinema chain wants to understand the revenue dynamics of each film broken down by month of screening.

**Tables:**

- **genres**: `genre_id` serial 🔑; `genre_name` varchar(50)
- **films**: `film_id` serial 🔑; `title` varchar(150); `genre_id` integer → genres.genre_id; `release_year` integer
- **halls**: `hall_id` serial 🔑; `hall_name` varchar(50); `capacity` integer
- **screenings**: `screening_id` serial 🔑; `film_id` integer → films.film_id; `hall_id` integer → halls.hall_id; `show_date` date; `show_time` varchar(10)
- **customers**: `customer_id` serial 🔑; `full_name` varchar(100); `email` varchar(100)
- **tickets**: `ticket_id` serial 🔑; `screening_id` integer → screenings.screening_id; `customer_id` integer → customers.customer_id; `price` decimal(6,2); `purchase_date` date

**Expected columns:** `title`, `revenue_month`, `revenue`, `change_vs_prev_month`

**Expected output (first rows):**

| title | revenue_month | revenue | change_vs_prev_month |
|---|---|---|---|
| Stellar Horizon | 2024-02-01 | 60.00 | 15.00 |
| Quiet Autumn | 2024-02-01 | 17.00 | 9.00 |
| Laugh Track | 2024-02-01 | 15.00 | 8.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1790478543031-ofx6?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 86. Rising Stars of the Travel Agency

*hard* · Dialects: PostgreSQL

The agency "South Pole Travel" sells tours through a network of guides, and management wants to understand whose sales are growing fastest quarter over quarter.

**Tables:**

- **guides**: `guide_id` serial 🔑; `full_name` varchar(100); `hire_date` date
- **destinations**: `destination_id` serial 🔑; `country` varchar(100); `city` varchar(100)
- **tours**: `tour_id` serial 🔑; `tour_name` varchar(150); `destination_id` integer → destinations.destination_id; `base_price` decimal(10,2); `duration_days` integer
- **customers**: `customer_id` serial 🔑; `full_name` varchar(100); `email` varchar(150)
- **bookings**: `booking_id` serial 🔑; `customer_id` integer → customers.customer_id; `tour_id` integer → tours.tour_id; `guide_id` integer → guides.guide_id; `booking_date` date; `total_amount` decimal(10,2); `status` varchar(20)
- **payments**: `payment_id` serial 🔑; `booking_id` integer → bookings.booking_id; `payment_date` date; `amount` decimal(10,2)
- **reviews**: `review_id` serial 🔑; `booking_id` integer → bookings.booking_id; `rating` integer

**Expected columns:** `guide_name`, `sale_year`, `sale_quarter`, `quarter_revenue`, `growth_pct`, `growth_rank`

**Expected output (first rows):**

| guide_name | sale_year | sale_quarter | quarter_revenue | growth_pct | growth_rank |
|---|---|---|---|---|---|
| Anna Kowalski | 2023 | 2 | 700.00 | 100.00 | 1 |
| Marco Rossi | 2023 | 3 | 790.00 | 92.68 | 2 |
| Elena Petrova | 2023 | 4 | 700.00 | 84.21 | 3 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1790481334663-qe95?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 87. Repeat Visit Intervals by Doctor

*hard* · Dialects: PostgreSQL

A hospital wants to analyze how often patients return to the same doctor within a department, in order to spot frequent visitors and workload patterns.

Only appointments with status 'completed' should be considered. For each doctor, compute the average number of days between consecutive visits of the same patient to the same doctor (the very first visit of a patient has no previous visit and is excluded), rounded to 2 decimal places. Include only doctors who have at least 2 such intervals in total across all their patients.

Return the doctor's name (doctor_name), the department name (department_name), and the average number of days between visits (avg_days_between). Sort the result by the average number of days from smallest to largest, and for ties sort by doctor name ascending.

**Tables:**

- **departments**: `department_id` serial 🔑; `department_name` varchar(100)
- **doctors**: `doctor_id` serial 🔑; `full_name` varchar(100); `department_id` integer → departments.department_id
- **patients**: `patient_id` serial 🔑; `full_name` varchar(100); `birth_date` date
- **rooms**: `room_id` serial 🔑; `room_number` varchar(10); `department_id` integer → departments.department_id
- **appointments**: `appointment_id` serial 🔑; `patient_id` integer → patients.patient_id; `doctor_id` integer → doctors.doctor_id; `room_id` integer → rooms.room_id; `appointment_date` date; `status` varchar(20)
- **diagnoses**: `diagnosis_id` serial 🔑; `appointment_id` integer → appointments.appointment_id; `diagnosis_code` varchar(10); `description` text
- **prescriptions**: `prescription_id` serial 🔑; `appointment_id` integer → appointments.appointment_id; `medication` varchar(100); `dosage` varchar(50)

**Expected columns:** `doctor_name`, `department_name`, `avg_days_between`

**Expected output (first rows):**

| doctor_name | department_name | avg_days_between |
|---|---|---|
| Dr. Anna Ivanova | Cardiology | 16.75 |
| Dr. Mikhail Sokolov | Neurology | 31.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1789731153744-4c8k?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**
