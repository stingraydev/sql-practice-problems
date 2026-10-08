# SELECT, WHERE, ORDER BY — filtering and sorting

[← All topics](../README.md)

## 1. Over-the-Counter Medications

*easy* · Dialects: PostgreSQL, MySQL, ClickHouse

On a pharmacy shift people often ask which medications they can buy straight off the shelf — no prescription required. Output the name and price of those (`requires_prescription = false`), sorted by name.

**Tables:**

- **Customer**: `id` int 🔑; `full_name` varchar(100); `birth_date` date; `phone` varchar(30); `city` varchar(100)
- **Pharmacist**: `id` int 🔑; `last_name` varchar(100); `hire_date` date; `specialty` varchar(50)
- **Medication**: `id` int 🔑; `name` varchar(100); `manufacturer` varchar(100); `category` varchar(50); `price` decimal(10,2); `requires_prescription` boolean
- **Purchase**: `id` int 🔑; `customer_id` int → Customer.id; `pharmacist_id` int → Pharmacist.id; `purchase_date` date; `payment_method` varchar(20)
- **PurchaseItem**: `id` int 🔑; `purchase_id` int → Purchase.id; `medication_id` int → Medication.id; `quantity` int; `unit_price` decimal(10,2)

**Expected columns:** `name`, `price`

**Expected output (first rows):**

| name | price |
|---|---|
| Aspirin | 4.50 |
| Ibuprofen | 5.80 |
| VitaminC | 6.20 |
| VitaminD3 | 9.50 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/pharma-1?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 2. Customers from Berlin

*easy* · Dialects: PostgreSQL, MySQL, ClickHouse

Marketing is preparing a local promo for Berlin residents. Count how many of the pharmacy's customers are based in Berlin.

**Tables:**

- **Customer**: `id` int 🔑; `full_name` varchar(100); `birth_date` date; `phone` varchar(30); `city` varchar(100)
- **Pharmacist**: `id` int 🔑; `last_name` varchar(100); `hire_date` date; `specialty` varchar(50)
- **Medication**: `id` int 🔑; `name` varchar(100); `manufacturer` varchar(100); `category` varchar(50); `price` decimal(10,2); `requires_prescription` boolean
- **Purchase**: `id` int 🔑; `customer_id` int → Customer.id; `pharmacist_id` int → Pharmacist.id; `purchase_date` date; `payment_method` varchar(20)
- **PurchaseItem**: `id` int 🔑; `purchase_id` int → Purchase.id; `medication_id` int → Medication.id; `quantity` int; `unit_price` decimal(10,2)

**Expected columns:** `count`

**Expected output (first rows):**

| count |
|---|
| 2 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/pharma-2?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 3. Platinum-Tier Members

*easy* · Dialects: PostgreSQL, MySQL, ClickHouse

A VIP manager is arranging personalized upgrades for the program's platinum members. Output the name and country of every member with `platinum` status, sorted by name.

**Tables:**

- **Member**: `id` int 🔑; `full_name` varchar(100); `status_tier` varchar(20); `joined_at` date; `country` varchar(100)
- **Flight**: `id` int 🔑; `route` varchar(50); `distance_miles` int; `base_class` varchar(20); `flight_date` date
- **MileEarning**: `id` int 🔑; `member_id` int → Member.id; `flight_id` int → Flight.id; `miles_earned` int; `earned_date` date
- **Redemption**: `id` int 🔑; `member_id` int → Member.id; `redeemed_date` date; `miles_spent` int; `item_redeemed` varchar(100)

**Expected columns:** `full_name`, `country`

**Expected output (first rows):**

| full_name | country |
|---|---|
| Olivia Bennett | USA |
| Sophia Laurent | France |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/loyal-1?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 4. Long-Haul Flights

*easy* · Dialects: PostgreSQL, MySQL, ClickHouse

PR is producing a "Network Coverage" banner and needs the count of genuinely long flights in the catalog. Count how many flights exceed 5000 miles.

**Tables:**

- **Member**: `id` int 🔑; `full_name` varchar(100); `status_tier` varchar(20); `joined_at` date; `country` varchar(100)
- **Flight**: `id` int 🔑; `route` varchar(50); `distance_miles` int; `base_class` varchar(20); `flight_date` date
- **MileEarning**: `id` int 🔑; `member_id` int → Member.id; `flight_id` int → Flight.id; `miles_earned` int; `earned_date` date
- **Redemption**: `id` int 🔑; `member_id` int → Member.id; `redeemed_date` date; `miles_spent` int; `item_redeemed` varchar(100)

**Expected columns:** `count`

**Expected output (first rows):**

| count |
|---|
| 4 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/loyal-2?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 5. Berlin Clubs

*easy* · Dialects: PostgreSQL, MySQL, ClickHouse

A regional director is planning an audit of the Berlin branches and wants the full list. Output the names of clubs located in Berlin, sorted by name.

**Tables:**

- **Club**: `id` int 🔑; `club_name` varchar(100); `city` varchar(100); `opened_at` date
- **Trainer**: `id` int 🔑; `full_name` varchar(100); `club_id` int → Club.id; `hire_date` date; `specialization` varchar(50)
- **MemberAccount**: `id` int 🔑; `full_name` varchar(100); `signup_date` date; `monthly_fee` decimal(10,2); `plan_type` varchar(20); `home_club_id` int → Club.id
- **ClassSession**: `id` int 🔑; `class_name` varchar(100); `club_id` int → Club.id; `trainer_id` int → Trainer.id; `session_date` date; `capacity` int
- **Booking**: `id` int 🔑; `member_id` int → MemberAccount.id; `session_id` int → ClassSession.id; `attended` boolean; `booked_at` date

**Expected columns:** `club_name`

**Expected output (first rows):**

| club_name |
|---|
| PowerHouse Charlottenburg |
| PowerHouse Kreuzberg |
| PowerHouse Mitte |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/fit-1?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 6. Premium Subscriptions

*easy* · Dialects: PostgreSQL, MySQL, ClickHouse

Product is reviewing last year's upsell campaign and wants the current count of Premium subscribers. Count members currently on the `Premium` plan.

**Tables:**

- **Club**: `id` int 🔑; `club_name` varchar(100); `city` varchar(100); `opened_at` date
- **Trainer**: `id` int 🔑; `full_name` varchar(100); `club_id` int → Club.id; `hire_date` date; `specialization` varchar(50)
- **MemberAccount**: `id` int 🔑; `full_name` varchar(100); `signup_date` date; `monthly_fee` decimal(10,2); `plan_type` varchar(20); `home_club_id` int → Club.id
- **ClassSession**: `id` int 🔑; `class_name` varchar(100); `club_id` int → Club.id; `trainer_id` int → Trainer.id; `session_date` date; `capacity` int
- **Booking**: `id` int 🔑; `member_id` int → MemberAccount.id; `session_id` int → ClassSession.id; `attended` boolean; `booked_at` date

**Expected columns:** `count`

**Expected output (first rows):**

| count |
|---|
| 4 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/fit-2?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 7. 5-Star Hotels

*easy* · Dialects: PostgreSQL, MySQL, ClickHouse

A premium concierge is curating a 5-star selection for a VIP client. Output the name and city of every 5-star hotel in the chain, sorted by name.

**Tables:**

- **Hotel**: `id` int 🔑; `hotel_name` varchar(100); `city` varchar(100); `star_rating` int; `opened_year` int
- **Room**: `id` int 🔑; `hotel_id` int → Hotel.id; `room_type` varchar(50); `floor` int; `max_occupancy` int; `base_price` decimal(10,2)
- **Guest**: `id` int 🔑; `full_name` varchar(100); `country` varchar(100); `registered_at` date
- **Reservation**: `id` int 🔑; `guest_id` int → Guest.id; `room_id` int → Room.id; `check_in` date; `check_out` date; `total_paid` decimal(10,2); `status` varchar(20)
- **ServiceCharge**: `id` int 🔑; `reservation_id` int → Reservation.id; `service_type` varchar(50); `charge_amount` decimal(10,2); `charged_at` date

**Expected columns:** `hotel_name`, `city`

**Expected output (first rows):**

| hotel_name | city |
|---|---|
| Grand Plaza | Paris |
| Royal Garden | London |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/hotel-1?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 8. Rock Artists

*easy* · Dialects: PostgreSQL, MySQL, ClickHouse

A booker is planning a series of rock festivals and is shortlisting rock acts from the database. Output the name and country of every artist in the `Rock` genre, sorted by name.

**Tables:**

- **Festival**: `id` int 🔑; `festival_name` varchar(100); `year` int; `location` varchar(100); `attendance` int
- **Stage**: `id` int 🔑; `festival_id` int → Festival.id; `stage_name` varchar(100); `capacity` int
- **Artist**: `id` int 🔑; `artist_name` varchar(100); `genre` varchar(50); `country` varchar(100)
- **Performance**: `id` int 🔑; `festival_id` int → Festival.id; `stage_id` int → Stage.id; `artist_id` int → Artist.id; `start_time` timestamp; `duration_min` int; `fee_paid` decimal(12,2)
- **Sponsor**: `id` int 🔑; `sponsor_name` varchar(100); `sponsorship_amount` decimal(12,2); `festival_id` int → Festival.id; `tier` varchar(20)

**Expected columns:** `artist_name`, `country`

**Expected output (first rows):**

| artist_name | country |
|---|---|
| Iron Sparrow | UK |
| River Stones | Ireland |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/fest-1?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 9. Spacious Rooms

*easy* · Dialects: PostgreSQL, MySQL, ClickHouse

A tour operator is booking a series of family vacations and needs to know how many rooms across the chain accommodate more than 2 guests. Count those rooms.

**Tables:**

- **Hotel**: `id` int 🔑; `hotel_name` varchar(100); `city` varchar(100); `star_rating` int; `opened_year` int
- **Room**: `id` int 🔑; `hotel_id` int → Hotel.id; `room_type` varchar(50); `floor` int; `max_occupancy` int; `base_price` decimal(10,2)
- **Guest**: `id` int 🔑; `full_name` varchar(100); `country` varchar(100); `registered_at` date
- **Reservation**: `id` int 🔑; `guest_id` int → Guest.id; `room_id` int → Room.id; `check_in` date; `check_out` date; `total_paid` decimal(10,2); `status` varchar(20)
- **ServiceCharge**: `id` int 🔑; `reservation_id` int → Reservation.id; `service_type` varchar(50); `charge_amount` decimal(10,2); `charged_at` date

**Expected columns:** `count`

**Expected output (first rows):**

| count |
|---|
| 6 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/hotel-2?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 10. Festivals in 2024

*easy* · Dialects: PostgreSQL, MySQL, ClickHouse

The annual-report team is summarizing 2024's scope: how many festivals were held that year. Count the number of festivals where the year equals 2024.

**Tables:**

- **Festival**: `id` int 🔑; `festival_name` varchar(100); `year` int; `location` varchar(100); `attendance` int
- **Stage**: `id` int 🔑; `festival_id` int → Festival.id; `stage_name` varchar(100); `capacity` int
- **Artist**: `id` int 🔑; `artist_name` varchar(100); `genre` varchar(50); `country` varchar(100)
- **Performance**: `id` int 🔑; `festival_id` int → Festival.id; `stage_id` int → Stage.id; `artist_id` int → Artist.id; `start_time` timestamp; `duration_min` int; `fee_paid` decimal(12,2)
- **Sponsor**: `id` int 🔑; `sponsor_name` varchar(100); `sponsorship_amount` decimal(12,2); `festival_id` int → Festival.id; `tier` varchar(20)

**Expected columns:** `count`

**Expected output (first rows):**

| count |
|---|
| 3 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/fest-2?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 11. Endangered Species

*easy* · Dialects: PostgreSQL, MySQL, ClickHouse

A conservation curator is preparing an educational banner about rare animals in the zoo. Output the species name and the conservation status for every species with status `endangered` or `critically_endangered`. Sort by species name.

**Tables:**

- **Section**: `id` int 🔑; `section_name` varchar(100); `climate_zone` varchar(50); `area_sqm` int
- **Species**: `id` int 🔑; `species_name` varchar(100); `conservation_status` varchar(50); `native_continent` varchar(50)
- **Animal**: `id` int 🔑; `name` varchar(100); `species_id` int → Species.id; `section_id` int → Section.id; `birth_date` date; `gender` varchar(1)
- **Caretaker**: `id` int 🔑; `full_name` varchar(100); `hire_date` date; `role` varchar(50)
- **FeedingLog**: `id` int 🔑; `animal_id` int → Animal.id; `caretaker_id` int → Caretaker.id; `feed_date` date; `food_type` varchar(50); `amount_kg` decimal(8,2)

**Expected columns:** `species_name`, `conservation_status`

**Expected output (first rows):**

| species_name | conservation_status |
|---|---|
| African Elephant | endangered |
| Black Rhino | critically_endangered |
| Sumatran Orangutan | critically_endangered |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/zoo-1?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 12. Savanna Residents

*easy* · Dialects: PostgreSQL, MySQL, ClickHouse

The head zookeeper is planning re-housing in a new section and first wants the current savanna headcount. Count how many animals currently live in the `Africa Savanna` section.

**Tables:**

- **Section**: `id` int 🔑; `section_name` varchar(100); `climate_zone` varchar(50); `area_sqm` int
- **Species**: `id` int 🔑; `species_name` varchar(100); `conservation_status` varchar(50); `native_continent` varchar(50)
- **Animal**: `id` int 🔑; `name` varchar(100); `species_id` int → Species.id; `section_id` int → Section.id; `birth_date` date; `gender` varchar(1)
- **Caretaker**: `id` int 🔑; `full_name` varchar(100); `hire_date` date; `role` varchar(50)
- **FeedingLog**: `id` int 🔑; `animal_id` int → Animal.id; `caretaker_id` int → Caretaker.id; `feed_date` date; `food_type` varchar(50); `amount_kg` decimal(8,2)

**Expected columns:** `count`

**Expected output (first rows):**

| count |
|---|
| 5 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/zoo-2?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 13. Product Showcase: Rename the Columns

*easy* · Dialects: PostgreSQL

The "Kotomarket" catalog has a `products` table of cat goods: `id`, `title`, `price`, `stock`.

The storefront needs human-friendly column captions. Write a query that selects **three** columns from `products` and gives them explicit aliases with `AS`:

- `title` → `naimenovanie`
- `price` → `cena`
- `stock` → `ostatok`

Return **all** rows of the table. Do not include the `id` column.

Row order does not matter. Column order must be exactly: `naimenovanie`, `cena`, `ostatok`.

**Tables:**

- **products**: `id` integer 🔑; `title` text; `price` numeric(10,2); `stock` integer

**Expected columns:** `naimenovanie`, `cena`, `ostatok`

**Expected output (first rows):**

| naimenovanie | cena | ostatok |
|---|---|---|
| Когтеточка Башня | 2490.00 | 12 |
| Корм Сухой Индейка 1кг | 790.50 | 40 |
| Игрушка Мышка с мятой | 149.00 | 200 |
| Лежанка Гнёздышко | 1290.00 | 8 |
| Лоток Закрытый | 1890.00 | 15 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/gen-m2l1-anatomy-product-aliases?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 14. Products Under 1000 Rubles

*easy* · Dialects: PostgreSQL

The `products` table holds the product catalog of the "Kotomarket" pet store. A marketer is building a "Budget Finds" selection and wants to show only inexpensive products.

Return the title, price, and category of every product whose price is **strictly less than** 1000 rubles. For each matching product return the columns `title`, `price`, `category` in exactly this order.

Use only `SELECT` and `WHERE` with a comparison — no sorting, grouping, or other constructs.

**Tables:**

- **products**: `product_id` integer 🔑; `title` text; `category` text; `price` integer; `in_stock` integer

**Expected columns:** `title`, `price`, `category`

**Expected output (first rows):**

| title | price | category |
|---|---|---|
| Корм «Сытый кот» 2кг | 890 | корм |
| Игрушка «Мышка» | 150 | игрушки |
| Шампунь «Чистый мех» | 320 | уход |
| Лакомство «Кусь» | 260 | корм |
| Туннель «Норка» | 990 | игрушки |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/gen-m1l5-affordable-products?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 15. Delivered Orders

*easy* · Dialects: PostgreSQL

In the "Kotomarket" marketplace all orders are stored in a flat table `orders`. Each order has a number, the customer's name, a city, a status, and an amount.

The `status` column takes the values: `'обработка'` (processing), `'в пути'` (in transit), `'доставлен'` (delivered), `'отменён'` (cancelled).

The support team wants to see **only delivered** orders, to collect feedback from happy customers.

Write a query that returns **three** columns — `order_id`, `customer`, `amount` — only for orders whose `status` equals `'доставлен'`.

Use only `SELECT` and `WHERE` with an equality check. No sorting is required and row order does not matter.

**Tables:**

- **orders**: `order_id` integer 🔑; `customer` text; `city` text; `status` text; `amount` integer

**Expected columns:** `order_id`, `customer`, `amount`

**Expected output (first rows):**

| order_id | customer | amount |
|---|---|---|
| 1 | Анна Котова | 2490 |
| 3 | Мария Усова | 1500 |
| 6 | Павел Когтев | 260 |
| 8 | Тимур Хвостов | 3200 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/gen-m1l5-orders-status-delivered?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 16. Customer card: projection with aliases

*easy* · Dialects: PostgreSQL

At "Kotomarket" the marketing team prepares a customer export for a mailing and wants the column headers to be readable.

The `customers` table holds the shop's customer data.

For **every** customer, output three columns, renaming them with `AS`:

- `full_name` as **`klient`**;
- `city` as **`gorod`**;
- `signup_date` as **`data_registracii`**.

No filtering, sorting or other transformations are required — just a projection of the needed columns with aliases.

**Tables:**

- **customers**: `id` integer 🔑; `full_name` text; `city` text; `signup_date` date

**Expected columns:** `klient`, `gorod`, `data_registracii`

**Expected output (first rows):**

| klient | gorod | data_registracii |
|---|---|---|
| Анна Котова | Москва | 2024-01-12 |
| Игорь Лапкин | Санкт-Петербург | 2024-02-03 |
| Мария Усова | Казань | 2024-02-21 |
| Олег Мурзин | Новосибирск | 2024-03-15 |
| Дарья Пушистова | Екатеринбург | 2024-04-01 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/gen-m2l1-customers-projection?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 17. Products from two warehouses

*easy* · Dialects: PostgreSQL

The `tovary` table of the "Kotomarket" marketplace stores products and the cities where their warehouses are located.

A manager wants to see products stored in a warehouse **in Moscow** or **in Saint Petersburg** — to plan delivery across the two capitals.

Return the columns `id`, `nazvanie`, `gorod_sklada`, `cena` for products whose `gorod_sklada` equals `'Москва'` **or** `'Санкт-Петербург'`.

Row order does not matter.

**Tables:**

- **tovary**: `id` integer 🔑; `nazvanie` text; `gorod_sklada` text; `cena` integer

**Expected columns:** `id`, `nazvanie`, `gorod_sklada`, `cena`

**Expected output (first rows):**

| id | nazvanie | gorod_sklada | cena |
|---|---|---|---|
| 1 | Когтеточка "Башня" | Москва | 2400 |
| 3 | Игрушка-мышка | Санкт-Петербург | 150 |
| 5 | Шлейка для кота | Москва | 600 |
| 7 | Домик-будка | Санкт-Петербург | 3100 |
| 9 | Переноска "Сафари" | Москва | 1800 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/gen-m2l2-where-or-sklady?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 18. Catalog Without Archive

*easy* · Dialects: PostgreSQL

The `cat_products` table holds the product catalog of the "Kotomarket" pet store. Some products are discontinued and marked with the category `'архив'` (archive) — they should not be shown to customers.

Return all products **except** those in the `'архив'` category. For each matching product return the columns `product_id`, `name`, `category`, `price`.

Use only `SELECT` and `WHERE` — no sorting, grouping, or other constructs.

**Tables:**

- **cat_products**: `product_id` integer 🔑; `name` text; `category` text; `price` integer; `in_stock` integer

**Expected columns:** `product_id`, `name`, `category`, `price`

**Expected output (first rows):**

| product_id | name | category | price |
|---|---|---|---|
| 1 | Когтеточка «Башня» | мебель | 2490 |
| 2 | Корм «Сытый кот» 2кг | корм | 890 |
| 3 | Игрушка «Мышка» | игрушки | 150 |
| 4 | Лежанка «Облако» | мебель | 1790 |
| 6 | Лакомство «Кусь» | корм | 260 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/gen-m2l2-where-exclude-archive?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 19. Warehouse shelf: SKU, weight and price under readable names

*easy* · Dialects: PostgreSQL

In the Kotomarket warehouse, items sit in a flat table `goods`. The columns have technical names that are hard for the shelf manager to read.

Select **exactly three** columns from `goods` and label each with a human-readable name using `AS`:

| From table | Alias in result |
|------------|-----------------|
| `sku`      | `artikul`       |
| `weight_g` | `ves`           |
| `price`    | `cena`          |

Return **all rows** of the table (no filters, no sorting). Row order does not matter.

This is pure projection: nothing beyond picking the needed columns and renaming them — no `WHERE`, `ORDER BY`, or `DISTINCT`.

**Tables:**

- **goods**: `sku` text 🔑; `title` text; `weight_g` integer; `price` numeric(10,2); `shelf` text

**Expected columns:** `artikul`, `ves`, `cena`

**Expected output (first rows):**

| artikul | ves | cena |
|---|---|---|
| KM-001 | 1500 | 549.00 |
| KM-002 | 3200 | 1290.00 |
| KM-003 | 45 | 99.50 |
| KM-004 | 800 | 1790.00 |
| KM-005 | 120 | 219.00 |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/gen-m2l1-goods-projection-as?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**

---

## 20. Drop Unrated Reviews, Replace Empty Comments

*easy* · Dialects: PostgreSQL

At "Kotomarket" customers leave reviews on products. The `reviews` table is flat: one review per row. Not every review is filled in completely — sometimes the customer left no rating (`rating` is `NULL`), and sometimes they wrote no text (`comment` is `NULL`).

The moderation team is preparing a review feed and asks for an export following two rules:

1. Show **only** reviews that **have a rating** — that is, `rating` is **not** `NULL`. Reviews without a rating must be excluded.
2. If a review **has no text** (`comment` is `NULL`), output the placeholder string `'нет комментария'` instead of the empty value. If text exists, output it as is.

Return three columns: `id`, `product`, and the comment text under the alias `comment_text`.

Use `IS NOT NULL` for the filter and `COALESCE` for the placeholder substitution. No sorting is required — row order does not matter.

**Tables:**

- **reviews**: `id` integer 🔑; `product` text; `author` text; `rating` integer; `comment` text

**Expected columns:** `id`, `product`, `comment_text`

**Expected output (first rows):**

| id | product | comment_text |
|---|---|---|
| 1 | Когтеточка «Башня» | Кот в восторге, точит каждый день |
| 2 | Корм «Сытый кот» 2кг | нет комментария |
| 3 | Игрушка «Мышка» | Любимая игрушка! |
| 5 | Шлейка «Прогулка» | нет комментария |
| 7 | Витамины «Бодрость» | Шерсть стала блестящей |

**[▶ Solve online with instant checking](https://sql.coderang.dev/en/trainer/tasks/gen-m2l3-reviews-null-coalesce?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**
