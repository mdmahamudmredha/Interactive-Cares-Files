##  RDBMS Protocol মেনে চলে কারা?

RDBMS (Relational Database Management System) মানে হল এমন ডাটাবেস সিস্টেম যা **টেবিল আকারে ডেটা স্টোর করে**, ডেটার মধ্যে **relationship** থাকে, আর **SQL (Structured Query Language)** দিয়ে ম্যানেজ হয়।

**জনপ্রিয় RDBMS প্ল্যাটফর্মগুলো হলো:**

* **MySQL**
* **PostgreSQL**
* **Oracle Database**
* **Microsoft SQL Server**
* **MariaDB**
* **SQLite**

**তারা যা মেনে চলে:**

* **ACID Properties** (Atomicity, Consistency, Isolation, Durability) → ট্রানজ্যাকশন সেফ রাখে।
* **Schema-based design** → আগে থেকেই ডেটার structure ঠিক করা লাগে (table, column, datatype)।
* **SQL Commands** দিয়ে Query করা হয়।


---
## RDBMS Protocol মেনে চলে কারা? (সংক্ষেপে) 

1. **প্রতিটা RDBMS (MySQL, PostgreSQL, Oracle, MS SQL Server, MariaDB, SQLite) কোন Use Case-এ বেশি ব্যবহার হয়**
2. **ACID Properties (Atomicity, Consistency, Isolation, Durability) ডিটেইলস**

---

## **1. প্রতিটি RDBMS-এর Use Case**

সবগুলোই **RDBMS Protocol** (Structured data, SQL, ACID compliance) ফলো করে, কিন্তু কিছু ফিচার ও পারফরম্যান্স ডিফারেন্স থাকার কারণে আলাদা আলাদা Use Case আছে।

| **Database**             | **Best For**                                             | **Example Use Case**                               |
| ------------------------ | -------------------------------------------------------- | -------------------------------------------------- |
| **MySQL**                | Web applications, read-heavy workloads, startups         | WordPress, eCommerce sites, booking systems        |
| **PostgreSQL**           | Complex queries, data integrity, analytics-heavy systems | Banking software, GIS mapping, scientific research |
| **Oracle Database**      | Enterprise-level applications, mission-critical data     | Airlines booking, Government tax systems, ERP      |
| **Microsoft SQL Server** | Windows ecosystem, enterprise BI (Business Intelligence) | Hospital management, Payroll systems               |
| **MariaDB**              | MySQL alternative, open-source with extra features       | SaaS platforms, small to medium business apps      |
| **SQLite**               | Lightweight, embedded systems, offline apps              | Mobile apps, IoT devices, desktop software         |

💡 **সংক্ষিপ্ত তুলনা:**

* **MySQL** → ফাস্ট, ওয়েব অ্যাপের জন্য ভালো, সস্তা হোস্টিং সাপোর্ট বেশি।
* **PostgreSQL** → বেশি পাওয়ারফুল ও ফিচার-সমৃদ্ধ, কমপ্লেক্স রিপোর্ট/অ্যানালিটিক্সে ভালো।
* **Oracle** → অনেক ব্যয়বহুল কিন্তু অনেক বড় এন্টারপ্রাইজের জন্য প্রিমিয়াম সাপোর্ট।
* **SQL Server** → মাইক্রোসফট ইকোসিস্টেমে ইন্টিগ্রেশন দারুণ।
* **MariaDB** → MySQL-এর ওপেন সোর্স ভাই, ফ্রি ফিচার বেশি।
* **SQLite** → ছোট ডেটাবেস, অফলাইন স্টোরেজে হালকা অ্যাপের জন্য পারফেক্ট।

---

## **2. ACID Properties ডিটেইলস**

**ACID** মানে — **Atomicity, Consistency, Isolation, Durability**।
এগুলো RDBMS-এর ডেটা সুরক্ষিত ও নির্ভুল রাখার জন্য বেসিক নীতিমালা।

---

### **A – Atomicity**

> *"সব বা কিছুই না"* — একটি Transaction (যেমন Bank Transfer) যদি আংশিকভাবে ব্যর্থ হয়, তাহলে পুরো Transaction রোলব্যাক হয়।

* **Example:** তুমি ব্যাংকে 500 টাকা পাঠাচ্ছো।

  1. তোমার অ্যাকাউন্ট থেকে 500 টাকা কাটা হবে।
  2. রিসিভারের অ্যাকাউন্টে 500 টাকা যোগ হবে।
     যদি দ্বিতীয় ধাপে সমস্যা হয়, প্রথম ধাপও বাতিল হয়ে যাবে।
* **Why important?** আংশিক ডেটা আপডেট হলে ডেটা করাপশন হতে পারে।

---

### **C – Consistency**

> *"ডেটা সবসময় বৈধ থাকবে"* — Transaction শেষে ডেটাবেস সবসময় সঠিক ও ভ্যালিড স্টেটে থাকবে।

* **Example:** যদি Rule থাকে "Balance কখনো Negative হবে না", তাহলে Transaction শেষে এই Rule ভাঙা যাবে না।
* **Why important?** ভুল ডেটা সিস্টেমে ঢুকলে পুরো সিস্টেম ভেঙে পড়তে পারে।

---

### **I – Isolation**

> *"একাধিক Transaction একে অপরকে প্রভাবিত করবে না"* — একসাথে হাজারো Transaction হলেও তারা আলাদা আলাদা ভাবে চলবে।

* **Example:**

  * ইউজার A টাকা পাঠাচ্ছে
  * ইউজার B টাকা তুলছে
    — একই সময়ে হলেও তারা একে অপরের ডেটা দেখবে না যতক্ষণ না তাদের Transaction সম্পন্ন হয়।
* **Why important?** কনকারেন্ট প্রসেসে ভুল ফলাফল এড়ানো যায়।

---

### **D – Durability**

> *"Transaction কমপ্লিট হলে ডেটা কখনো হারাবে না"* — সার্ভার ক্র্যাশ হলেও ডেটা টিকে থাকবে।

* **Example:** টাকা পাঠানোর পর যদি সার্ভার হঠাৎ বন্ধ হয়, Transaction ইতিমধ্যে Complete হলে ডেটা হারাবে না।
* **Why important?** ডেটা লস হলে Business Trust নষ্ট হয়ে যাবে।

---

### **বাস্তব জীবনের মিল**

* **MySQL** → ACID মেনে চলে, কিন্তু কিছু Storage Engine (যেমন MyISAM) পুরোপুরি ACID না, তাই `InnoDB` ব্যবহার করতে হয়।
* **PostgreSQL** → ডিফল্টভাবেই Full ACID, বড় এবং জটিল Transaction-এ নির্ভুল।
* **Oracle / SQL Server** → Enterprise Grade ACID, খুব বড় Transaction হ্যান্ডেল করতে পারে।
* **SQLite** → ACID মেনে চলে কিন্তু Lightweight, তাই Concurrent Transaction-এ সীমাবদ্ধতা আছে।
* **MariaDB** → MySQL-এর মতোই ACID মেনে চলে, কিন্তু কিছু অতিরিক্ত ফিচার আছে।


---

## NoSQL Protocol মেনে চলে কারা?

NoSQL মানে “Not Only SQL” — এখানে ডেটা টেবিল আকারে না হয়ে **JSON-like documents, key-value pairs, wide-column stores, বা graph-based** হতে পারে।
এগুলো **fixed schema** ফলো করে না এবং **horizontal scalability** তে বেশি ভালো।

**জনপ্রিয় NoSQL প্ল্যাটফর্মগুলো হলো:**

* **MongoDB** (Document Store)
* **Cassandra** (Wide-Column Store)
* **Redis** (Key-Value Store)
* **Neo4j** (Graph Database)
* **Couchbase**
* **DynamoDB** (AWS)

**তারা যা মেনে চলে:**

* **Flexible schema** (structure যেকোনো সময় পরিবর্তন করা যায়)।
* **High scalability** (distributed systems এ millions of users handle করতে পারে)।
* Mostly **BASE properties** (Basically Available, Soft state, Eventually consistent) — consistency কম rigid হয়।

---

## RDBMS বনাম NoSQL — মূল পার্থক্য

| ফিচার               | RDBMS                                  | NoSQL                                       |
| ------------------- | -------------------------------------- | ------------------------------------------- |
| **ডেটা স্ট্রাকচার** | টেবিল আকারে                            | JSON, Key-Value, Graph, Wide Column         |
| **Schema**          | Fixed Schema                           | Flexible Schema                             |
| **Query Language**  | SQL                                    | Varies (Mongo Query Language, CQL, ইত্যাদি) |
| **Scalability**     | Vertical scaling (একটা সার্ভার বড় করা) | Horizontal scaling (অনেক সার্ভারে ভাগ করা)  |
| **Consistency**     | Strong Consistency (ACID)              | Eventual Consistency (BASE)                 |
| **Use case**        | Structured data                        | Unstructured / Semi-structured data         |

---

## কবে কোনটা ব্যবহার করব? (Real-Life Examples সহ)

### **RDBMS ব্যবহার করব যখন**

* ডেটা খুব **structured** এবং ফিক্সড রিলেশনশিপ আছে।
* ডেটার consistency সবসময় ঠিক রাখতে হবে।
* Complex queries, joins, এবং reports দরকার।

**উদাহরণ:**

1. **Banking System** — টাকা ট্রান্সফারের সময় consistency খুব দরকার (MySQL, Oracle)।
2. **University Database** — স্টুডেন্ট, কোর্স, রেজাল্ট সব টেবিল আকারে রিলেশন সহ রাখতে হবে।
3. **E-commerce Inventory** — stock, order, customer info relational ভাবে ম্যানেজ করতে।

---

### **NoSQL ব্যবহার করব যখন**

* ডেটা **semi-structured বা unstructured** (যেমন JSON)।
* ডেটার ফরম্যাট দ্রুত পরিবর্তন হতে পারে।
* ডেটা অনেক বড় এবং millions of concurrent users handle করতে হবে।

**উদাহরণ:**

1. **Social Media Feed** — প্রতিদিন কোটি কোটি post আসে, structure fix না (MongoDB)।
2. **Real-time Analytics** — বড় ডেটা দ্রুত query করতে হবে (Cassandra)।
3. **Chat Application** — দ্রুত key-value based message storage (Redis)।


