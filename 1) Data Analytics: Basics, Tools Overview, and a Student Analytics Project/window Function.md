## Window Function কেন ব্যবহার হয়
**সাধারণত SQL-এ আমরা GROUP BY করলে, গ্রুপভিত্তিক ক্যালকুলেশন হয়, কিন্তু প্রতিটা রোতে সেই ক্যালকুলেশন দেখানো যায় না — কারণ GROUP BY আউটপুটে রো সংখ্যা কমিয়ে দেয়।
Window Function এর সুবিধা হলো, আমরা গ্রুপ না ভেঙে একই টেবিলে ক্যালকুলেশন, র‍্যাঙ্কিং, তুলনা ইত্যাদি করতে পারি।**


## **1️⃣ Ranking Functions** (র‌্যাঙ্ক বা পজিশন নির্ধারণ করে)

| Function       | কাজ                                                         |
| -------------- | ----------------------------------------------------------- |
| `ROW_NUMBER()` | প্রতিটি রো-কে ক্রমানুসারে নম্বর দেয় (টায় থাকলেও গ্যাপ নেই)। |
| `RANK()`       | টায় হলে একই র‍্যাঙ্ক, কিন্তু গ্যাপ থাকে।                    |
| `DENSE_RANK()` | টায় হলে একই র‍্যাঙ্ক, কিন্তু গ্যাপ থাকে না।                 |
| `NTILE(n)`     | ডেটাকে **n সমান ভাগে** ভাগ করে বালতি নম্বর দেয়।             |


### Example


### dataset

```sql
CREATE TABLE Students (
    Student VARCHAR(10),
    Score INT
);

INSERT INTO Students (Student, Score) VALUES
('A', 95),
('B', 85),
('C', 85),
('D', 75),
('E', 70),
('F', 70),
('G', 60);
```

এবার Ranking Functions ব্যবহার করা যাক:

```sql
SELECT
    Student,
    Score,
    ROW_NUMBER() OVER (ORDER BY Score DESC) AS Row_Number,
    RANK()       OVER (ORDER BY Score DESC) AS Rank_No,
    DENSE_RANK() OVER (ORDER BY Score DESC) AS Dense_Rank,
    NTILE(3)     OVER (ORDER BY Score DESC) AS Ntile_3
FROM Students;
```

👉 Output হবে এমন:

| Student | Score | Row\_Number | Rank\_No | Dense\_Rank | Ntile\_3 |
| ------- | ----- | ----------- | -------- | ----------- | -------- |
| A       | 95    | 1           | 1        | 1           | 1        |
| B       | 85    | 2           | 2        | 2           | 1        |
| C       | 85    | 3           | 2        | 2           | 1        |
| D       | 75    | 4           | 4        | 3           | 2        |
| E       | 70    | 5           | 5        | 4           | 2        |
| F       | 70    | 6           | 5        | 4           | 3        |
| G       | 60    | 7           | 7        | 5           | 3        |


---

## **2️⃣ Aggregate Functions as Window Functions** (গ্রুপের ওপর ক্যালকুলেশন, কিন্তু গ্রুপ না ভেঙে)

> এগুলো সাধারণ `SUM()` বা `AVG()`-এর মতোই, কিন্তু `OVER()` ব্যবহার করলে **window function** হয়ে যায়।

| Function  | কাজ                              |
| --------- | -------------------------------- |
| `SUM()`   | একটি পার্টিশন/উইন্ডো জুড়ে যোগফল। |
| `AVG()`   | গড় বের করে।                      |
| `MIN()`   | সর্বনিম্ন মান।                   |
| `MAX()`   | সর্বোচ্চ মান।                    |
| `COUNT()` | গণনা করে।                        |


### Dataset

```sql
CREATE TABLE Students (
    Student VARCHAR(10),
    Score INT
);

INSERT INTO Students (Student, Score) VALUES
('A', 95),
('B', 85),
('C', 85),
('D', 75),
('E', 70),
('F', 70),
('G', 60);
```

---

### Query (Aggregate Functions as Window Functions)

```sql
SELECT
    Student,
    Score,

    SUM(Score)   OVER () AS Total_Sum,        -- সব রো এর যোগফল
    AVG(Score)   OVER () AS Avg_Score,        -- সব রো এর গড়
    MIN(Score)   OVER () AS Min_Score,        -- সব রো এর সর্বনিম্ন
    MAX(Score)   OVER () AS Max_Score,        -- সব রো এর সর্বোচ্চ
    COUNT(Score) OVER () AS Total_Count       -- সব রো এর সংখ্যা

FROM Students;
```

---

### Output (Window ছাড়া Group করলে এক লাইনে আসতো, কিন্তু এখানে প্রতিটি রো-তেই রেজাল্ট দেখাবে)

| Student | Score | Total\_Sum | Avg\_Score | Min\_Score | Max\_Score | Total\_Count |
| ------- | ----- | ---------- | ---------- | ---------- | ---------- | ------------ |
| A       | 95    | 540        | 77.14      | 60         | 95         | 7            |
| B       | 85    | 540        | 77.14      | 60         | 95         | 7            |
| C       | 85    | 540        | 77.14      | 60         | 95         | 7            |
| D       | 75    | 540        | 77.14      | 60         | 95         | 7            |
| E       | 70    | 540        | 77.14      | 60         | 95         | 7            |
| F       | 70    | 540        | 77.14      | 60         | 95         | 7            |
| G       | 60    | 540        | 77.14      | 60         | 95         | 7            |


---

## **3️⃣ Value Functions** (পূর্ববর্তী বা পরবর্তী রো-এর ডেটা আনা)

| Function        | কাজ                                           |
| --------------- | --------------------------------------------- |
| `LAG(expr, n)`  | বর্তমান রো থেকে **n রো আগে** থাকা ভ্যালু আনে। |
| `LEAD(expr, n)` | বর্তমান রো থেকে **n রো পরে** থাকা ভ্যালু আনে। |
| `FIRST_VALUE()` | উইন্ডোর প্রথম ভ্যালু আনে।                     |
| `LAST_VALUE()`  | উইন্ডোর শেষ ভ্যালু আনে।                       |
| `NTH_VALUE()`   | উইন্ডোর n-তম ভ্যালু আনে।                      |

### Example

### Dataset

```sql
CREATE TABLE Students (
    Student VARCHAR(10),
    Score INT
);

INSERT INTO Students (Student, Score) VALUES
('A', 95),
('B', 85),
('C', 85),
('D', 75),
('E', 70),
('F', 70),
('G', 60);
```

### Query (Value Functions)

```sql
SELECT
    Student,
    Score,

    LAG(Score, 1)  OVER (ORDER BY Score DESC) AS Prev_Score,   -- 1 রো আগে
    LEAD(Score, 1) OVER (ORDER BY Score DESC) AS Next_Score,   -- 1 রো পরে

    FIRST_VALUE(Score) OVER (ORDER BY Score DESC) AS First_Score, -- প্রথম ভ্যালু
    LAST_VALUE(Score)  OVER (ORDER BY Score DESC 
                             ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS Last_Score, -- শেষ ভ্যালু

    NTH_VALUE(Score, 3) OVER (ORDER BY Score DESC 
                              ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS Third_Score -- ৩য় ভ্যালু

FROM Students;
```

### Output

| Student | Score | Prev\_Score | Next\_Score | First\_Score | Last\_Score | Third\_Score |
| ------- | ----- | ----------- | ----------- | ------------ | ----------- | ------------ |
| A       | 95    | NULL        | 85          | 95           | 60          | 85           |
| B       | 85    | 95          | 85          | 95           | 60          | 85           |
| C       | 85    | 85          | 75          | 95           | 60          | 85           |
| D       | 75    | 85          | 70          | 95           | 60          | 85           |
| E       | 70    | 75          | 70          | 95           | 60          | 85           |
| F       | 70    | 70          | 60          | 95           | 60          | 85           |
| G       | 60    | 70          | NULL        | 95           | 60          | 85           |



---

## **4️⃣ Statistical / Offset Functions** (ডিস্ট্রিবিউশন বা শতাংশ নির্ধারণ করে)

| Function            | কাজ                                                                    |
| ------------------- | ---------------------------------------------------------------------- |
| `PERCENT_RANK()`    | 0–1 স্কেলে র‌্যাঙ্ক নির্ধারণ করে।                                      |
| `CUME_DIST()`       | cumulative distribution — একটি রো-এর আগে বা সমান স্কোরের রো-এর অনুপাত। |
| `RATIO_TO_REPORT()` | একটি ভ্যালুর অনুপাত পুরো পার্টিশনের যোগফলের সাথে।                      |

---

💡 **মনে রাখবে**

* সব Window Function-এর মধ্যে `OVER()` ক্লজ থাকে, যেটা দিয়ে `PARTITION BY` ও `ORDER BY` ঠিক করা হয়।
* `PARTITION BY` = ডেটা গ্রুপ করা
* `ORDER BY` (inside OVER) = উইন্ডোর ভিতরে সাজানো

