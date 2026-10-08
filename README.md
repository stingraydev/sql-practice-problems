# SQL Practice Problems with Online Checking

99 hands-on SQL exercises, from `SELECT` and `WHERE` to window functions, CTEs and table design. Use them to learn SQL from scratch, get comfortable with JOINs and GROUP BY, or prepare for a data analyst, developer or QA interview.

Every problem comes with a real-world scenario, the table schema and a sample of the expected output. The easiest way to solve them is the online trainer **[SQL Arena](https://sql.coderang.dev/en?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)**: write a query in your browser, press Submit, and your answer is checked right away against hidden data. Nothing to install — every problem runs on PostgreSQL, and many also on MySQL and ClickHouse.

## Topics

| Topic | Problems |
|---|---|
| [SELECT, WHERE, ORDER BY — filtering and sorting](tasks/01-select-where-order-by.md) | 20 |
| [Aggregate functions and GROUP BY](tasks/02-aggregates-group-by.md) | 18 |
| [JOINs](tasks/03-joins.md) | 18 |
| [Subqueries](tasks/04-subqueries.md) | 9 |
| [CTEs (WITH clause)](tasks/05-cte-with.md) | 8 |
| [Window functions](tasks/06-window-functions.md) | 14 |
| [INSERT, UPDATE, DELETE — modifying data](tasks/07-insert-update-delete.md) | 6 |
| [CREATE and ALTER TABLE — table design](tasks/08-create-alter-table.md) | 6 |

## What a problem looks like

- **Statement** — a short work scenario: what to find and how to present it.
- **Tables** — columns, types, primary (🔑) and foreign (→) keys.
- **Expected columns and sample output** — the fields the checker expects and the first rows of a correct result.
- **"Solve online" link** — the problem in the trainer, with an editor, a sandbox with data and automatic checking.

There are no ready-made solutions here on purpose: a problem you peeked at teaches nothing. The trainer compares your query with the reference on data you cannot see and tells you what is off: extra rows, wrong columns, wrong order.

## All problems

### [SELECT, WHERE, ORDER BY — filtering and sorting](tasks/01-select-where-order-by.md)

1. [Over-the-Counter Medications](https://sql.coderang.dev/en/trainer/tasks/pharma-1?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
2. [Customers from Berlin](https://sql.coderang.dev/en/trainer/tasks/pharma-2?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
3. [Platinum-Tier Members](https://sql.coderang.dev/en/trainer/tasks/loyal-1?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
4. [Long-Haul Flights](https://sql.coderang.dev/en/trainer/tasks/loyal-2?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
5. [Berlin Clubs](https://sql.coderang.dev/en/trainer/tasks/fit-1?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
6. [Premium Subscriptions](https://sql.coderang.dev/en/trainer/tasks/fit-2?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
7. [5-Star Hotels](https://sql.coderang.dev/en/trainer/tasks/hotel-1?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
8. [Rock Artists](https://sql.coderang.dev/en/trainer/tasks/fest-1?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
9. [Spacious Rooms](https://sql.coderang.dev/en/trainer/tasks/hotel-2?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
10. [Festivals in 2024](https://sql.coderang.dev/en/trainer/tasks/fest-2?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
11. [Endangered Species](https://sql.coderang.dev/en/trainer/tasks/zoo-1?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
12. [Savanna Residents](https://sql.coderang.dev/en/trainer/tasks/zoo-2?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
13. [Product Showcase: Rename the Columns](https://sql.coderang.dev/en/trainer/tasks/gen-m2l1-anatomy-product-aliases?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
14. [Products Under 1000 Rubles](https://sql.coderang.dev/en/trainer/tasks/gen-m1l5-affordable-products?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
15. [Delivered Orders](https://sql.coderang.dev/en/trainer/tasks/gen-m1l5-orders-status-delivered?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
16. [Customer card: projection with aliases](https://sql.coderang.dev/en/trainer/tasks/gen-m2l1-customers-projection?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
17. [Products from two warehouses](https://sql.coderang.dev/en/trainer/tasks/gen-m2l2-where-or-sklady?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
18. [Catalog Without Archive](https://sql.coderang.dev/en/trainer/tasks/gen-m2l2-where-exclude-archive?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
19. [Warehouse shelf: SKU, weight and price under readable names](https://sql.coderang.dev/en/trainer/tasks/gen-m2l1-goods-projection-as?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
20. [Drop Unrated Reviews, Replace Empty Comments](https://sql.coderang.dev/en/trainer/tasks/gen-m2l3-reviews-null-coalesce?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy

### [Aggregate functions and GROUP BY](tasks/02-aggregates-group-by.md)

21. [Monthly Sales Pulse](https://sql.coderang.dev/en/trainer/tasks/dtm-monthly-sales-pulse?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
22. [Listening Hours by Month](https://sql.coderang.dev/en/trainer/tasks/dtm-streaming-monthly-hours?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
23. [Store delivery scorecard](https://sql.coderang.dev/en/trainer/tasks/aag-store-delivery-scorecard?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
24. [A Customer's First Digital Footprint](https://sql.coderang.dev/en/trainer/tasks/ret-first-banking-activity?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
25. [Duplicate Parcel Registrations](https://sql.coderang.dev/en/trainer/tasks/dqa-duplicate-parcel-business-keys?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
26. [Purchase Frequency in an Audio App](https://sql.coderang.dev/en/trainer/tasks/rfm-quarterly-purchase-frequency?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
27. [Which Customers Need a Win-Back Campaign?](https://sql.coderang.dev/en/trainer/tasks/rfm-client-recency-as-of-date?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
28. [From KYC Submission to Approval](https://sql.coderang.dev/en/trainer/tasks/fun-kyc-submit-to-approval?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
29. [Most Read Books Lookup](https://sql.coderang.dev/en/trainer/tasks/ai-1775636066836-hemq?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
30. [Kotomarket monthly orders report](https://sql.coderang.dev/en/trainer/tasks/gen-g6l5-monthly-orders-report?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
31. [Top 3 categories by revenue](https://sql.coderang.dev/en/trainer/tasks/ai-1777187603534-aok0?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
32. [Average Salary of Employees by Departments for 2023](https://sql.coderang.dev/en/trainer/tasks/ai-1777187735180-c7kf?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
33. [Book Sales Split by Genre](https://sql.coderang.dev/en/trainer/tasks/ai-1775635279697-f1bp?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
34. [Analysis of courier performance by delivered packages](https://sql.coderang.dev/en/trainer/tasks/ai-1781871231464-fsst?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
35. [Client Buying Behavior Study](https://sql.coderang.dev/en/trainer/tasks/ai-1775670901436-66td?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
36. [Sales Split by Product Category](https://sql.coderang.dev/en/trainer/tasks/ai-1775641700820-h25c?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
37. [Box Office Revenue by Popular Genres](https://sql.coderang.dev/en/trainer/tasks/ai-1784269947391-uk7v?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
38. [Most prolific authors with high ratings](https://sql.coderang.dev/en/trainer/tasks/ai-1783004573963-aiwb?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium

### [JOINs](tasks/03-joins.md)

39. [Second-level shelves](https://sql.coderang.dev/en/trainer/tasks/rct-store-direct-subcategories?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
40. [One-to-one, one-to-many](https://sql.coderang.dev/en/trainer/tasks/jcr-academy-relations?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
41. [Row fan-out after a JOIN](https://sql.coderang.dev/en/trainer/tasks/jcr-stream-fanout?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
42. [Comparable apartment pairs](https://sql.coderang.dev/en/trainer/tasks/lsa-district-listing-pairs?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
43. [Employees Shown with Their Departments](https://sql.coderang.dev/en/trainer/tasks/ai-1775637019643-eunn?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
44. [Popular vehicles with multiple bookings](https://sql.coderang.dev/en/trainer/tasks/ai-1777261814660-zi32?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
45. [Package delivery tracking by shipment codes](https://sql.coderang.dev/en/trainer/tasks/ai-1778256950814-4sv2?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
46. [Top players with high average score](https://sql.coderang.dev/en/trainer/tasks/ai-1779047665720-a2sr?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
47. [Analyzing Airline Route Profitability](https://sql.coderang.dev/en/trainer/tasks/ai-1782644485879-37vn?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
48. [High-Volume and Profitable Products](https://sql.coderang.dev/en/trainer/tasks/ai-1787750925236-chyg?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
49. [Most Active Authors by Published Articles Count](https://sql.coderang.dev/en/trainer/tasks/ai-1787751852906-h5a1?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
50. [Overloaded Hospital Departments](https://sql.coderang.dev/en/trainer/tasks/ai-1791184175847-gz7f?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
51. [Top hotel rooms by average rating and revenue](https://sql.coderang.dev/en/trainer/tasks/ai-1789653316245-yp2u?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
52. [Top companies by average applicant review rating](https://sql.coderang.dev/en/trainer/tasks/ai-1785332014250-r4f3?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
53. [Profitable room categories for the quarter](https://sql.coderang.dev/en/trainer/tasks/ai-1789563056453-x45d?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
54. [Doctors with the highest patient complexity](https://sql.coderang.dev/en/trainer/tasks/ai-1787905556716-aupk?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
55. [Analysis of insurance policy losses by region](https://sql.coderang.dev/en/trainer/tasks/ai-1790319194211-v0bh?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
56. [Top farmers' yield by crops](https://sql.coderang.dev/en/trainer/tasks/ai-1787822297972-f1yr?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium

### [Subqueries](tasks/04-subqueries.md)

57. [Find the most expensive item](https://sql.coderang.dev/en/trainer/tasks/easy-subq-most-expensive-product?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
58. [Pull orders from Russian customers only](https://sql.coderang.dev/en/trainer/tasks/easy-subq-orders-from-ru-customers?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
59. [Find orders bigger than average](https://sql.coderang.dev/en/trainer/tasks/easy-subq-orders-above-avg?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
60. [Customers who already ordered something](https://sql.coderang.dev/en/trainer/tasks/easy-subq-customers-with-orders?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
61. [Products that nobody bought](https://sql.coderang.dev/en/trainer/tasks/easy-subq-products-never-ordered?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
62. [Show every customer's order count](https://sql.coderang.dev/en/trainer/tasks/easy-subq-order-count-per-customer?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
63. [Cheapest pick in every category](https://sql.coderang.dev/en/trainer/tasks/easy-subq-cheapest-per-category?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
64. [Parcel scans after the watermark](https://sql.coderang.dev/en/trainer/tasks/etl-watermark-parcel-scans?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
65. [Documentary watchers](https://sql.coderang.dev/en/trainer/tasks/lsa-documentary-watchers?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy

### [CTEs (WITH clause)](tasks/05-cte-with.md)

66. [Top Bank Clients by Transaction Amount](https://sql.coderang.dev/en/trainer/tasks/ai-1777242925149-2xrk?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — hard
67. [Quarterly Performance of Sales Managers](https://sql.coderang.dev/en/trainer/tasks/ai-1775635598933-m421?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — hard
68. [Top Couriers by Deliveries with Urgency Priority](https://sql.coderang.dev/en/trainer/tasks/ai-1777263423404-9c2a?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — hard
69. [Employee Earnings Breakdown](https://sql.coderang.dev/en/trainer/tasks/ai-1775671119763-2ukv?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — hard
70. [Monthly Top Tracks in Playlists](https://sql.coderang.dev/en/trainer/tasks/ai-1775675622104-qs7d?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — hard
71. [Most-Played Artists Across Playlists](https://sql.coderang.dev/en/trainer/tasks/ai-1775675459674-b6li?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — hard
72. [Student Performance Ranking by Department with Grade Dynamics](https://sql.coderang.dev/en/trainer/tasks/ai-1788857992408-sa5x?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — hard
73. [Revenue Month-on-Month Growth](https://sql.coderang.dev/en/trainer/tasks/ai-1775673452252-fuqx?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — hard

### [Window functions](tasks/06-window-functions.md)

74. [Gaps between plays](https://sql.coderang.dev/en/trainer/tasks/ses-stream-play-gaps?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
75. [Session-start flag in an online store](https://sql.coderang.dev/en/trainer/tasks/ses-shop-session-flag?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
76. [Neobank Operating Balance](https://sql.coderang.dev/en/trainer/tasks/wfr-neobank-running-balance?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
77. [Each Product's Share of Total Revenue via SUM() OVER ()](https://sql.coderang.dev/en/trainer/tasks/gen-m7l1-window-share-of-total?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
78. [Staff Salaries: How Far From the Average](https://sql.coderang.dev/en/trainer/tasks/gen-m7l1b-staff-salary-vs-average?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
79. [Student Rating by Average Grade with Group Position](https://sql.coderang.dev/en/trainer/tasks/ai-1778004364778-0tho?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
80. [Crop Variety Yield Rankings by Plot](https://sql.coderang.dev/en/trainer/tasks/ai-1786790300439-tv0i?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
81. [Genre Champions Among Library Readers](https://sql.coderang.dev/en/trainer/tasks/ai-1790350306207-8sq5?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — hard
82. [Payout Trends Across Insurance Policies](https://sql.coderang.dev/en/trainer/tasks/ai-1790535919225-byut?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — hard
83. [Gym Member Payment Momentum](https://sql.coderang.dev/en/trainer/tasks/ai-1790360193402-040t?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — hard
84. [Fleet Revenue Growth by Month](https://sql.coderang.dev/en/trainer/tasks/ai-1790361107661-qhhp?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — hard
85. [Monthly Box Office Peaks by Film](https://sql.coderang.dev/en/trainer/tasks/ai-1790478543031-ofx6?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — hard
86. [Rising Stars of the Travel Agency](https://sql.coderang.dev/en/trainer/tasks/ai-1790481334663-qe95?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — hard
87. [Repeat Visit Intervals by Doctor](https://sql.coderang.dev/en/trainer/tasks/ai-1789731153744-4c8k?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — hard

### [INSERT, UPDATE, DELETE — modifying data](tasks/07-insert-update-delete.md)

88. [Discount on Action games](https://sql.coderang.dev/en/trainer/tasks/discount-action-games?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
89. [Seed a batch of test orders](https://sql.coderang.dev/en/trainer/tasks/qa-seed-test-orders?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
90. [Spring cleaning — drop everything unpinned](https://sql.coderang.dev/en/trainer/tasks/easy-dml-delete-unpinned?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
91. [Save your first journal entry](https://sql.coderang.dev/en/trainer/tasks/easy-dml-insert-note?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
92. [Pin every January note for the new year](https://sql.coderang.dev/en/trainer/tasks/easy-dml-pin-old-notes?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
93. [Add a test user](https://sql.coderang.dev/en/trainer/tasks/qa-insert-test-user?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy

### [CREATE and ALTER TABLE — table design](tasks/08-create-alter-table.md)

94. [Drop the Departments Table](https://sql.coderang.dev/en/trainer/tasks/ddl-drop-departments?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
95. [Add Email Column](https://sql.coderang.dev/en/trainer/tasks/ddl-add-email-column?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
96. [Drop Salary Column](https://sql.coderang.dev/en/trainer/tasks/ddl-drop-salary-column?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
97. [Rename Column name](https://sql.coderang.dev/en/trainer/tasks/ddl-rename-name-column?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — easy
98. [Normalization: split a flat book catalog into authors + books (PK/FK)](https://sql.coderang.dev/en/trainer/tasks/gen-m9l5-normalize-books-authors?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium
99. [Kotomarket: split an order into 3NF](https://sql.coderang.dev/en/trainer/tasks/gen-ddll5-orders-3nf-split?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) — medium

## More problems

This repository holds 99 problems from the free part of the trainer. [SQL Arena](https://sql.coderang.dev/en/trainer/tasks?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems) has more than 1,400: interview questions, a SQL course from scratch, courses on analytics, ClickHouse and Kafka, duels and a leaderboard.

---

[Русская версия → sql-zadachi](https://github.com/stingraydev/sql-zadachi)

© SQL Arena, [sql.coderang.dev](https://sql.coderang.dev/en?utm_source=github&utm_medium=repo&utm_campaign=sql-practice-problems)
