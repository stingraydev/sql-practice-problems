# JOINs

[← All topics](../README.md)

## 39. Second-level shelves

*easy* · Dialects: PostgreSQL

You are a catalog analyst at a large marketplace. Product categories form a tree: every category may have a parent, root sections have none. The storefront team is redesigning the `'Electronics'` section page and needs the list of its DIRECT subcategories only — grandchildren and deeper levels must not appear, they get their own pages.

Table categories: id, name, parent_id (NULL for root sections). The section is named exactly `'Electronics'`.

Return columns:
- `subcategory_name` — name of a direct subcategory of `'Electronics'` (text, as stored).

Sort by subcategory_name ascending. Categories of other sections and anything deeper than one level below `'Electronics'` are excluded. Direct children have unique names.

**Tables:**

- **categories**: `id` int 🔑 — Category id; `name` text — Category name; `parent_id` int — Parent category (NULL for roots)

**Expected columns:** `subcategory_name`

**Expected output (first rows):**

| subcategory_name |
|---|
| Audio |
| Cameras |
| Laptops |
| Phones |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/rct-store-direct-subcategories?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 40. One-to-one, one-to-many

*easy* · Dialects: PostgreSQL

You are an analyst at the Brightpath online school. There are three tables in the database: students — one row per student; student_profiles — a profile form, exactly one per student (a one-to-one relationship); enrollments — course sign-ups: a student may have several of them, or none at all (a one-to-many relationship). The curator needs a summary: which plan each student is on and how many courses they attend. Important: the profile form must not multiply a student's rows, and the absence of course sign-ups must not throw the student out of the report.

Return the columns:
- `full_name` — the student's name;
- `plan` — the plan from the profile form;
- `courses_cnt` — the number of course sign-ups (an integer; 0 if there are none).
Sorting: courses_cnt descending, then full_name ascending. Students with no course sign-ups must be present in the result with the value 0.

**Tables:**

- **students**: `student_id` integer 🔑 — Student id; `full_name` text — Student name
- **student_profiles**: `student_id` integer 🔑 — Student id (exactly one profile per student); `city` text — City; `plan` text — Plan: free or premium
- **enrollments**: `enrollment_id` integer 🔑 — Enrollment id; `student_id` integer — Student id; `course_title` text — Course title

**Expected columns:** `full_name`, `plan`, `courses_cnt`

**Expected output (first rows):**

| full_name | plan | courses_cnt |
|---|---|---|
| Chloe Davis | premium | 3 |
| Alice Brown | premium | 2 |
| Emma Fisher | free | 2 |
| Henry Irwin | premium | 2 |
| Jack Kelly | premium | 2 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/jcr-academy-relations?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 41. Row fan-out after a JOIN

*easy* · Dialects: PostgreSQL

You are a junior analyst at the PlayReel streaming service. The catalog lives in shows (one row per show) and seasons live in seasons: a show may have several. A teammate complained that after joining the two tables shows got duplicated and the catalog view looks bloated. You are asked to show the scale of the problem: for every show that occupies more than one row after the join, output how many rows it fans out into.

Return columns:
- `title` — show title;
- `join_rows` — how many rows this show produces after joining to seasons (integer, strictly greater than 1).
Sort by join_rows descending, then title ascending. Exclude shows that produce exactly one row or have no seasons at all.

**Tables:**

- **shows**: `show_id` integer 🔑 — Show id; `title` text — Show title
- **seasons**: `season_id` integer 🔑 — Season id; `show_id` integer — Show id; `season_no` integer — Season number

**Expected columns:** `title`, `join_rows`

**Expected output (first rows):**

| title | join_rows |
|---|---|
| Silver Steppe | 4 |
| Iron Harbor | 3 |
| Paper Storm | 3 |
| Quantum Alley | 2 |
| Sunken City | 2 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/jcr-stream-fanout?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 42. Comparable apartment pairs

*easy* · Dialects: PostgreSQL

You are an analyst at the UrbanNest real-estate agency. The appraisal team wants a tool that finds comparable listings: two apartments in the same district with the same number of rooms make a perfect pair for a price sanity check. You have the listings table with active offers.

For every district, find all pairs of listings with the same number of rooms. Each pair must appear exactly once: the listing with the smaller id comes first. Listings with an unknown number of rooms (NULL) never form pairs.

Return columns:
- `district` — the district;
- `rooms` — number of rooms;
- `listing_a` — id of the listing with the smaller id in the pair;
- `listing_b` — id of the listing with the larger id in the pair;
- `price_gap` — absolute price difference within the pair (raw number, no rounding).

Sort by district alphabetically, then listing_a ascending, then listing_b ascending. If a district has three matching listings, all three pairwise combinations must appear.

**Tables:**

- **listings**: `id` int 🔑 — Listing id; `district` text — City district; `rooms` int — Number of rooms (NULL if unknown); `price` numeric(12,2) — Price, units

**Expected columns:** `district`, `rooms`, `listing_a`, `listing_b`, `price_gap`

**Expected output (first rows):**

| district | rooms | listing_a | listing_b | price_gap |
|---|---|---|---|---|
| Docklands | 2 | 10 | 12 | 3000.00 |
| Hillside | 3 | 7 | 8 | 10000.00 |
| Old Town | 1 | 4 | 5 | 5000.00 |
| Riverside | 2 | 1 | 2 | 15000.00 |
| Riverside | 3 | 3 | 13 | 5000.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/lsa-district-listing-pairs?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 43. Employees Shown with Their Departments

*easy* · Dialects: PostgreSQL, ClickHouse

The company has employee and department tables. Display a list of all employees with the name of the department they work in. Sort the result by employee last name alphabetically. Show first name, last name, and department name.

**Tables:**

- **departments**: `id` serial 🔑; `name` varchar(100)
- **employees**: `id` serial 🔑; `first_name` varchar(50); `last_name` varchar(50); `department_id` integer → departments.id

**Expected columns:** `first_name`, `last_name`, `department_name`

**Expected output (first rows):**

| first_name | last_name | department_name |
|---|---|---|
| Anna | Clark | Sales |
| Igor | Fedorov | Sales |
| Elena | Foster | Marketing |
| Alex | Johnson | Engineering |
| Paul | Newman | Engineering |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1775637019643-eunn?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 44. Popular vehicles with multiple bookings

*easy* · Dialects: PostgreSQL, ClickHouse

Find all vehicles that have been booked more than once and display the number of bookings for each, sorted by popularity.

**Tables:**

- **vehicles**: `vehicle_id` serial 🔑; `model` varchar(100); `license_plate` varchar(20); `daily_rate` decimal(8,2)
- **bookings**: `booking_id` serial 🔑; `vehicle_id` integer → vehicles.vehicle_id; `customer_name` varchar(100); `booking_date` date

**Expected columns:** `vehicle_id`, `model`, `license_plate`, `booking_count`

**Expected output (first rows):**

| vehicle_id | model | license_plate | booking_count |
|---|---|---|---|
| 2 | Honda Accord | XY789EF | 3 |
| 1 | Toyota Camry | AB123CD | 3 |
| 3 | BMW 3 Series | KL456GH | 2 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1777261814660-zi32?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 45. Package delivery tracking by shipment codes

*easy* · Dialects: PostgreSQL, ClickHouse

Find all packages with status 'in_transit', sort them by shipment date in ascending order and limit results to the first 5 records. Display package information along with recipient details from the related table.

**Tables:**

- **shipments**: `shipment_id` serial 🔑; `package_code` varchar(20); `weight` decimal(5,2); `status` varchar(30); `ship_date` date; `recipient_id` integer → recipients.recipient_id
- **recipients**: `recipient_id` serial 🔑; `full_name` varchar(100); `city` varchar(50); `phone` varchar(15)

**Expected columns:** `shipment_id`, `package_code`, `weight`, `status`, `ship_date`, `full_name`, `city`, `phone`

**Expected output (first rows):**

| shipment_id | package_code | weight | status | ship_date | full_name | city | phone |
|---|---|---|---|---|---|---|---|
| 4 | PKG-2024-004 | 0.90 | in_transit | 2024-01-09 | Dmitri Orlov | Novosibirsk | 89994445566 |
| 1 | PKG-2024-001 | 2.50 | in_transit | 2024-01-10 | Maria Volkova | Moscow | 89991234567 |
| 6 | PKG-2024-006 | 2.30 | in_transit | 2024-01-11 | Maria Volkova | Moscow | 89991234567 |
| 3 | PKG-2024-003 | 3.80 | in_transit | 2024-01-12 | Olga Smirnova | Yekaterinburg | 89991112233 |
| 7 | PKG-2024-007 | 1.50 | in_transit | 2024-01-13 | Ivan Sokolov | Saint Petersburg | 89998765432 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1778256950814-4sv2?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 46. Top players with high average score

*medium* · Dialects: PostgreSQL

Analysts want to highlight consistently strong players, counting only high-value matches. From the `match_results` table consider only matches where `score` > `60`. Over those matches, for each player compute the number of games played (`games_played`) and the average score (`avg_score`). Keep only players who have at least `3` such matches (with `score` > `60`) and whose average score across them exceeds `75`. Output the player's name (`name`), the count of such matches, and their average score, sorting the result by the average score `avg_score` in descending order.

**Tables:**

- **players**: `player_id` int 🔑; `name` varchar(100); `country` varchar(50); `join_date` date
- **games**: `game_id` int 🔑; `title` varchar(100); `release_year` integer; `genre` varchar(50)
- **match_results**: `match_id` int 🔑; `player_id` integer → players.player_id; `game_id` integer → games.game_id; `score` integer; `match_date` date
- **achievements**: `achievement_id` int 🔑; `player_id` integer → players.player_id; `title` varchar(100); `unlocked_date` date

**Expected columns:** `name`, `games_played`, `avg_score`

**Expected output (first rows):**

| name | games_played | avg_score |
|---|---|---|
| Carlos Martinez | 3 | 92.0000000000000000 |
| Elena Petrova | 4 | 83.0000000000000000 |
| Alice Johnson | 3 | 82.6666666666666667 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1779047665720-a2sr?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 47. Analyzing Airline Route Profitability

*medium* · Dialects: PostgreSQL

An airline company wants to identify its most profitable routes. Find routes where the average ticket price exceeds 250 dollars, grouping by destination and showing the number of distinct flights, average ticket price, and total revenue. Sort results by descending total revenue and output the following columns: route (origin to destination airport code), number of flights, average ticket price, and total revenue. Round `avg_ticket_price`, `total_revenue` to 2 decimal places.

**Tables:**

- **airports**: `airport_id` serial 🔑; `airport_code` varchar(3); `city_name` varchar(100)
- **flights**: `flight_id` serial 🔑; `origin_airport_id` integer → airports.airport_id; `destination_airport_id` integer → airports.airport_id; `flight_number` varchar(10)
- **bookings**: `booking_id` serial 🔑; `flight_id` integer → flights.flight_id; `ticket_price` decimal(10,2)
- **passengers**: `passenger_id` serial 🔑; `booking_id` integer → bookings.booking_id; `passenger_name` varchar(100)

**Expected columns:** `route`, `flights_count`, `avg_ticket_price`, `total_revenue`

**Expected output (first rows):**

| route | flights_count | avg_ticket_price | total_revenue |
|---|---|---|---|
| JFK-LAX | 3 | 285.00 | 1710.00 |
| JFK-LHR | 2 | 450.00 | 1350.00 |
| LAX-JFK | 2 | 290.00 | 1160.00 |
| LHR-CDG | 1 | 380.00 | 380.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1782644485879-37vn?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 48. High-Volume and Profitable Products

*medium* · Dialects: PostgreSQL

A warehouse manager is analyzing product performance. Find products that sold more than 50 units, where the average selling price of each product is at least 20% higher than its cost price. Results must include product name, total units sold, average selling price, and cost price, sorted by sales volume in descending order.

**Tables:**

- **products**: `product_id` serial 🔑; `product_name` varchar(100); `cost_price` decimal(10,2)
- **warehouses**: `warehouse_id` serial 🔑; `warehouse_name` varchar(100); `location` varchar(100)
- **stock**: `stock_id` serial 🔑; `product_id` integer → products.product_id; `warehouse_id` integer → warehouses.warehouse_id; `quantity_on_hand` integer
- **sales**: `sale_id` serial 🔑; `product_id` integer → products.product_id; `warehouse_id` integer → warehouses.warehouse_id; `quantity_sold` integer; `selling_price` decimal(10,2)

**Expected columns:** `product_name`, `total_units_sold`, `avg_selling_price`, `cost_price`

**Expected output (first rows):**

| product_name | total_units_sold | avg_selling_price | cost_price |
|---|---|---|---|
| Mechanical Keyboard | 60 | 96.5000000000000000 | 65.00 |
| HDMI Cable | 60 | 4.5000000000000000 | 3.00 |
| Wireless Mouse | 55 | 22.0000000000000000 | 15.00 |
| Laptop Dell XPS | 55 | 665.0000000000000000 | 450.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1787750925236-chyg?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 49. Most Active Authors by Published Articles Count

*medium* · Dialects: PostgreSQL

A news portal needs to identify authors who have published more than 3 articles in total and display their names, total number of distinct publications, and average number of comments per article (articles with no comments count too). Sort the results by the number of articles in descending order, then by average comments in descending order. Round `avg_comments_per_article` to 2 decimal places.

**Tables:**

- **authors**: `author_id` serial 🔑; `author_name` varchar(100); `email` varchar(100)
- **articles**: `article_id` serial 🔑; `author_id` integer → authors.author_id; `title` varchar(255); `published_date` date
- **comments**: `comment_id` serial 🔑; `article_id` integer → articles.article_id; `commenter_name` varchar(100); `comment_text` text; `created_at` timestamp
- **categories**: `category_id` serial 🔑; `article_id` integer → articles.article_id; `category_name` varchar(50)

**Expected columns:** `author_name`, `total_articles`, `avg_comments_per_article`

**Expected output (first rows):**

| author_name | total_articles | avg_comments_per_article |
|---|---|---|
| Elena Petrova | 4 | 2.75 |
| Ivan Sokolov | 4 | 1.75 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1787751852906-h5a1?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 50. Overloaded Hospital Departments

*medium* · Dialects: PostgreSQL

The hospital administration wants to understand which departments are overloaded with patient visits in order to redistribute doctors.

**Tables:**

- **departments**: `department_id` serial 🔑; `name` varchar(100)
- **doctors**: `doctor_id` serial 🔑; `full_name` varchar(100); `department_id` integer → departments.department_id
- **patients**: `patient_id` serial 🔑; `full_name` varchar(100)
- **visits**: `visit_id` serial 🔑; `patient_id` integer → patients.patient_id; `doctor_id` integer → doctors.doctor_id; `visit_date` date; `cost` decimal(10,2)

**Expected columns:** `department_name`, `visit_count`, `avg_cost`

**Expected output (first rows):**

| department_name | visit_count | avg_cost |
|---|---|---|
| Kardiologiya | 5 | 1620.00 |
| Pediatriya | 3 | 750.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1791184175847-gz7f?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 51. Top hotel rooms by average rating and revenue

*medium* · Dialects: PostgreSQL

A hotel chain is analyzing the quality of its rooms based on guest reviews and financial performance. For each room, calculate the average rating from all reviews and total revenue from bookings, but only for rooms that have received at least 3 reviews and generated at least 5000 rubles in revenue.

Return the room number, room type, average rating (rounded to 2 decimals), total revenue, and review count. Sort by average rating descending, then by total revenue descending in case of a tie.

**Tables:**

- **hotels**: `hotel_id` serial 🔑; `hotel_name` varchar(100)
- **rooms**: `room_id` serial 🔑; `hotel_id` integer → hotels.hotel_id; `room_number` varchar(20); `room_type` varchar(50)
- **reservations**: `reservation_id` serial 🔑; `room_id` integer → rooms.room_id; `guest_name` varchar(100); `total_price` decimal(10,2)
- **reviews**: `review_id` serial 🔑; `reservation_id` integer → reservations.reservation_id; `rating` integer; `comment` text

**Expected columns:** `room_number`, `room_type`, `avg_rating`, `total_revenue`, `review_count`

**Expected output (first rows):**

| room_number | room_type | avg_rating | total_revenue | review_count |
|---|---|---|---|---|
| 305 | Suite | 4.75 | 13000.00 | 4 |
| 201 | Deluxe | 4.67 | 7500.00 | 3 |
| 101 | Standard | 4.33 | 6500.00 | 3 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1789653316245-yp2u?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 52. Top companies by average applicant review rating

*medium* · Dialects: PostgreSQL

A job portal hosts vacancies from various companies, and each applicant can leave a review about their interview experience. Find companies with an average rating of at least 4.0 across all reviews, sort them by average rating in descending order, and output the company name, number of reviews received, and average rating (rounded to one decimal place).

**Tables:**

- **companies**: `id` serial 🔑; `name` varchar(100); `industry` varchar(50)
- **job_postings**: `id` serial 🔑; `company_id` integer → companies.id; `title` varchar(150); `salary_min` decimal(10,2); `salary_max` decimal(10,2)
- **applicants**: `id` serial 🔑; `name` varchar(100); `email` varchar(100)
- **reviews**: `id` serial 🔑; `job_posting_id` integer → job_postings.id; `applicant_id` integer → applicants.id; `rating` integer; `review_text` text

**Expected columns:** `name`, `review_count`, `avg_rating`

**Expected output (first rows):**

| name | review_count | avg_rating |
|---|---|---|
| GreenEnergy Inc | 2 | 5.0 |
| CloudSync Systems | 2 | 4.5 |
| TechCore Solutions | 5 | 4.0 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1785332014250-r4f3?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 53. Profitable room categories for the quarter

*medium* · Dialects: PostgreSQL

A hotel chain is analyzing the profitability of its room inventory. Find all room categories that generated revenue above the average for the quarter. For each such category, return the category name, number of bookings, average nightly rate, and total revenue for the period. Sort the results by total revenue in descending order.

**Tables:**

- **room_categories**: `category_id` serial 🔑; `category_name` varchar(100)
- **rooms**: `room_id` serial 🔑; `room_number` varchar(20); `category_id` integer → room_categories.category_id
- **reservations**: `reservation_id` serial 🔑; `room_id` integer → rooms.room_id; `check_in` date; `check_out` date; `nightly_rate` decimal(10, 2)
- **reservation_dates**: `reservation_id` integer 🔑; `revenue` decimal(12, 2)

**Expected columns:** `category_name`, `booking_count`, `avg_nightly_rate`, `total_revenue`

**Expected output (first rows):**

| category_name | booking_count | avg_nightly_rate | total_revenue |
|---|---|---|---|
| Deluxe | 4 | 180.00 | 4680.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1789563056453-x45d?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 54. Doctors with the highest patient complexity

*medium* · Dialects: PostgreSQL

A hospital needs to identify doctors who deal with the most complex cases. Find all doctors whose patients have an average age exceeding 50 years, and return the doctor name, the count of distinct patients, and average patient age. Sort results by average age in descending order, then by doctor name alphabetically. Round `average_patient_age` to 1 decimal place.

**Tables:**

- **doctors**: `doctor_id` serial 🔑; `name` varchar(100); `specialty` varchar(50)
- **patients**: `patient_id` serial 🔑; `name` varchar(100); `age` integer; `admission_date` date
- **appointments**: `appointment_id` serial 🔑; `doctor_id` integer → doctors.doctor_id; `patient_id` integer → patients.patient_id; `visit_date` date; `notes` text
- **diagnoses**: `diagnosis_id` serial 🔑; `appointment_id` integer → appointments.appointment_id; `condition` varchar(100); `severity` varchar(20)

**Expected columns:** `doctor_name`, `patient_count`, `average_patient_age`

**Expected output (first rows):**

| doctor_name | patient_count | average_patient_age |
|---|---|---|
| Ivan Petrov | 3 | 65.0 |
| Alexei Romanov | 2 | 56.5 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1787905556716-aupk?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 55. Analysis of insurance policy losses by region

*medium* · Dialects: PostgreSQL

An insurance company analyzes the profitability of its policy portfolio across geographic regions. Find all regions where claims paid exceed premiums received by more than 50,000 rubles, indicating unprofitability.

For each such region, return the region name, total premiums received, total claims paid, and loss amount (difference between payments and premiums). Sort results by loss size in descending order.

**Tables:**

- **regions**: `region_id` serial 🔑; `region_name` varchar(100)
- **policies**: `policy_id` serial 🔑; `region_id` integer → regions.region_id; `policy_number` varchar(50); `premium_amount` decimal(10,2); `issue_date` date
- **claims**: `claim_id` serial 🔑; `policy_id` integer → policies.policy_id; `claim_number` varchar(50); `claim_amount` decimal(10,2); `claim_date` date; `status` varchar(20)
- **claim_payments**: `payment_id` serial 🔑; `claim_id` integer → claims.claim_id; `payment_amount` decimal(10,2); `payment_date` date

**Expected columns:** `region_name`, `total_premiums`, `total_payments`, `loss_amount`

**Expected output (first rows):**

| region_name | total_premiums | total_payments | loss_amount |
|---|---|---|---|
| Moskva | 235000.00 | 365000.00 | 130000.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1790319194211-v0bh?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 56. Top farmers' yield by crops

*medium* · Dialects: PostgreSQL

On an agricultural exchange, you need to identify farmers who grow multiple crops and harvest an average of at least 500 centners of yield per crop. Find the farmer ID, name, number of distinct crops grown, and average yield, sorted by average yield in descending order. Round `avg_yield` to 2 decimal places.

**Tables:**

- **farmers**: `farmer_id` serial 🔑; `name` varchar(100); `region` varchar(50)
- **crops**: `crop_id` serial 🔑; `crop_name` varchar(100); `crop_type` varchar(50)
- **harvest_records**: `record_id` serial 🔑; `farmer_id` integer → farmers.farmer_id; `crop_id` integer → crops.crop_id; `harvest_year` integer; `yield_centners` decimal(10, 2)
- **soil_quality**: `quality_id` serial 🔑; `farmer_id` integer → farmers.farmer_id; `soil_type` varchar(50); `ph_level` decimal(3, 1)

**Expected columns:** `farmer_id`, `name`, `crops_count`, `avg_yield`

**Expected output (first rows):**

| farmer_id | name | crops_count | avg_yield |
|---|---|---|---|
| 5 | Mikhail Smirnov | 3 | 560.00 |
| 2 | Elena Volkova | 2 | 555.00 |
| 3 | Sergei Orlov | 2 | 505.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/ai-1787822297972-f1yr?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**
