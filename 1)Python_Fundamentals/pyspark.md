---
## 🧱 PHASE 0 — Tiny Prerequisites (before PySpark)

**Goal:** Be comfortable with:

* Basic Python (functions, loops, if, imports)
* Very basic SQL (SELECT, WHERE, GROUP BY)

No PySpark questions here, but it makes later parts easy.

---

## 🔵 PHASE 1 — Big Picture: What is PySpark & Spark?

**Goal:** Understand **what PySpark is**, why it exists, and where it’s used.

### 1.1 Big Data & Spark

Learn:

* **What is Apache Spark?**

  * A distributed computing engine for processing large datasets.
* **What is a cluster?**

  * Group of machines (nodes) working together.
* **Where does PySpark fit?**

  * PySpark = **Python API for Spark**.

🔗 **Questions covered:**

1. What is PySpark?
2. Why do we use PySpark instead of normal Python?
3. Difference between Pandas and PySpark?
4. What is Apache Spark? (very short)
5. What is a cluster in Spark?
6. What are the main advantages of using PySpark?
7. How does PySpark differ from Apache Spark?
8. What are RDDs and how do they differ from DataFrames? (just conceptual)
9. What is the difference between RDD, DataFrame and Dataset? (high level, no depth)

🧠 **Core idea:**

* Pandas → small data, one machine
* PySpark → big data, many machines, with Spark engine

You can remember: **“Pandas in laptop, PySpark in cluster.”**

---

## 🔵 PHASE 2 — SparkSession (Entry Point)

**Goal:** Understand and create `SparkSession`. Without this, nothing works.

### 2.1 What is SparkSession?

* SparkSession is the **main object** in PySpark.
* You use it to:

  * Read files
  * Create DataFrames
  * Run SQL

```python
from pyspark.sql import SparkSession

spark = (
    SparkSession
    .builder
    .appName("demo_app")
    .getOrCreate()
)
```

🔗 **Questions covered:**
10. What is SparkSession?
11. Why do we need SparkSession?
12. How do you create a SparkSession?
13. Describe different ways to read data into PySpark. (You’ll expand in next phases.)

---

## 🔵 PHASE 3 — DataFrames: Your Main Weapon

**Goal:** Be fully comfortable with PySpark **DataFrames**.

### 3.1 What is a DataFrame?

Learn:

* DataFrame = **table-like structure** (rows & columns), distributed.
* Similar to SQL table or Pandas DataFrame, but handled by Spark.

🔗 **Questions:**
14. What is a DataFrame in PySpark?
15. How is a DataFrame different from a SQL table?

### 3.2 Reading a CSV

Use:

```python
df = spark.read.csv(
    "data.csv",
    header=True,
    inferSchema=True
)
```

Understand:

* `header=True` → first row is column names
* `inferSchema=True` → Spark auto-detects types

🔗 **Questions:**
16. How do you read a CSV file in PySpark?
17. What do `header=True` and `inferSchema=True` mean?

### 3.3 Inspecting Data

Use:

```python
df.show()          # first 20 rows
df.printSchema()   # structure and data types
```

🔗 **Questions:**
18. How to view data in a DataFrame? (`show()`)
19. How to check schema of a DataFrame? (`printSchema()`)

### 3.4 Selecting & Filtering

```python
df.select("name", "age").show()
df.filter(df.age > 25).show()
```

🔗 **Questions:**
20. How to select columns in PySpark?
21. How to filter rows in PySpark?
22. What methods can be used for filtering in PySpark DataFrames?

### 3.5 Grouping, WithColumn, Missing Data & Misc

```python
from pyspark.sql import functions as F

df.groupBy("department").agg(F.avg("salary")).show()
df2 = df.withColumn("bonus", df.salary * 0.1)
df_clean = df.dropna()
df_filled = df.fillna({"age": 0})
df_sorted = df.orderBy("salary")
df_distinct = df.select("department").distinct()
```

🔗 **Questions:**
23. Explain the use of `groupBy` and `agg` functions in PySpark.
24. What is the use of `withColumn` function?
25. How do you handle missing data in PySpark?
26. What is the difference between `union` and `unionByName` in PySpark? (Just know: `unionByName` matches columns by name.)
27. How can you sort or order data in a DataFrame?
28. Describe the `distinct` function and its use cases.

### 3.6 UDFs & Pandas ⇄ PySpark Conversion (Just Basics)

Concept only:

* UDF = **User Defined Function**, when built-in functions aren’t enough.
* Conversion:

```python
pandas_df = df.toPandas()
spark_df = spark.createDataFrame(pandas_df)
```

🔗 **Questions:**
29. What is a UDF in PySpark, and how do you use it? (High-level understanding)
30. How can you convert a Pandas DataFrame to a PySpark DataFrame and vice versa?
24. What are the differences between PySpark and pandas? (Reinforces Pandas vs PySpark)

---

## 🔵 PHASE 4 — Transformations vs Actions

**Goal:** Understand **lazy evaluation** and how Spark actually runs jobs.

### 4.1 Transformations

* Don’t run immediately.
* Create a **plan**.
* Examples:

```python
df2 = df.select("name", "age")
df3 = df2.filter(df2.age > 25)
df4 = df3.withColumn("double_age", df3.age * 2)
```

### 4.2 Actions

* Trigger execution.
* Examples:

```python
df4.show()
df4.count()
rows = df4.collect()
```

### 4.3 Lazy Evaluation

* Spark waits until an **action** is called.
* Optimizes the full plan at once.

🔗 **Questions:**
31. What is a transformation in PySpark?
32. What is an action in PySpark?
33. Give examples of transformations.
34. Give examples of actions.
35. What is lazy evaluation in PySpark?
36. Why does Spark use lazy evaluation?

---

## 🔵 PHASE 5 — Basic Operations & Aggregations

**Goal:** Do most common business tasks.

### 5.1 Adding New Column

```python
df = df.withColumn("bonus", df.salary * 0.1)
```

### 5.2 Grouping & Aggregations

```python
from pyspark.sql import functions as F

df.groupBy("department").agg(
    F.avg("salary").alias("avg_salary"),
    F.max("salary").alias("max_salary"),
    F.sum("salary").alias("total_salary")
).show()
```

🔗 **Questions:**
37. How do you add a new column using `withColumn`?
38. How do you calculate bonus or percentage column?
39. How do you group data in PySpark? (groupBy + agg)
40. How do you calculate average, sum, max in a group?

---

## 🔵 PHASE 6 — Joins (Very Important)

**Goal:** Understand and code joins between DataFrames.

Assume:

```python
emp(id, name, dept_id, salary)
dept(id, dept_name)
```

### 6.1 Inner Join

```python
emp.join(dept, emp.dept_id == dept.id, "inner")
```

### 6.2 Left / Right / Full

```python
emp.join(dept, emp.dept_id == dept.id, "left")
emp.join(dept, emp.dept_id == dept.id, "right")
emp.join(dept, emp.dept_id == dept.id, "full")
```

🔗 **Questions:**
41. What is a join in PySpark?
42. What are the types of joins in PySpark?
43. How do you perform a join in PySpark?
44. What is a left join? Explain with example.

---

## 🔵 PHASE 7 — Handling NULL Values

**Goal:** Not fail when data is dirty (common in real life).

### 7.1 Dropping NULLs

```python
df2 = df.dropna()                  # any null
# or specific columns
df2 = df.dropna(subset=["age", "salary"])
```

### 7.2 Filling NULLs

```python
df2 = df.fillna({"age": 0, "salary": 0})
```

### 7.3 Why Important?

* Avoid wrong aggregations
* Avoid errors in joins, calculations, etc.

🔗 **Questions:**
45. How do you drop rows with NULL values? (`dropna`)
46. How do you fill NULL values? (`fillna`)
47. Why is NULL handling important in data processing?

---

## 🔵 PHASE 8 — File Formats & Schema

**Goal:** Know basic file formats & why Parquet is loved.

### 8.1 Supported Formats

PySpark commonly works with:

* CSV
* JSON
* Parquet
* ORC
* (sometimes Avro)

### 8.2 Why Parquet?

* Columnar
* Compressed
* Reads only needed columns

### 8.3 JSON

* Good for nested/hierarchical data.

### 8.4 Schema

* Schema = structure of DataFrame (columns, types).
* Important for consistency, performance, compatibility.

🔗 **Questions:**
48. What file formats does PySpark support?
49. Why is Parquet faster than CSV?
50. What is JSON used for?
51. Which format is best for big data use cases?
52. How do you work with JSON, Parquet, or Avro in PySpark? (concept-level)
53. What is a DataFrame schema and why is it important?

---

## 🔵 PHASE 9 — SQL in PySpark

**Goal:** Run SQL on top of DataFrames.

### 9.1 Creating a Temp View

```python
df.createOrReplaceTempView("emp")
```

### 9.2 Running SQL

```python
result = spark.sql("SELECT name, age FROM emp WHERE age > 30")
result.show()
```

You can:

* Filter with `WHERE`
* Group with `GROUP BY`
* Aggregate with `AVG`, `SUM`, etc.

🔗 **Questions:**
54. How do you create a temporary SQL table in PySpark?
55. How do you run SQL queries using `spark.sql`?
56. How do you filter data using SQL queries in PySpark?
57. How do you select columns using SQL in PySpark?

---

## 🔵 PHASE 10 — Mini ETL Task (Must Be Confident)

**Goal:** Be able to **speak through a tiny ETL pipeline**.

Assume DataFrame:

`df(id, name, age, salary)`

### 10.1 Filter employees age > 30

```python
df2 = df.filter(df.age > 30)
```

### 10.2 Add bonus column

```python
df3 = df2.withColumn("bonus", df2.salary * 0.1)
```

### 10.3 Group by age, get average salary

```python
from pyspark.sql import functions as F

df4 = df3.groupBy("age").agg(F.avg("salary").alias("avg_salary"))
df4.show()
```

### 10.4 Explain ETL Steps (In Words)

* **E (Extract)**: Data read from CSV/Parquet into DataFrame.
* **T (Transform)**:

  * Filter rows where age > 30
  * Add a new column `bonus`
  * Group by age and compute avg salary
* **L (Load)**:

  * Could be written back to a file or used in a report.

🔗 **Questions:**
58. How do you filter employees whose age > 30?
59. How do you add a bonus column = 10% salary?
60. How do you group by age and find average salary?
61. Explain the ETL steps you performed.

---

## 🔵 PHASE 11 — Practical & HR Answers

**Goal:** Have confident, honest answers when they ask about your PySpark experience.

### 11.1 “Have you done any PySpark project?”

You:

> “I don’t have an end-to-end PySpark project yet, but I’ve used PySpark to practice DataFrames, joins, aggregations, simple ETL operations, and SQL queries. My main projects are in Flask + Python + SQL, and I’m actively learning PySpark fundamentals.”

### 11.2 “What parts of PySpark have you practiced?”

You:

> “I’ve practiced reading CSV data into DataFrames, selecting and filtering columns, using withColumn, groupBy + agg, handling NULL values, performing joins, using Parquet files, and running SQL queries through `spark.sql`.”

### 11.3 “Are you comfortable learning PySpark on the job?”

You:

> “Yes. Since PySpark is based on Python and similar to Pandas DataFrame operations, I’m comfortable learning and extending it on the job.”

🔗 **Questions:**
62. Have you done any PySpark project?
63. What parts of PySpark have you practiced so far?
64. Are you comfortable learning PySpark on the job?

---

## ✅ How to Use This Roadmap (Very Practical)

If you want to **study using this roadmap**, do this:

1. **Phase 1 → 3**:

   * Understand what PySpark is.
   * Set up SparkSession.
   * Load a CSV and play with `show()`, `printSchema()`, `select`, `filter`.

2. **Phase 4 → 7**:

   * Practice transformations vs actions.
   * Add columns, groupBy, joins, handle NULLs.

3. **Phase 8 → 9**:

   * Learn file formats and SQL with `createOrReplaceTempView` and `spark.sql`.

4. **Phase 10**:

   * Implement the small ETL task on sample data.
   * Be able to explain it **verbally** like an interviewer is asking.

5. **Phase 11**:

   * Memorize your HR/safe answers.

If you want next, I can:

* Turn **each phase** into a **lesson with code + short answers to the exact questions**, or
* Build a **2–3 day PySpark study plan** using this roadmap.


Alright, welcome to **Phase 1** 😄
We’ll do exactly this:

> **Learn concept → See tiny code (where useful) → See which interview questions it answers → Get a few small practice Qs**

Only **basic level**, no deep architecture, no tuning, no cluster admin stuff.

---

# 🔵 PHASE 1 — Big Picture: What is PySpark & Spark?

🎯 **Goal for this phase:**
By the end, you should be able to confidently explain:

* What is **Spark**?
* What is **PySpark**?
* Why do we need it if we already have Python & Pandas?
* What is a **cluster**?
* What are **RDD, DataFrame, Dataset** (just at bird’s-eye level)?

This is 100% theory + mental model, very light code.

---

## 1️⃣ Step 1 — What problem does PySpark solve?

### 🧠 Concept

First, imagine:

* You have a **small CSV file** with 10,000 rows → Pandas is OK.
* Now imagine a **huge log file** with **200 GB** of data.

Problems with normal Python / Pandas:

* File might not even fit in RAM.
* Processing will be very slow.
* Only **one CPU** is used.

So we need something that can:

* Split the data across **many machines**.
* Use **many CPUs** in parallel.
* Still give us a nice **table-like API** (like DataFrame).

➡️ That “something” is **Apache Spark**.
➡️ And **PySpark** is how we talk to Spark using **Python**.

---

## 2️⃣ Step 2 — What is Apache Spark?

### 🧠 Concept

> **Apache Spark** is a **distributed computing engine** for processing large-scale data.

Key words (you can say this in interview):

* **Distributed** → runs on multiple machines.
* **In-memory** → keeps data in RAM when possible (faster than disk).
* **General-purpose** → supports batch jobs, SQL, streaming, ML, etc.

You don’t need deep architecture. At apprentice level, this is enough:

> “Spark helps us process big data quickly by distributing it across multiple machines.”

---

## 3️⃣ Step 3 — What is a cluster? (Beginner meaning)

### 🧠 Concept

> A **cluster** = a **group of machines** working together as if they are one big machine.

Very simple:

* Each machine → called a **node**.
* One special node controls others (driver/coordinator).
* Other nodes do the actual work (workers).

You don’t need driver/executor details yet. Just say:

> “Spark usually runs on a cluster, which is a group of machines that share the work.”

---

## 4️⃣ Step 4 — Where does PySpark fit?

Now we combine everything.

* **Spark** = big data engine (written in Scala/Java).
* **PySpark** = **Python API** that lets you control Spark from Python code.

Analogy:

* Spark = car engine.
* PySpark = steering wheel written in Python.

So when you run:

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("demo").getOrCreate()
```

You are actually:

* Using **Python** to tell **Spark** what to do.
* Spark internally distributes the work on the cluster.

---

## 5️⃣ Step 5 — Pandas vs PySpark vs “normal Python”

### 🧠 Concept

You can think like this:

| Tool          | Runs on                 | Best for                           |
| ------------- | ----------------------- | ---------------------------------- |
| Normal Python | Single CPU              | Simple scripts, logic              |
| Pandas        | Single machine (RAM)    | Small/medium data (MB–GB)          |
| PySpark       | Many machines (cluster) | Big data (tens/hundreds of GB, TB) |

So:

* If **data size < RAM of your laptop** → Pandas is fine.
* If **data is very large or you want distributed processing** → PySpark.

👉 This gives you a **perfect interview line**:

> “Pandas is good for small data on one machine, PySpark is for big data on a cluster.”

---

## 6️⃣ Step 6 — What are RDD, DataFrame, Dataset? (Only high-level)

We don’t go deep. You just need **conceptual understanding**.

### 🧠 Concept

* **RDD (Resilient Distributed Dataset)**

  * Low-level data structure in Spark.
  * Like a distributed list of objects.
  * More control, but more code.
  * Not usually needed in beginner PySpark for interviews.

* **DataFrame**

  * Table with rows and columns (like SQL or Pandas).
  * Higher-level, optimized, easy to use.
  * This is your **main focus**.

* **Dataset** (mainly in Scala/Java, not used much in Python)

  * Like typed DataFrames (with compile-time type safety).
  * **Not important** for you now as a Python + PySpark candidate.

Best line for interview:

> “In PySpark, we mostly use DataFrames. RDDs are the lower-level API, and Datasets are more common in Scala/Java, not in Python.”

---

## 7️⃣ Tiny Code Glimpse (Just to Visualize)

Even though this is conceptual, let’s see a **very small code snippet** to connect theory:

```python
from pyspark.sql import SparkSession

# 1. Create SparkSession (entry point)
spark = SparkSession.builder.appName("phase1_demo").getOrCreate()

# 2. Read a small CSV into a DataFrame
df = spark.read.csv("employees.csv", header=True, inferSchema=True)

# 3. Show some rows
df.show()

# 4. Print schema
df.printSchema()
```

At this stage you don’t need to run it, just **understand**:

* We’re using **PySpark (Python)** to control **Spark**.
* Spark can run on a **cluster**, even if for local learning it runs on your machine.
* Data is in a **DataFrame**, not RDD.

---

## 8️⃣ Which interview questions does Phase 1 cover?

From our merged list, Phase 1 helps you answer:

1. What is PySpark?
2. Why do we use PySpark instead of normal Python?
3. Difference between Pandas and PySpark?
4. What is Apache Spark? (very short)
5. What is a cluster in Spark?
6. What are the main advantages of using PySpark?
7. How does PySpark differ from Apache Spark?
8. What are RDDs and how do they differ from DataFrames? (just conceptual)
9. What is the difference between RDD, DataFrame and Dataset? (high level)

If you can confidently explain everything we just discussed, you already have **Phase 1 fully covered.**

---

## 9️⃣ Small Practice Section (for you to think/answer)

These are NOT advanced coding questions – just to test your understanding.

### 🧩 Practice Q1 (Concept)

**Q:** Your CSV file is 50 MB and runs fine with Pandas. Should you immediately move to PySpark for it? Why / why not?

*(Think: do you really need a cluster for that?)*

---

### 🧩 Practice Q2 (Concept)

**Q:** Your company has 2 TB of log data stored on a distributed file system. Is it better to use:

* a) normal Python loops
* b) Pandas
* c) PySpark DataFrames

Explain in one or two lines.

---

### 🧩 Practice Q3 (Interview simulation)

**Q (Interviewer):** “In simple words, what is a cluster?”
Try to answer in **one sentence**.

---

### 🧩 Practice Q4 (Difference question)

**Q:** Say one difference between:

* RDD vs DataFrame
* DataFrame vs Dataset

(Only high-level, 1 line each.)

---

### 🧩 Practice Q5 (Tiny code reading)

Look at this code:

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("check").getOrCreate()
df = spark.read.csv("users.csv", header=True, inferSchema=True)
df.show()
```

Answer:

1. Which part is PySpark?
2. Which object represents Spark?
3. What type of thing is `df`?

---
**Phase 1 interview answers + all practice question answers**, written in the **exact style you must speak in interviews**.
---

# ✅ **PHASE 1 — Interview Questions & Perfect Answers**

Below are the answers to the 9 questions covered in Phase 1.

---

## **1️⃣ What is PySpark?**

PySpark is the Python API for Apache Spark. It lets us process large datasets in a distributed way using Python.

---

## **2️⃣ Why do we use PySpark instead of normal Python?**

Normal Python runs on a single machine and processes data slowly, while PySpark distributes data across multiple machines, making it much faster for big data.

---

## **3️⃣ Difference between Pandas and PySpark?**

* Pandas → small data, single machine
* PySpark → big data, many machines (distributed processing)

---

## **4️⃣ What is Apache Spark? (very short)**

Apache Spark is a distributed computing engine used to process large datasets quickly.

---

## **5️⃣ What is a cluster in Spark?**

A cluster is a group of connected machines that work together to process data.

---

## **6️⃣ What are the main advantages of using PySpark?**

* Handles large data efficiently
* Uses multiple machines (distributed)
* Very fast due to in-memory execution
* Easy DataFrame API like Pandas
* Allows SQL, streaming, ML, etc.

---

## **7️⃣ How does PySpark differ from Apache Spark?**

Apache Spark is the engine; PySpark is the Python interface used to work with Spark.

---

## **8️⃣ What are RDDs and how do they differ from DataFrames? (simple)**

RDDs are low-level distributed collections without schema; DataFrames are high-level tables with named columns.

---

## **9️⃣ Difference between RDD, DataFrame, and Dataset? (very high-level)**

* RDD → low-level, unstructured
* DataFrame → high-level, structured
* Dataset → strongly typed DataFrame (not used in Python)

---

# 🧠 **Phase 1 is complete — Now the Practice Question Answers**

---

# 🧩 Practice Q1

**Q:** A CSV file is 50 MB and runs fine in Pandas. Should you move to PySpark?

### ✅ **Answer:**

**No.**
Pandas is enough for 50 MB because it easily fits into memory. You only need PySpark when the data becomes very large (GBs or TBs).

---

# 🧩 Practice Q2

**Q:** Your company has 2 TB logs. Which option is best?

a) Python loops
b) Pandas
c) PySpark DataFrames

### ✅ **Answer:**

**c) PySpark DataFrames**
Because 2 TB is too large for one machine; PySpark can distribute the data across a cluster.

---

# 🧩 Practice Q3

**Q:** “In simple words, what is a cluster?”

### ✅ **Answer:**

A cluster is a group of machines working together to process data faster.

---

# 🧩 Practice Q4

**Q:** One-line differences:

### **RDD vs DataFrame**

RDD → low-level, no schema
DataFrame → table with columns, optimized

### **DataFrame vs Dataset**

DataFrame → dynamic typing
Dataset → strong typing (not used in Python)

---

# 🧩 Practice Q5

### Code:

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("check").getOrCreate()
df = spark.read.csv("users.csv", header=True, inferSchema=True)
df.show()
```

### Q1: Which part is PySpark?

`from pyspark.sql import SparkSession` and all code using `spark` and `df` are PySpark.

### Q2: Which object represents Spark?

`spark` is the SparkSession object that represents Spark.

### Q3: What type of thing is df?

`df` is a **PySpark DataFrame**.

---

# 🎉 **Phase 1 Completed 100%**

You are ready to move to Phase 2.

Say: **“Go to Phase 2”**
and I will start:

Absolutely — here is **PHASE 2**, explained *exactly like Phase 1*:

✔ Learn concept
✔ See small code
✔ Know which interview questions this covers
✔ Do practice questions
✔ Do small coding tasks

Beginner-friendly, no advanced internal architecture.

---

# 🔵 **PHASE 2 — SparkSession (Entry Point of PySpark)**

### 🎯 Phase Goal:

By the end of Phase 2, you should be able to answer:

* What is SparkSession?
* Why is it needed?
* How to create it?
* How to read data using SparkSession?

This phase is *very important* because every PySpark program starts with SparkSession.

---

# 2.1 **What is SparkSession?**

### 🧠 Concept (beginner level)

> **SparkSession is the main entry point to PySpark.**
> It is like the “controller” or “brain” of your PySpark program.

You need it for:

* Reading files (`read`)
* Creating DataFrames
* Running SQL queries (`spark.sql`)
* Configuring the app (name, settings)
* Connecting to the cluster (internally)

Think of it as:

🟦 **PySpark → SparkSession → Everything happens through this**

Just like:

* Flask → `app`
* PySpark → `spark`

---

# 2.2 **Why do we need SparkSession?**

### 🧠 Simple explanation:

Without SparkSession:

❌ You cannot read files.
❌ You cannot create DataFrames.
❌ You cannot run SQL queries.
❌ PySpark cannot talk to the Spark engine.

So the rule is:

> **No SparkSession = No PySpark program.**

---

# 2.3 **How to Create SparkSession? (Must memorize)**

This is the **exact** code the interviewer expects you to know:

```python
from pyspark.sql import SparkSession

spark = (
    SparkSession
    .builder
    .appName("demo_app")
    .getOrCreate()
)
```

### 🔍 Break it down:

* `SparkSession.builder` → start building a SparkSession
* `.appName("demo_app")` → name your app
* `.getOrCreate()` → create new one or reuse existing

### 🧠 Interview trick:

If they ask:

> “What does getOrCreate() do?”

You say:

> “It creates a SparkSession if it doesn’t exist, otherwise returns the existing one.”

---

# 2.4 **How do we read data using SparkSession?**

SparkSession gives you `spark.read`

```python
df = spark.read.csv("data.csv", header=True, inferSchema=True)
```

Later, you will use:

* `spark.read.json()`
* `spark.read.parquet()`
* `spark.read.format()`

But for now, CSV is enough.

---

# 🔗 **Interview Questions Covered in Phase 2**

10. What is SparkSession?
11. Why do we need SparkSession?
12. How do you create a SparkSession?
13. Describe different ways to read data into PySpark.

And an extra one they sometimes ask:

❓ **What does getOrCreate() do?**

✔ You already learned that.

---

# 📘 **Mini Code Example (Beginner-friendly)**

Just to visualize everything:

```python
from pyspark.sql import SparkSession

# 1. Create SparkSession
spark = SparkSession.builder.appName("example").getOrCreate()

# 2. Read CSV file
df = spark.read.csv("employees.csv", header=True, inferSchema=True)

# 3. Show first rows
df.show()
```

That’s it. No complexity.

---

# 🧩 PRACTICE QUESTIONS (For Understanding)

### **Q1:**

What is SparkSession in PySpark?
(Give a 1-line interview answer.)

---

### **Q2:**

Why do we write `.getOrCreate()` at the end of SparkSession?

---

### **Q3:**

Which object is responsible for reading files in PySpark?

* a) pandas
* b) spark
* c) df
* d) SQLContext

---

### **Q4:**

Write the code to create a SparkSession named “test_app”.

*(Write exact 3 lines.)*

---

### **Q5:**

Why do we need SparkSession before reading a CSV file?

---

# 🧪 PRACTICE CODING TASK (Very Simple)

**Task:**
Write PySpark code to:

1. Create a SparkSession named “practice_session”
2. Read a file called `students.csv`
3. Print first 20 rows
4. Print the schema

---
Perfect — here are the **Phase 2 interview answers + practice question answers**, written exactly in interview-perfect format.

---

# ✅ **PHASE 2 — Interview Questions & Perfect Answers**

These are the answers to the 4 official interview questions covered in Phase 2.

---

## **10. What is SparkSession?**

SparkSession is the entry point to any PySpark application.
We use it to create DataFrames, read files, and run SQL queries.

---

## **11. Why do we need SparkSession?**

Because without SparkSession, PySpark cannot connect to the Spark engine.
It is required for reading data, creating DataFrames, and executing Spark operations.

---

## **12. How do you create a SparkSession?**

This is the exact syntax:

```python
from pyspark.sql import SparkSession

spark = (
    SparkSession
    .builder
    .appName("demo_app")
    .getOrCreate()
)
```

---

## **13. Describe different ways to read data into PySpark.**

We use `spark.read` to load data:

* `spark.read.csv("file.csv")`
* `spark.read.json("file.json")`
* `spark.read.parquet("file.parquet")`
* `spark.read.format("csv").load(path)`

For beginners, CSV is enough.

---

## ⭐ Bonus Mini-Question (often asked)

**Q: What does getOrCreate() do?**
It creates a new SparkSession if one doesn't exist; otherwise it returns the existing one.

---

# 🧩 **Practice Question Answers**

These test your understanding and help you speak confidently.

---

## **Practice Q1:**

**Q:** What is SparkSession in PySpark?
**A:**
SparkSession is the main object in PySpark that allows us to read data, create DataFrames, and run SQL queries.

---

## **Practice Q2:**

**Q:** Why do we use `.getOrCreate()`?
**A:**
Because it either creates a new SparkSession or returns the existing one. This prevents duplicate sessions.

---

## **Practice Q3:**

**Q:** Which object reads files in PySpark?

Options:
a) pandas
b) spark
c) df
d) SQLContext

**Correct Answer:** **b) spark**
Because `spark.read` is used to load data into DataFrames.

---

## **Practice Q4:**

**Q:** Write the code to create a SparkSession named “test_app”.

### ✅ Answer:

```python
from pyspark.sql import SparkSession

spark = (
    SparkSession
    .builder
    .appName("test_app")
    .getOrCreate()
)
```

---

## **Practice Q5:**

**Q:** Why do we need SparkSession before reading a CSV file?
**A:**
Because SparkSession gives us the `spark.read` interface.
Without SparkSession, PySpark cannot load files or create DataFrames.

---

# 🧪 Practice Coding Task — SOLUTION

**Task:** Create SparkSession → Read CSV → show rows → print schema

### ✅ Solution:

```python
from pyspark.sql import SparkSession

# 1. Create SparkSession
spark = (
    SparkSession
    .builder
    .appName("practice_session")
    .getOrCreate()
)

# 2. Read CSV
df = spark.read.csv("students.csv", header=True, inferSchema=True)

# 3. Show first rows
df.show()

# 4. Print schema
df.printSchema()
```

---

# 🎉 Phase 2 is 100% complete.
Perfect — here is **PHASE 3 explained exactly like Phase 1 & Phase 2**, including:

✔ Concept
✔ Mini-code
✔ Interview answers (for ALL 17 questions in this phase)
✔ Practice questions
✔ Small coding tasks

No advanced topics, only beginner-level DataFrame skills.

---

# 🔵 **PHASE 3 — DataFrames: Your Main Weapon**

DataFrames are **the MOST important** part of PySpark for your apprenticeship round.
If you master Phase 3 + joins + SQL → you already look experienced.

Let’s walk step-by-step.

---

# ✅ **3.1 What is a DataFrame?**

### 🧠 Concept

A **PySpark DataFrame** is:

* A **distributed table** with rows & columns
* Similar to:

  * SQL table
  * Pandas DataFrame
* But stored & processed **in parallel on multiple machines**

You can think:

> “DataFrame = a table spread across many computers.”

### 💬 Interview Questions & Answers

### **Q14. What is a DataFrame in PySpark?**

A DataFrame is a distributed collection of data organized into named columns, similar to a SQL table or Pandas DataFrame.

---

### **Q15. How is a DataFrame different from a SQL table?**

A DataFrame is an in-memory distributed table processed by Spark, whereas a SQL table is stored in a database.

---

# ✅ **3.2 Reading a CSV File**

### 🧠 Concept

Syntax:

```python
df = spark.read.csv(
    "data.csv",
    header=True,
    inferSchema=True
)
```

### Important parameters:

* **header=True**
  Means first row of the CSV contains column names.

* **inferSchema=True**
  Spark automatically detects correct data types
  (e.g., age → integer, salary → double)

### 💬 Interview Questions & Answers

### **Q16. How do you read a CSV file in PySpark?**

```python
df = spark.read.csv("file.csv", header=True, inferSchema=True)
```

---

### **Q17. What do header=True and inferSchema=True mean?**

* `header=True` → first row contains column names
* `inferSchema=True` → Spark automatically detects data types

---

# ✅ **3.3 Inspecting Data**

### 🧠 Concept

These two commands are mandatory:

```python
df.show()        # prints first 20 rows
df.printSchema() # prints column names & data types
```

### 💬 Interview Questions & Answers

### **Q18. How to view data in a DataFrame?**

Use:

```python
df.show()
```

---

### **Q19. How to check schema of a DataFrame?**

Use:

```python
df.printSchema()
```

---

# ✅ **3.4 Selecting & Filtering Columns**

### 🧠 Concept

```python
df.select("name", "age").show()
df.filter(df.age > 25).show()
```

### 💬 Interview Questions & Answers

### **Q20. How to select columns in PySpark?**

```python
df.select("column1", "column2")
```

---

### **Q21. How to filter rows in PySpark?**

```python
df.filter(df.age > 25)
```

---

### **Q22. What methods can be used for filtering in PySpark?**

* `filter()`
* `where()`

---

# ✅ **3.5 Grouping, WithColumn, Missing Data & Misc Operations**

### 🧠 Concept + Code

```python
from pyspark.sql import functions as F

# Grouping
df.groupBy("department").agg(F.avg("salary")).show()

# Add a new column
df2 = df.withColumn("bonus", df.salary * 0.1)

# Drop nulls
df_clean = df.dropna()

# Fill nulls
df_filled = df.fillna({"age": 0})

# Sort
df_sorted = df.orderBy("salary")

# Unique values
df_distinct = df.select("department").distinct()
```

---

### 💬 Interview Questions & Answers

### **Q23. Explain groupBy & agg functions.**

They are used to group rows by a column and apply aggregations such as avg, sum, max, min, count.

---

### **Q24. What is the use of withColumn()?**

It is used to add a new column or update an existing column.

---

### **Q25. How do you handle missing data in PySpark?**

* Remove missing values → `dropna()`
* Replace missing values → `fillna()`

---

### **Q26. Difference between union and unionByName?**

`union()` → matches columns by position
`unionByName()` → matches columns by name

---

### **Q27. How can you sort or order data in a DataFrame?**

```python
df.orderBy("salary")
```

---

### **Q28. What does distinct() do?**

It returns unique values from a column or DataFrame.

---

# ✅ **3.6 UDFs & Pandas ⇄ PySpark Conversion**

### 🧠 Concept

A **UDF (User Defined Function)** allows custom Python functions to run on DataFrame columns.

*(Beginner level: just know what it is. No need to write UDF code yet.)*

### **Conversion**

```python
pandas_df = df.toPandas()
spark_df = spark.createDataFrame(pandas_df)
```

---

### 💬 Interview Questions & Answers

### **Q29. What is a UDF in PySpark?**

A UDF is a User Defined Function that allows you to apply custom Python logic to PySpark columns.

---

### **Q30. How can you convert Pandas DataFrame to PySpark and vice versa?**

```python
# PySpark → Pandas
pandas_df = df.toPandas()

# Pandas → PySpark
spark_df = spark.createDataFrame(pandas_df)
```

---

### **Extra: What are differences between Pandas & PySpark?**

* Pandas → single machine
* PySpark → distributed
* Pandas → eager
* PySpark → lazy

---

# 🎉 **PHASE 3 — ALL INTERVIEW ANSWERS DONE**

Now let’s test your understanding.

---

# 🧩 PHASE 3 — PRACTICE QUESTIONS (Answer These)

### **Q1:** What is a DataFrame in PySpark?

---

### **Q2:** What do header=True and inferSchema=True mean?

---

### **Q3:** Write a command to select only “name” and “salary” columns.

---

### **Q4:** Write a command to filter employees whose age > 40.

---

### **Q5:** How do you add a new column “bonus = salary * 0.05”?

---

### **Q6:** How do you drop rows with NULLs?

---

### **Q7:** What is the difference between union and unionByName?

---

### **Q8:** How do you get unique department names from a DataFrame?

---

# 🧪 Coding Practice Task

Use PySpark to:

1. Read `employees.csv`
2. Select only: name, age, department
3. Add a column: `tax = salary * 0.1`
4. Filter: age > 25
5. Group by department and show avg salary

---
Absolutely — here are the **perfect, beginner-friendly, interview-ready answers for all Phase 3 questions**, PLUS the **practice question answers** and the **coding task solution**.

I will follow the exact format used in Phase 1 and Phase 2.

---

# ✅ **PHASE 3 — Interview Questions & Perfect Answers**

Below are the answers to **all 17 DataFrame questions** from Phase 3.

---

# 🔵 **3.1 — What is a DataFrame?**

### **Q14. What is a DataFrame in PySpark?**

A DataFrame is a distributed table with rows and columns, similar to a SQL table or Pandas DataFrame, but processed in parallel by Spark.

---

### **Q15. How is a DataFrame different from a SQL table?**

A DataFrame is stored in memory and processed by Spark across multiple machines, while a SQL table is stored in a database system.

---

# 🔵 **3.2 — Reading a CSV**

### **Q16. How do you read a CSV file in PySpark?**

```python
df = spark.read.csv("file.csv", header=True, inferSchema=True)
```

---

### **Q17. What do header=True and inferSchema=True mean?**

* `header=True` → The first row contains column names.
* `inferSchema=True` → Spark automatically detects correct data types.

---

# 🔵 **3.3 — Inspecting Data**

### **Q18. How do you view data in a DataFrame?**

Use:

```python
df.show()
```

---

### **Q19. How do you check the schema of a DataFrame?**

Use:

```python
df.printSchema()
```

---

# 🔵 **3.4 — Selecting & Filtering**

### **Q20. How do you select columns in PySpark?**

```python
df.select("name", "age")
```

---

### **Q21. How do you filter rows in PySpark?**

```python
df.filter(df.age > 25)
```

---

### **Q22. What methods can be used for filtering?**

* `filter()`
* `where()`

Both work the same.

---

# 🔵 **3.5 — Grouping, WithColumn, Missing Data & Misc**

### **Q23. Explain the use of groupBy and agg.**

`groupBy` groups rows by a column, and `agg` applies aggregations like avg, sum, max, min.

---

### **Q24. What is the use of withColumn()?**

Used to create a new column or update an existing column.

---

### **Q25. How do you handle missing data in PySpark?**

* `dropna()` → remove rows with NULLs
* `fillna()` → replace NULL values with defaults

---

### **Q26. Difference between union and unionByName?**

* `union()` → matches columns by position
* `unionByName()` → matches columns by column name

---

### **Q27. How can you sort or order data in a DataFrame?**

```python
df.orderBy("salary")
```

---

### **Q28. What does distinct() do?**

Returns unique values of a column or unique rows of the DataFrame.

---

# 🔵 **3.6 — UDFs & Pandas Conversion**

### **Q29. What is a UDF in PySpark?**

A UDF (User Defined Function) lets you apply custom Python logic on DataFrame columns.

---

### **Q30. How can you convert a Pandas DataFrame to PySpark and vice versa?**

```python
# PySpark → Pandas
pandas_df = df.toPandas()

# Pandas → PySpark
spark_df = spark.createDataFrame(pandas_df)
```

---

### **Q24 (duplicate from earlier): Differences between PySpark and Pandas?**

* PySpark → distributed, lazy evaluation, big data
* Pandas → single machine, eager evaluation, small data

---

# 🎉 **PHASE 3 — ALL INTERVIEW ANSWERS COMPLETED**

Now practice time.

---

# 🧩 **PHASE 3 — PRACTICE QUESTION ANSWERS**

Here are the answers to the practice questions you were supposed to think about.

---

### **Q1: What is a DataFrame in PySpark?**

A distributed table with rows and columns, processed by Spark across multiple machines.

---

### **Q2: What do header=True and inferSchema=True mean?**

* `header=True` → first row is column names
* `inferSchema=True` → Spark auto-detects data types

---

### **Q3: Write a command to select only “name” and “salary” columns.**

```python
df.select("name", "salary")
```

---

### **Q4: Write a command to filter employees whose age > 40.**

```python
df.filter(df.age > 40)
```

---

### **Q5: How do you add a new column “bonus = salary * 0.05”?**

```python
df.withColumn("bonus", df.salary * 0.05)
```

---

### **Q6: How do you drop rows with NULLs?**

```python
df.dropna()
```

---

### **Q7: Difference between union and unionByName?**

* `union()` → matches columns by position
* `unionByName()` → matches by column names

---

### **Q8: How do you get unique department names?**

```python
df.select("department").distinct()
```

---

# 🧪 **PHASE 3 — Coding Task Solution**

**Task:**

1. Read `employees.csv`
2. Select: name, age, department
3. Add column: tax = salary * 0.1
4. Filter: age > 25
5. Group by department and show average salary

### ✅ **Solution**

```python
from pyspark.sql import SparkSession
from pyspark.sql import functions as F

# 1. Create SparkSession
spark = SparkSession.builder.appName("phase3_task").getOrCreate()

# 2. Read CSV
df = spark.read.csv("employees.csv", header=True, inferSchema=True)

# 3. Select needed columns
df_sel = df.select("name", "age", "department", "salary")

# 4. Add tax column
df_tax = df_sel.withColumn("tax", df_sel.salary * 0.1)

# 5. Filter age > 25
df_filt = df_tax.filter(df_tax.age > 25)

# 6. Group by department → avg salary
df_group = df_filt.groupBy("department").agg(F.avg("salary").alias("avg_salary"))

df_group.show()
```

---

# 🎉 **PHASE 3 is 100% complete**

Below is **PHASE 4 taught EXACTLY like Phase 1, 2, 3**:

✔ Concept explained simply
✔ Code examples
✔ Interview answers for all questions
✔ Practice questions
✔ Mini coding test

Absolutely beginner-friendly, zero advanced content.

---

# 🔵 **PHASE 4 — Transformations vs Actions**

## 🎯 **Goal:**

Understand **how Spark thinks**, **how jobs run**, and **why lazy evaluation makes Spark fast**.

This phase is *small but extremely important* — interviewers always ask about this.

---

# ✅ **4.1 What are Transformations? (Very Important)**

### 🧠 Concept

Transformations:

✔ Do **NOT** execute immediately
✔ Only **prepare** the steps
✔ Creates a **logical plan** in Spark
✔ Execution happens later when an action is called

Think of transformations like:

> “Writing cooking steps but not actually cooking yet.”

---

### 🧪 Example

```python
df2 = df.select("name", "age")
df3 = df2.filter(df2.age > 25)
df4 = df3.withColumn("double_age", df3.age * 2)
```

None of the above **runs immediately**.

Spark is just building a plan.

---

# ✨ **4.2 What are Actions?**

### 🧠 Concept

Actions:

✔ **Trigger the real execution**
✔ Force Spark to compute results
✔ Return output to driver or print results

Think:

> “Now start cooking — execute all steps.”

---

### 🧪 Example

```python
df4.show()        # executes full pipeline
df4.count()       # counts rows
rows = df4.collect()  # brings all rows to driver
```

---

# 🔥 **4.3 Lazy Evaluation (Most Important Concept)**

### 🧠 Concept

Lazy evaluation means:

✔ Transformations do NOT execute immediately
✔ Spark waits until an **action** is called
✔ Then Spark optimizes everything using **Catalyst Optimizer**
✔ This makes Spark **much faster**

---

### 🧠 Beginner Explanation

Spark does this for speed:

> “Don’t run step-by-step.
> Wait until the last moment, optimize everything, then run once.”

---

# 🔗 **INTERVIEW QUESTIONS & PERFECT ANSWERS**

Below are the answers for all questions in this phase.

---

### **Q31. What is a transformation in PySpark?**

A transformation is an operation that creates a new DataFrame without executing immediately.

Examples:
`select()`, `filter()`, `withColumn()`, `groupBy()`

---

### **Q32. What is an action in PySpark?**

An action is an operation that triggers execution of the entire plan.

Examples:
`show()`, `count()`, `collect()`

---

### **Q33. Give examples of transformations.**

* `select()`
* `filter()`
* `groupBy()`
* `withColumn()`
* `orderBy()`
* `dropna()`

---

### **Q34. Give examples of actions.**

* `show()`
* `collect()`
* `count()`
* `take()`
* `head()`

---

### **Q35. What is lazy evaluation in PySpark?**

Transformations don’t run immediately.
Spark waits until an action is called to execute the full plan.

---

### **Q36. Why does Spark use lazy evaluation?**

Because it:

✔ Optimizes the job
✔ Reduces unnecessary computation
✔ Makes big data processing faster

---

# 🧩 **PHASE 4 — PRACTICE QUESTIONS**

Try answering these before checking the solutions.

---

### **Q1. Is select() a transformation or action? Why?**

---

### **Q2. When does a filter() actually run?**

---

### **Q3. What happens if you write transformations but never call show()?**

---

### **Q4. Write one transformation and one action.**

---

### **Q5. Explain lazy evaluation in 1 line.**

---

### **Q6. Which line triggers execution?**

```python
df2 = df.filter(df.age > 20)
df3 = df2.withColumn("tax", df.salary * 0.1)
df4 = df3.groupBy("department")
df4.show()
```

---

# 🧪 **PHASE 4 — CODE PRACTICE**

### **Task: Identify transformations vs actions**

```python
df2 = df.select("name", "age")
df3 = df2.filter(df2.age > 30)
df4 = df3.withColumn("bonus", df3.salary * 0.2)
total = df4.count()
df4.show()
```

Questions:

1. Which lines are transformations?
2. Which lines are actions?
3. Which line triggers actual execution?

---

# 🎉 **PHASE 4 Completed**

Once you answer the practice questions, say:
Here are the **perfect beginner-friendly answers** for all **Phase 4 practice questions + code identification questions.**
These are the exact answers interviewers expect.

---

# ✅ **PHASE 4 — PRACTICE QUESTION ANSWERS**

---

### **Q1. Is select() a transformation or action? Why?**

**Answer:**
`select()` is a **transformation** because it creates a new DataFrame but does NOT trigger execution.

---

### **Q2. When does a filter() actually run?**

**Answer:**
`filter()` runs only when an **action** (like `show()` or `count()`) is called.

---

### **Q3. What happens if you write transformations but never call show()?**

**Answer:**
Nothing gets executed.
Spark only builds a plan; it doesn’t run any computation until an action is triggered.

---

### **Q4. Write one transformation and one action.**

**Transformation:**

```python
df2 = df.filter(df.age > 30)
```

**Action:**

```python
df2.count()
```

---

### **Q5. Explain lazy evaluation in 1 line.**

**Answer:**
Lazy evaluation means Spark waits for an **action** to run all transformations together efficiently.

---

### **Q6. Which line triggers execution?**

```python
df2 = df.filter(df.age > 20)
df3 = df2.withColumn("tax", df.salary * 0.1)
df4 = df3.groupBy("department")
df4.show()
```

**Answer:**
`df4.show()` is the **action** → it triggers execution of *all previous transformations*.

---

# 🧪 **PHASE 4 — CODE PRACTICE ANSWERS**

Given code:

```python
df2 = df.select("name", "age")
df3 = df2.filter(df2.age > 30)
df4 = df3.withColumn("bonus", df3.salary * 0.2)
total = df4.count()
df4.show()
```

---

## **1. Which lines are transformations?**

✔ `df2 = df.select("name", "age")`
✔ `df3 = df2.filter(df2.age > 30)`
✔ `df4 = df3.withColumn("bonus", df3.salary * 0.2)`

---

## **2. Which lines are actions?**

✔ `total = df4.count()`
✔ `df4.show()`

---

## **3. Which line triggers actual execution?**

**Answer:**
Both:

* `df4.count()`
* `df4.show()`

trigger execution (each action separately runs the entire plan).

---

# 🎉 **PHASE 4 completed 100%**

Great — here is **PHASE 5 explained exactly like previous phases**, including:

✔ Simple explanation
✔ Code
✔ Interview answers
✔ Practice questions
✔ Small coding task

No advanced content — fully beginner/interview-level only.

---

# 🔵 **PHASE 5 — Basic Operations & Aggregations**

## 🎯 **Goal:**

Learn the most common real-world DataFrame operations you’ll definitely face in interviews & assignments.

These operations are ALWAYS asked in practical rounds.

---

# ✅ **5.1 Adding New Column (withColumn)**

### 🧠 Concept

`withColumn()` is used to:

✔ Add a new column
✔ Modify an existing column

### 🧪 Example: Add bonus = 10% of salary

```python
df = df.withColumn("bonus", df.salary * 0.1)
```

This creates a new column **bonus** for every row.

---

# 🔗 **Interview Question & Answer**

### **Q37. How do you add a new column using withColumn?**

Using `withColumn("new_column", expression)`.

Example:

```python
df.withColumn("bonus", df.salary * 0.1)
```

---

### **Q38. How do you calculate a bonus or percentage column?**

**Answer:**

```python
df.withColumn("bonus", df.salary * 0.1)
```

OR for percentage:

```python
df.withColumn("tax", df.salary * 0.05)
```

---

# ✅ **5.2 Grouping & Aggregations (Most Asked)**

### 🧠 Concept

You can group rows by a column and apply aggregations like:

* avg
* sum
* max
* min
* count

### 🧪 Example:

```python
from pyspark.sql import functions as F

df.groupBy("department").agg(
    F.avg("salary").alias("avg_salary"),
    F.max("salary").alias("max_salary"),
    F.sum("salary").alias("total_salary")
).show()
```

---

# 🔗 **Interview Questions & Answers**

### **Q39. How do you group data in PySpark?**

Using `groupBy()` and `agg()`:

```python
df.groupBy("department").agg(F.avg("salary"))
```

---

### **Q40. How do you calculate average, sum, max in a group?**

```python
df.groupBy("department").agg(
    F.avg("salary"),
    F.sum("salary"),
    F.max("salary")
)
```

---

# 🎉 **All 4 Phase 5 Interview Questions Completed**

Now test your understanding.

---

# 🧩 **PHASE 5 — Practice Questions (Answer These)**

### **Q1:** Write code to add a column: `tax = salary * 0.15`

---

### **Q2:** Write code to group by “city” and calculate avg(age).

---

### **Q3:** Write code to find total salary for each department.

---

### **Q4:** What does withColumn() do?

(One line explanation)

---

### **Q5:** What is the output of this?

```python
df.withColumn("double_salary", df.salary * 2)
```

---

# 🧪 **Mini Coding Task**

Dataset columns:

`id, name, age, salary, department`

### **Task:**

1. Add column: `hra = salary * 0.2`
2. Filter rows: age > 30
3. Group by department and calculate:

   * avg salary
   * max salary
   * min salary
4. Show the result
Here are the **perfect beginner-friendly answers** for all **Phase 5 practice questions + coding task solution** — exactly how you should answer in an interview.

---

# ✅ **PHASE 5 — Practice Question Answers**

---

### **Q1: Write code to add a column: `tax = salary * 0.15`**

```python
df = df.withColumn("tax", df.salary * 0.15)
```

---

### **Q2: Write code to group by “city” and calculate avg(age).**

```python
from pyspark.sql import functions as F

df.groupBy("city").agg(F.avg("age").alias("avg_age")).show()
```

---

### **Q3: Write code to find total salary for each department.**

```python
from pyspark.sql import functions as F

df.groupBy("department").agg(F.sum("salary").alias("total_salary")).show()
```

---

### **Q4: What does withColumn() do? (One line)**

**Answer:**
`withColumn()` is used to create a new column or update an existing column in a DataFrame.

---

### **Q5: What is the output of this?**

```python
df.withColumn("double_salary", df.salary * 2)
```

**Answer:**
It creates a new column **double_salary** where each row contains salary × 2.

---

# 🧪 **PHASE 5 — Mini Coding Task Solution**

Dataset columns:
`id, name, age, salary, department`

### **Task Requirements + Final Answer**

---

### **1. Add column: `hra = salary * 0.2`**

```python
df1 = df.withColumn("hra", df.salary * 0.2)
```

---

### **2. Filter rows: age > 30**

```python
df2 = df1.filter(df1.age > 30)
```

---

### **3. Group by department → avg, max, min salary**

```python
from pyspark.sql import functions as F

df3 = df2.groupBy("department").agg(
    F.avg("salary").alias("avg_salary"),
    F.max("salary").alias("max_salary"),
    F.min("salary").alias("min_salary")
)
```

---

### **4. Show result**

```python
df3.show()
```

---

# 🎉 **FINAL FULL SOLUTION (Combined Clean Code)**

```python
from pyspark.sql import SparkSession
from pyspark.sql import functions as F

spark = SparkSession.builder.appName("phase5_task").getOrCreate()

# Assume df is already loaded
# df = spark.read.csv("employees.csv", header=True, inferSchema=True)

# 1. Add HRA column
df1 = df.withColumn("hra", df.salary * 0.2)

# 2. Filter age > 30
df2 = df1.filter(df1.age > 30)

# 3. Group and aggregate
df3 = df2.groupBy("department").agg(
    F.avg("salary").alias("avg_salary"),
    F.max("salary").alias("max_salary"),
    F.min("salary").alias("min_salary")
)

# 4. Show results
df3.show()
```

---
Here is **PHASE 6 explained exactly like earlier phases**, including:

✔ Concept
✔ Code
✔ Interview answers
✔ Practice questions
✔ Coding test

No advanced topics — only beginner-friendly and interview-ready content.

---

# 🔵 **PHASE 6 — Joins (Very Important)**

Joins are **the #1 topic asked in PySpark interviews**
→ If you learn this phase properly, you can clear most basic PySpark rounds.

---

# ✅ **6.0 Understanding Joins**

You will usually have two DataFrames:

### **Employees Table**

```
emp(id, name, dept_id, salary)
```

### **Departments Table**

```
dept(id, dept_name)
```

We join them on:

```
emp.dept_id == dept.id
```

---

# ✅ **6.1 Inner Join**

### 🧠 Concept

Returns **only matching rows** from both DataFrames.

### 🧪 Code

```python
emp.join(dept, emp.dept_id == dept.id, "inner")
```

If dept_id doesn’t match → row is NOT included.

---

# ✅ **6.2 Left Join**

### 🧠 Concept

Return:

✔ All rows from LEFT (emp)
✔ Matching rows from right (dept)
✔ If no match → dept columns = NULL

### 🧪 Code

```python
emp.join(dept, emp.dept_id == dept.id, "left")
```

---

# ✅ **6.3 Right Join**

### 🧠 Concept

Opposite of left join:

✔ All rows from RIGHT (dept)
✔ Matching rows from emp
✔ If no match → emp columns = NULL

```python
emp.join(dept, emp.dept_id == dept.id, "right")
```

---

# ✅ **6.4 Full Join**

### 🧠 Concept

Return:

✔ All rows from both sides
✔ Match when possible
✔ No match → NULLs on missing side

### 🧪 Code

```python
emp.join(dept, emp.dept_id == dept.id, "full")
```

---

# 🔗 **INTERVIEW QUESTIONS & PERFECT ANSWERS**

---

### **Q41. What is a join in PySpark?**

A join combines two DataFrames based on a condition, usually matching keys.

---

### **Q42. What are the types of joins in PySpark?**

✔ inner
✔ left
✔ right
✔ full
✔ (Others exist, but these 4 are enough for beginner interviews)

---

### **Q43. How do you perform a join in PySpark?**

```python
emp.join(dept, emp.dept_id == dept.id, "inner")
```

---

### **Q44. What is a left join? Explain with example.**

A **left join** returns all rows from the left DataFrame and matching rows from the right.
If no match exists, right-side columns become NULL.

**Example:**

```python
emp.join(dept, emp.dept_id == dept.id, "left")
```

---

# 🎉 **All Phase 6 Interview Answers DONE**

Now practice for exam + interview.

---

# 🧩 **PHASE 6 — PRACTICE QUESTIONS**

### **Q1:** Write code to inner join `emp` and `dept`.

---

### **Q2:** What does a left join return?

---

### **Q3:** Which join will return NULLs on BOTH sides?

---

### **Q4:** What is the difference between inner and full join?

---

### **Q5:** True or False?

Right join returns all rows from the left DataFrame.

---

### **Q6:** Write a full join between these:

```
orders(order_id, user_id)
users(id, name)
```

---

# 🧪 **PHASE 6 — Coding Task**

### **Task:**

Given two DataFrames:

```
orders(order_id, user_id, amount)
users(id, name)
```

Do the following:

1. Perform a **left join** between orders and users
2. Show `order_id, name, amount`
3. Display NULL where name is missing

---
Here are the **complete, beginner-friendly answers** for all **Phase 6 practice questions + coding task**, exactly in the style interviewers expect.

---

# ✅ **PHASE 6 — PRACTICE QUESTION ANSWERS**

---

### **Q1: Write code to inner join `emp` and `dept`.**

```python
emp.join(dept, emp.dept_id == dept.id, "inner")
```

---

### **Q2: What does a left join return?**

**Answer:**
A left join returns:

✔ All rows from the left DataFrame
✔ Matching rows from the right
✔ If no match → right columns become NULL

---

### **Q3: Which join will return NULLs on BOTH sides?**

**Answer:**
**Full join**

---

### **Q4: What is the difference between inner and full join?**

* **Inner Join:** Returns only matching rows from both sides.
* **Full Join:** Returns all rows from both sides; unmatched rows contain NULLs.

---

### **Q5: True or False?

Right join returns all rows from the left DataFrame.**

**Answer:**
❌ **False**
Right join returns all rows from the **right** DataFrame.

---

### **Q6: Write a full join between orders and users.**

```python
orders.join(users, orders.user_id == users.id, "full")
```

---

# 🧪 **PHASE 6 — CODING TASK SOLUTION**

### **Task:**

DataFrames:

```
orders(order_id, user_id, amount)
users(id, name)
```

Goal:

1. Left join
2. Select: order_id, name, amount
3. Show NULL when no matching user

---

# ✅ **Final Code Solution**

```python
# 1. LEFT JOIN orders with users
result = orders.join(
    users,
    orders.user_id == users.id,
    "left"
)

# 2. Select necessary columns
final_df = result.select(
    "order_id",
    "name",
    "amount"
)

# 3. Show result
final_df.show()
```

---

# 🎉 **PHASE 6 Completed 100%**

Here is **PHASE 7 explained exactly like previous phases**, including:

✔ Clear concept
✔ Code
✔ Interview answers
✔ Practice questions
✔ Coding task

Beginner-friendly, no advanced topics.

---

# 🔵 **PHASE 7 — Handling NULL Values**

Handling NULLs is extremely important — in real data almost every dataset has missing values.

---

# ✅ **7.1 Dropping NULL Values**

### 🧠 Concept

You drop rows that contain **any NULL** or NULL in **specific columns**.

### 🧪 Example 1 — Drop rows with ANY NULL:

```python
df2 = df.dropna()
```

---

### 🧪 Example 2 — Drop rows with NULL in specific columns:

```python
df2 = df.dropna(subset=["age", "salary"])
```

---

# ✅ **7.2 Filling NULL Values**

### 🧠 Concept

Use `fillna()` to replace NULLs with default values.

### 🧪 Example:

```python
df2 = df.fillna({"age": 0, "salary": 0})
```

You can fill:

* Age → 0
* Salary → 0
* Department → "Unknown"

---

# 🧠 **7.3 Why is NULL Handling Important?**

NULLs cause:

❌ Wrong aggregations (avg, sum, max)
❌ Errors in joins
❌ Wrong calculations (salary * 0.1)
❌ Incorrect ML results

So cleaning NULLs is ALWAYS done in ETL.

Example:

If salary = NULL → bonus calculation → becomes NULL → wrong output.

---

# 🔗 **INTERVIEW QUESTIONS & PERFECT ANSWERS**

---

### **Q45. How do you drop rows with NULL values?**

```python
df.dropna()
```

Or specific columns:

```python
df.dropna(subset=["age"])
```

---

### **Q46. How do you fill NULL values?**

```python
df.fillna({"age": 0, "salary": 0})
```

---

### **Q47. Why is NULL handling important?**

Because NULL values can cause incorrect results in aggregations, joins, and calculations. Cleaning NULLs ensures accurate and reliable data processing.

---

# 🎉 **All PHASE 7 interview answers DONE**

Now practice time.

---

# 🧩 **PHASE 7 — PRACTICE QUESTIONS**

Try answering these:

### **Q1:** Remove rows where *any* value is NULL.

---

### **Q2:** Remove rows only when “age” is NULL.

---

### **Q3:** Fill NULL salary values with 50000.

---

### **Q4:** Fill NULL department values with “Unknown”.

---

### **Q5:** Why is handling NULL important during joins?

---

### **Q6:** If salary = NULL, what will happen when you compute `salary * 0.1`?

---

---

# 🧪 **PHASE 7 — Coding Task**

Dataset columns:

`id, name, age, salary, department`

### **Task:**

1. Remove rows where salary is NULL
2. Replace missing age with 0
3. Replace missing department with "Not Available"
4. Show result

Here are the **perfect answers** for all **Phase 7 practice questions + coding task**, exactly in interview style.

---

# ✅ **PHASE 7 — Practice Question Answers**

---

### **Q1: Remove rows where *any* value is NULL.**

```python
df2 = df.dropna()
```

---

### **Q2: Remove rows only when “age” is NULL.**

```python
df2 = df.dropna(subset=["age"])
```

---

### **Q3: Fill NULL salary values with 50000.**

```python
df2 = df.fillna({"salary": 50000})
```

---

### **Q4: Fill NULL department values with “Unknown”.**

```python
df2 = df.fillna({"department": "Unknown"})
```

---

### **Q5: Why is handling NULL important during joins?**

**Answer:**
Because NULLs can cause missing matches, produce incorrect join results, or generate NULL outputs in the final merged dataset.

---

### **Q6: If salary = NULL, what happens when you compute `salary * 0.1`?**

**Answer:**
The result becomes **NULL**, because any calculation with NULL results in NULL.

---

# 🎉 Perfect — practice questions done!

---

# 🧪 **PHASE 7 — Coding Task Solution**

Dataset:

`id, name, age, salary, department`

### **Task Requirements + Solution**

---

### **1. Remove rows where salary is NULL**

```python
df1 = df.dropna(subset=["salary"])
```

---

### **2. Replace missing age with 0**

```python
df2 = df1.fillna({"age": 0})
```

---

### **3. Replace missing department with "Not Available"**

```python
df3 = df2.fillna({"department": "Not Available"})
```

---

### **4. Show the final result**

```python
df3.show()
```

---

# 🌟 **Final Full Solution (Clean Code)**

```python
# 1. Drop rows where salary is NULL
df1 = df.dropna(subset=["salary"])

# 2. Fill missing age
df2 = df1.fillna({"age": 0})

# 3. Fill missing department
df3 = df2.fillna({"department": "Not Available"})

# 4. Show
df3.show()
```

---

Here is **PHASE 8 explained exactly like earlier phases**, with:

✔ Concept
✔ Simple examples
✔ Interview answers
✔ Practice questions
✔ Coding task

Everything is beginner-friendly and 100% interview-oriented.

---

# 🔵 **PHASE 8 — File Formats & Schema**

File formats are an **easy but high-frequency interview topic**, especially for apprenticeship & fresher rounds.

---

# ✅ **8.1 Supported File Formats in PySpark**

PySpark commonly works with:

### ✔ CSV

Text-based, row-oriented, slow for big data.

### ✔ JSON

Hierarchical / nested data.

### ✔ Parquet

Columnar, compressed, best for big data processing.

### ✔ ORC

Also columnar, optimized for Hadoop.

### ✔ Avro

Used in streaming / messaging systems.

---

# 🧪 **How to read them (concept-level)**

### **CSV**

```python
df = spark.read.csv("data.csv", header=True, inferSchema=True)
```

---

### **JSON**

```python
df = spark.read.json("data.json")
```

---

### **Parquet**

```python
df = spark.read.parquet("data.parquet")
```

---

### **Avro** (if supported)

```python
df = spark.read.format("avro").load("data.avro")
```

---

# 🔥 **8.2 Why Parquet Is the Best Format**

### ✔ Columnar

Data stored column-by-column, not row-by-row.

### ✔ Highly compressed

Takes far less space on disk.

### ✔ Faster queries

Spark reads only required columns rather than entire rows.

### ✔ Preferred for big data & analytics

Used in almost all production pipelines.

---

# 🟦 **8.3 JSON Format**

JSON is used for:

✔ Nested data
✔ API data
✔ Logs
✔ Event data

Spark automatically handles nested structures (concept-level only for now).

---

# 🟩 **8.4 Schema in PySpark**

### 🧠 What is schema?

Schema = structure of your DataFrame
(columns + datatypes)

Example schema:

```
root
 |-- name: string
 |-- age: integer
 |-- salary: double
```

### 🧪 How to see schema?

```python
df.printSchema()
```

### 💡 Why schema matters?

✔ Ensures type correctness
✔ Improves performance
✔ Prevents errors in joins
✔ Helps Spark optimize queries

---

# 🔗 **INTERVIEW QUESTIONS & PERFECT ANSWERS**

---

### **Q48. What file formats does PySpark support?**

CSV, JSON, Parquet, ORC, Avro.

---

### **Q49. Why is Parquet faster than CSV?**

Parquet is columnar, compressed, and Spark reads only required columns, making it faster and more efficient.

---

### **Q50. What is JSON used for?**

For nested or hierarchical data like API responses, logs, and metadata.

---

### **Q51. Which format is best for big data use cases?**

**Parquet** — because it is columnar, compressed, and optimized for analytics.

---

### **Q52. How do you work with JSON, Parquet, Avro in PySpark?**

Use:

```python
spark.read.json()
spark.read.parquet()
spark.read.format("avro").load()
```

---

### **Q53. What is a DataFrame schema and why is it important?**

Schema defines the structure and data types of a DataFrame.
It is important for performance, correctness, and preventing type errors during transformations and joins.

---

# 🎉 **Phase 8 Interview Answers Completed**

Now test your understanding.

---

# 🧩 **PHASE 8 — Practice Questions**

### **Q1:** Why is Parquet preferred over CSV?

---

### **Q2:** Write code to read "products.json" in PySpark.

---

### **Q3:** What kind of data does JSON handle well?

---

### **Q4:** Write code to read a Parquet file.

---

### **Q5:** What does a schema contain?

---

### **Q6:** Why is schema important in PySpark?

---

---

# 🧪 **PHASE 8 — Coding Task**

Dataset files:

```
employees.csv
employees.parquet
employees.json
```

### **Task:**

1. Read all three files into DataFrames
2. Print schema of each
3. Identify which format loads fastest (conceptually)
4. Explain why

---
Here are the **complete Phase 8 answers**, including **practice questions + coding task solution**, written exactly in beginner-friendly, interview-ready style.

---

# ✅ **PHASE 8 — Practice Question Answers**

---

### **Q1: Why is Parquet preferred over CSV?**

**Answer:**
Because Parquet is **columnar, compressed, faster, and more efficient** than CSV.
Spark reads only required columns instead of whole rows, which reduces scanning time.

---

### **Q2: Write code to read `"products.json"` in PySpark.**

```python
df = spark.read.json("products.json")
```

---

### **Q3: What kind of data does JSON handle well?**

**Answer:**
JSON works well with **nested** or **hierarchical** data such as:

* API responses
* Logs
* Event data
* Metadata

---

### **Q4: Write code to read a Parquet file.**

```python
df = spark.read.parquet("data.parquet")
```

---

### **Q5: What does a schema contain?**

**Answer:**
Schema contains:

* Column names
* Data types
* Structure of the DataFrame

Example:

```
name: string  
age: integer  
salary: double
```

---

### **Q6: Why is schema important in PySpark?**

**Answer:**
Schema is important because it ensures:

✔ Correct data types
✔ Faster execution
✔ Fewer errors in joins
✔ Better optimization by Spark

---

# 🎉 Practice Questions DONE PERFECTLY

Now the coding task.

---

# 🧪 **PHASE 8 — Coding Task Solution**

### **Task:**

Read:

* `employees.csv`
* `employees.parquet`
* `employees.json`

Then print schema of each and compare which format loads fastest.

---

# ✅ **Final Full Code Solution**

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("phase8_formats").getOrCreate()

# 1. Read CSV
df_csv = spark.read.csv("employees.csv", header=True, inferSchema=True)

# 2. Read Parquet
df_parquet = spark.read.parquet("employees.parquet")

# 3. Read JSON
df_json = spark.read.json("employees.json")

# Print schemas
print("CSV Schema:")
df_csv.printSchema()

print("Parquet Schema:")
df_parquet.printSchema()

print("JSON Schema:")
df_json.printSchema()
```

---

# 🧠 **3. Identify which is fastest (conceptual answer)**

### ✔ **Parquet loads fastest**

Because:

* It’s columnar
* Compressed
* Optimized for Spark
* Stores data + schema together

CSV and JSON are slower because they:

* Are row-based
* Not compressed
* Require parsing
* Need type inference

---

# 🎉 **PHASE 8 is fully completed**

Here is **PHASE 9 explained exactly like previous phases**, including:

✔ Simple concepts
✔ Code
✔ Interview answers
✔ Practice questions
✔ Coding task

Beginner-friendly & perfect for apprenticeship interviews.

---

# 🔵 **PHASE 9 — SQL in PySpark**

SQL with PySpark is very powerful because you can use normal SQL syntax directly on DataFrames.

---

# ✅ **9.1 Creating a Temporary SQL View**

### 🧠 Concept

A temp view allows you to run SQL queries **as if the DataFrame were a SQL table**.

### 🧪 Code

```python
df.createOrReplaceTempView("emp")
```

This creates a table named `"emp"` that you can query using SQL.

---

# ✅ **9.2 Running SQL Queries**

### 🧠 Concept

Use `spark.sql()` to run SQL statements.

### 🧪 Example

```python
result = spark.sql("SELECT name, age FROM emp WHERE age > 30")
result.show()
```

---

# 🔥 What SQL can do in PySpark?

✔ SELECT columns
✔ WHERE filtering
✔ GROUP BY
✔ ORDER BY
✔ Aggregations (SUM, AVG, MAX, MIN)

Everything you know from SQL works here.

---

# 🔗 **INTERVIEW QUESTIONS & PERFECT ANSWERS**

---

### **Q54. How do you create a temporary SQL table in PySpark?**

```python
df.createOrReplaceTempView("emp")
```

---

### **Q55. How do you run SQL queries using spark.sql?**

```python
spark.sql("SELECT * FROM emp")
```

---

### **Q56. How do you filter data using SQL queries in PySpark?**

```python
spark.sql("SELECT * FROM emp WHERE age > 30")
```

---

### **Q57. How do you select columns using SQL in PySpark?**

```python
spark.sql("SELECT name, age FROM emp")
```

---

# 🎉 PHASE 9 — Interview Answers Completed

Now practice to strengthen your skills.

---

# 🧩 **PHASE 9 — Practice Questions**

Try answering these yourself:

---

### **Q1:** Create a temp view called `"students"` from DataFrame `df_students`.

---

### **Q2:** Write SQL to select `name` and `city` from `"students"`.

---

### **Q3:** Write SQL to get employees with salary > 50000.

---

### **Q4:** Write SQL to get average salary per department.

---

### **Q5:** Write SQL to get only distinct department names.

---

---

# 🧪 **PHASE 9 — Coding Task**

You have a DataFrame:

```
emp(id, name, age, salary, department)
```

### **Task:**

1. Create temp view `"emp"`
2. Run SQL to:

   * Select name, salary
   * Filter age > 25
   * Group by department
   * Show average salary

---

Below are the **perfect beginner-friendly answers** for all **Phase 9 practice questions + coding task** — exactly as expected in interviews.

---

# ✅ **PHASE 9 — Practice Question Answers**

---

### **Q1: Create a temp view called `"students"` from DataFrame `df_students`.**

```python
df_students.createOrReplaceTempView("students")
```

---

### **Q2: Write SQL to select `name` and `city` from `"students"`.**

```python
spark.sql("SELECT name, city FROM students")
```

---

### **Q3: Write SQL to get employees with salary > 50000.**

```python
spark.sql("SELECT * FROM emp WHERE salary > 50000")
```

---

### **Q4: Write SQL to get average salary per department.**

```python
spark.sql("SELECT department, AVG(salary) AS avg_salary FROM emp GROUP BY department")
```

---

### **Q5: Write SQL to get only distinct department names.**

```python
spark.sql("SELECT DISTINCT department FROM emp")
```

---

# 🎉 Practice Questions DONE!

Now the coding task solution.

---

# 🧪 **PHASE 9 — Coding Task Solution**

DataFrame:

```
emp(id, name, age, salary, department)
```

### **Task Requirements + Final Solution**

---

### **1. Create temp view "emp"**

```python
df.createOrReplaceTempView("emp")
```

---

### **2. Run SQL to:**

* Select **name**, **salary**
* Filter **age > 25**
* Group by **department**
* Show **average salary**

### ✅ **Final SQL Query**

```python
result = spark.sql("""
    SELECT 
        department,
        AVG(salary) AS avg_salary
    FROM emp
    WHERE age > 25
    GROUP BY department
""")

result.show()
```

---

# 🎉 PHASE 9 COMPLETED 100%
Here is **PHASE 10 explained exactly like previous phases**, with:

✔ Concept
✔ Clean code
✔ Interview answers
✔ Practice questions
✔ Mini coding task (your last test before finishing PySpark basics)

Beginner-friendly. No advanced content.

---

# 🔵 **PHASE 10 — Mini ETL Task (Must Be Confident)**

This is the **same coding task** almost every company gives for apprenticeships & fresher PySpark interviews.

You must be able to:

✔ Write the ETL steps
✔ Explain them verbally
✔ Show code
✔ Answer related questions

Let’s go step by step.

---

# ✅ **10.1 FILTER → Employees age > 30**

### 🧠 Concept

Keep only rows where age is greater than 30.

### 🧪 Code

```python
df2 = df.filter(df.age > 30)
```

Equivalent using `where()`:

```python
df2 = df.where(df.age > 30)
```

---

# ✅ **10.2 TRANSFORM → Add Bonus Column**

### 🧠 Concept

Add a new column:
**bonus = salary * 0.1**

### 🧪 Code

```python
df3 = df2.withColumn("bonus", df2.salary * 0.1)
```

---

# ✅ **10.3 GROUP → Average Salary by Age**

### 🧠 Concept

Group rows by age and compute average salary.

### 🧪 Code

```python
from pyspark.sql import functions as F

df4 = df3.groupBy("age").agg(
    F.avg("salary").alias("avg_salary")
)

df4.show()
```

---

# ✅ **10.4 Explain ETL Steps Clearly (Interview-Perfect Answer)**

When interviewer asks:

**“Explain what ETL you performed.”**

You say:

**E (Extract)**

* Data loaded from CSV/Parquet into a DataFrame using `spark.read`.

**T (Transform)**

* Filtered employees with age > 30
* Added a new calculated column: bonus = salary * 0.1
* Grouped by age and calculated average salary

**L (Load)**

* Final DataFrame can be written back to CSV/Parquet or passed to reporting.

This is **exactly** how you explain it in a face-to-face round.

---

# 🔗 **PHASE 10 — INTERVIEW QUESTIONS & PERFECT ANSWERS**

---

### **Q58. How do you filter employees whose age > 30?**

```python
df.filter(df.age > 30)
```

---

### **Q59. How do you add a bonus column = 10% salary?**

```python
df.withColumn("bonus", df.salary * 0.1)
```

---

### **Q60. How do you group by age and find average salary?**

```python
df.groupBy("age").agg(F.avg("salary"))
```

---

### **Q61. Explain the ETL steps you performed.**

**Answer:**
I extracted the data from CSV into a DataFrame.
Then I transformed it by filtering employees older than 30, adding a bonus column, and grouping by age to compute average salary.
Finally, the result can be loaded into a new file or used in reports.

---

# 🎉 **All PHASE 10 interview answers DONE**

Now let’s practice.

---

# 🧩 **PHASE 10 — Practice Questions**

Try answering these yourself:

---

### **Q1:** Write code to filter rows where salary > 60000.

---

### **Q2:** Add a new column `tax = salary * 0.05`.

---

### **Q3:** Group by department and find total salary.

---

### **Q4:** Explain ETL in 3 lines.

---

### **Q5:** What happens if salary contains NULL when computing bonus?

---

---

# 🧪 **PHASE 10 — Coding Task (Final ETL Test)**

Dataset:

`id, name, age, salary, department`

### **Task:**

1. Filter employees age >= 28
2. Add HRA = salary * 0.2
3. Add PF = salary * 0.12
4. Group by department → find avg, max, min salary
5. Show final output

---

Here are the **answers for all Phase 10 practice questions + final ETL coding task**, written exactly in beginner-friendly + interview-ready format.

---

# ✅ **PHASE 10 — Practice Question Answers**

---

# 🧩 **Q1. Write code to filter rows where salary > 60000.**

```python
df_high_salary = df.filter(df.salary > 60000)
df_high_salary.show()
```

---

# 🧩 **Q2. Add a new column `tax = salary * 0.05`.**

```python
df_with_tax = df.withColumn("tax", df.salary * 0.05)
df_with_tax.show()
```

---

# 🧩 **Q3. Group by department and find total salary.**

```python
from pyspark.sql import functions as F

df_dept_total = df.groupBy("department").agg(
    F.sum("salary").alias("total_salary")
)
df_dept_total.show()
```

---

# 🧩 **Q4. Explain ETL in 3 lines. (Interview Answer)**

**E (Extract):** Load data from CSV/JSON/Parquet into a PySpark DataFrame.
**T (Transform):** Apply operations like filtering, adding columns, joining, grouping.
**L (Load):** Save the final output to CSV/Parquet or pass to another system.

---

# 🧩 **Q5. What happens if salary contains NULL when computing bonus?**

**Answer:**
If salary is NULL, then:

```python
bonus = salary * 0.1
```

will also become **NULL**, because any calculation with NULL results in NULL.

To avoid this, we can fill NULL salaries before computing bonus:

```python
df = df.fillna({"salary": 0})
```

---

# 🎯 **PHASE 10 — Final ETL Task (FULL ANSWER)**

Dataset columns:

`id, name, age, salary, department`

---

# 🔵 **Step 1 — Filter employees age >= 28**

```python
df1 = df.filter(df.age >= 28)
```

---

# 🔵 **Step 2 — Add HRA = salary * 0.2**

```python
df2 = df1.withColumn("HRA", df1.salary * 0.2)
```

---

# 🔵 **Step 3 — Add PF = salary * 0.12**

```python
df3 = df2.withColumn("PF", df2.salary * 0.12)
```

---

# 🔵 **Step 4 — Group by department → avg, max, min salary**

```python
from pyspark.sql import functions as F

df4 = df3.groupBy("department").agg(
    F.avg("salary").alias("avg_salary"),
    F.max("salary").alias("max_salary"),
    F.min("salary").alias("min_salary")
)
```

---

# 🔵 **Step 5 — Show final output**

```python
df4.show()
```

---

# 🧠 **Interview Explanation (Use This)**

“In my ETL pipeline, I first **extracted** the data into a DataFrame using Spark.
Then I **transformed** it by filtering employees aged 28+, adding calculated columns like HRA and PF, and grouping by department to get summary metrics.
Finally, the results can be **loaded** into Parquet or CSV for reporting.”

---














  


