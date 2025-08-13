# **Main Types of SQL Commands (With Examples)**

SQL commands are divided into **5 main categories** based on their functionality. Here's a simple breakdown:

---

## **1. DDL (Data Definition Language)**  
**Purpose:** Define/modify database structures (tables, schemas).  

### **Key Commands:**  
- **`CREATE`** → Creates a new table/database.  
  ```sql
  CREATE TABLE Students (
      id INT PRIMARY KEY,
      name VARCHAR(50),
      age INT
  );
  ```
- **`ALTER`** → Modifies an existing table.  
  ```sql
  ALTER TABLE Students ADD COLUMN email VARCHAR(100);
  ```
- **`DROP`** → Deletes a table/database.  
  ```sql
  DROP TABLE Students;
  ```
- **`TRUNCATE`** → Removes all data from a table (faster than DELETE).  
  ```sql
  TRUNCATE TABLE Students;
  ```

---

## **2. DML (Data Manipulation Language)**  
**Purpose:** Manage data within tables (add, update, delete).  

### **Key Commands:**  
- **`INSERT`** → Adds new records.  
  ```sql
  INSERT INTO Students (id, name, age) 
  VALUES (1, 'Alice', 20);
  ```
- **`UPDATE`** → Modifies existing records.  
  ```sql
  UPDATE Students SET age = 21 WHERE id = 1;
  ```
- **`DELETE`** → Removes specific records.  
  ```sql
  DELETE FROM Students WHERE id = 1;
  ```

---

## **3. DQL (Data Query Language)**  
**Purpose:** Retrieve data from databases.  

### **Key Command:**  
- **`SELECT`** → Fetches data (most used SQL command).  
  ```sql
  SELECT * FROM Students; -- All columns
  SELECT name, age FROM Students WHERE age > 18;
  ```

---

## **4. DCL (Data Control Language)**  
**Purpose:** Control access to data (permissions).  

### **Key Commands:**  
- **`GRANT`** → Gives user privileges.  
  ```sql
  GRANT SELECT, INSERT ON Students TO user1;
  ```
- **`REVOKE`** → Takes back privileges.  
  ```sql
  REVOKE INSERT ON Students FROM user1;
  ```

---

## **5. TCL (Transaction Control Language)**  
**Purpose:** Manage transactions (ensure data consistency).  

### **Key Commands:**  
- **`COMMIT`** → Saves changes permanently.  
  ```sql
  COMMIT;
  ```
- **`ROLLBACK`** → Undoes changes in a transaction.  
  ```sql
  ROLLBACK;
  ```
- **`SAVEPOINT`** → Sets a rollback point.  
  ```sql
  SAVEPOINT sp1;
  ```

---

## **Summary Table**  

| **Type** | **Commands**               | **Purpose**                          |
|----------|---------------------------|--------------------------------------|
| DDL      | CREATE, ALTER, DROP       | Define database structure            |
| DML      | INSERT, UPDATE, DELETE    | Modify data                         |
| DQL      | SELECT                    | Query data                          |
| DCL      | GRANT, REVOKE             | Manage user permissions             |
| TCL      | COMMIT, ROLLBACK          | Control transactions                |

---

### **When to Use Which?**  
- Need to **create a table**? → **DDL**  
- Want to **add/update data**? → **DML**  
- Need to **fetch records**? → **DQL**  
- Managing **user access**? → **DCL**  
- Handling **bank transactions**? → **TCL**  

**Example Workflow:**  
1. **CREATE** a table (DDL)  
2. **INSERT** data (DML)  
3. **SELECT** data (DQL)  
4. **GRANT** access to a user (DCL)  
5. **COMMIT** changes (TCL)  

---

## **১. SQL Command Types (মূল ৫ ভাগ)**

| Command Type                           | Purpose                              | উদাহরণ                                |
| -------------------------------------- | ------------------------------------ | ------------------------------------- |
| **DDL (Data Definition Language)**     | Database structure define/modify করা | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| **DML (Data Manipulation Language)**   | Data insert, update, delete করা      | `INSERT`, `UPDATE`, `DELETE`          |
| **DQL (Data Query Language)**          | Data retrieve করা (শুধু SELECT)      | `SELECT`                              |
| **DCL (Data Control Language)**        | Database permission control করা      | `GRANT`, `REVOKE`                     |
| **TCL (Transaction Control Language)** | Transaction manage করা               | `COMMIT`, `ROLLBACK`, `SAVEPOINT`     |

---

## **২. Data Analysis এর জন্য কোনগুলো ব্যবহার হয়?**

### ** প্রধানত লাগে:**

* **DQL (Data Query Language)** — কারণ ডেটা analysis করার সময় আমরা ডেটা পড়ি, filter করি, aggregate করি।

  * `SELECT` → column নির্বাচন
  * `WHERE` → filter করা
  * `GROUP BY` + `HAVING` → aggregate & condition
  * `ORDER BY` → sort করা
  * `JOIN` → একাধিক টেবিল থেকে ডেটা আনা
  * Aggregate Functions → `SUM()`, `AVG()`, `COUNT()`, `MAX()`, `MIN()`
* **কিছু DML (Data Manipulation Language)** — যখন ডেটা clean বা prepare করতে হয়।

  * `UPDATE` → ডেটা ঠিক করা
  * `DELETE` → ভুল ডেটা বাদ দেওয়া
  * `INSERT` → নতুন data যোগ করা (যেমন clean data table তৈরি করা)

---

## **৩. Data Analytics-এ বাকিগুলো কেন কম লাগে?**

* **DDL (Data Definition Language)**

  * Structure create/modify করতে লাগে, কিন্তু pure analysis-এ তত দরকার হয় না।
  * সাধারণত DBA বা Data Engineer এই কাজ করে, Analyst শুধু read permission পায়।
  * উদাহরণ: নতুন টেবিল বানানো (`CREATE TABLE`) বা column rename করা (`ALTER TABLE`)।

* **DCL (Data Control Language)**

  * Permission management — কে কোন data দেখতে বা পরিবর্তন করতে পারবে।
  * Analyst সাধারণত এই কাজ করে না, Admin/DBA করে।

* **TCL (Transaction Control Language)**

  * Multiple queries একসাথে execute করে data safe রাখা।
  * Banking, e-commerce transaction-এর মতো ক্ষেত্রে বেশি লাগে, analytics-এ তেমন লাগে না কারণ analysis সাধারণত read-only environment-এ হয়।

---

## **৪. সহজ উদাহরণ (Data Analysis use case)**

**Sales Data Analysis Example**

```sql
SELECT 
    region, 
    SUM(sales) AS total_sales, 
    AVG(sales) AS avg_sales
FROM sales_data
WHERE year = 2024
GROUP BY region
ORDER BY total_sales DESC;
```

এখানে:

* `SELECT` → DQL
* `WHERE` → DQL
* `GROUP BY` → DQL
* `ORDER BY` → DQL
* Aggregate functions → DQL

সবই DQL, কারণ আমরা শুধু ডেটা পড়ছি এবং সারাংশ বের করছি।

