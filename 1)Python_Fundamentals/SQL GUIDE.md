# 🎯 COMPREHENSIVE SQL GUIDE: MASTERING SUBQUERIES, GROUP BY & HAVING

## 📚 **TABLE OF CONTENTS**
1. [Question Recognition Patterns](#question-recognition-patterns)
2. [Decision Tree: Which Concept to Use](#decision-tree)
3. [GROUP BY & HAVING Deep Dive](#group-by-having)
4. [SUBQUERY Mastery Guide](#subquery-mastery)
5. [Step-by-Step Problem Solving Framework](#problem-solving-framework)
6. [100+ Solved Examples with Patterns](#solved-examples)

---

## 🔍 **QUESTION RECOGNITION PATTERNS**

### **INSTANT IDENTIFICATION KEYWORDS**

| **Keywords in Question** | **Concept to Use** | **Confidence** |
|-------------------------|-------------------|----------------|
| "each", "every", "per", "in each" | GROUP BY | 100% |
| "total", "sum", "average", "count", "maximum", "minimum" + "each/per" | GROUP BY + Aggregate | 100% |
| "more than X employees/records", "at least", "having" | GROUP BY + HAVING | 100% |
| "department NAME", "location", "other table columns" | SUBQUERY (JOIN alternative) | 95% |
| "same as [person]", "greater than [person]", "less than [person]" | SUBQUERY (comparison) | 100% |
| "who is reporting to [name]", "[person]'s manager" | SUBQUERY (self-reference) | 100% |
| "maximum", "minimum", "average" used for COMPARISON | SUBQUERY | 90% |
| "2nd maximum", "3rd minimum", "nth highest" | NESTED SUBQUERY | 100% |
| "more than ANY", "less than ALL", "greater than ALL" | MULTIROW SUBQUERY | 100% |

---

## 🌳 **DECISION TREE: WHICH CONCEPT TO USE?**

```
START: Read the Question
    |
    ├─► Contains "EACH", "EVERY", "PER"?
    │       │
    │       YES ──► Contains "MORE THAN", "AT LEAST", "FILTER GROUPS"?
    │       │           │
    │       │           YES ──► USE: GROUP BY + HAVING
    │       │           │
    │       │           NO ──► USE: GROUP BY (without HAVING)
    │       │
    │       NO
    │       │
    ├─► Needs data from ANOTHER TABLE (DEPT, not in EMP)?
    │       │
    │       YES ──► USE: SUBQUERY (to get dept name, location, etc.)
    │       │
    │       NO
    │       │
    ├─► Comparing with SPECIFIC PERSON/VALUE (same as SCOTT, more than SMITH)?
    │       │
    │       YES ──► USE: SUBQUERY (single row or multirow)
    │       │
    │       NO
    │       │
    ├─► Finding NTH MAX/MIN (2nd highest, 3rd minimum)?
    │       │
    │       YES ──► USE: NESTED SUBQUERY
    │       │
    │       NO
    │       │
    └─► Simple filtering (salary > 1500, dept = 10)?
            │
            YES ──► USE: WHERE clause (Basic Operators)
```

---

## 📊 **GROUP BY & HAVING DEEP DIVE**

### **CORE CONCEPT**
- **GROUP BY**: Divides rows into groups based on column values
- **HAVING**: Filters those groups based on aggregate conditions
- **WHERE**: Filters ROWS before grouping (cannot use aggregate functions)

### **EXECUTION ORDER**
```
1. FROM        ──► Select table
2. WHERE       ──► Filter ROWS (row by row)
3. GROUP BY    ──► Create groups
4. HAVING      ──► Filter GROUPS (group by group)
5. SELECT      ──► Display results
6. ORDER BY    ──► Sort results
```

### **PATTERN RECOGNITION FOR GROUP BY**

#### **Pattern 1: Simple Grouping (No Filter)**
**Keywords**: "in each", "per", "every", "for each"

**Example Question**:
> "Display number of employees working in EACH department"

**Recognition**: 
- ✅ Has "EACH" → GROUP BY needed
- ❌ No filter condition → No HAVING

**Solution Pattern**:
```sql
SELECT COUNT(*), DEPTNO
FROM EMP
GROUP BY DEPTNO;
```

**Template**:
```sql
SELECT AGGREGATE_FUNCTION(column), GROUPING_COLUMN
FROM TABLE
GROUP BY GROUPING_COLUMN;
```

---

#### **Pattern 2: Grouping with Row Filter (WHERE)**
**Keywords**: "in each" + condition on individual rows

**Example Question**:
> "Display number of SALESMEN in EACH department"

**Recognition**:
- ✅ Has "EACH" → GROUP BY needed
- ✅ "SALESMEN" is row-level filter → Use WHERE
- ❌ No group filter → No HAVING

**Solution Pattern**:
```sql
SELECT COUNT(*), DEPTNO
FROM EMP
WHERE JOB = 'SALESMAN'  -- Filter ROWS first
GROUP BY DEPTNO;
```

**Template**:
```sql
SELECT AGGREGATE_FUNCTION(column), GROUPING_COLUMN
FROM TABLE
WHERE ROW_LEVEL_CONDITION
GROUP BY GROUPING_COLUMN;
```

---

#### **Pattern 3: Grouping with Group Filter (HAVING)**
**Keywords**: "more than", "at least", "filter groups", "having"

**Example Question**:
> "Display departments having MORE THAN 2 employees"

**Recognition**:
- ✅ Has "MORE THAN" → HAVING needed
- ✅ Filtering based on COUNT → GROUP BY + HAVING
- ✅ "2 employees" is group-level condition

**Solution Pattern**:
```sql
SELECT COUNT(*), DEPTNO
FROM EMP
GROUP BY DEPTNO
HAVING COUNT(*) > 2;  -- Filter GROUPS
```

**Template**:
```sql
SELECT AGGREGATE_FUNCTION(column), GROUPING_COLUMN
FROM TABLE
GROUP BY GROUPING_COLUMN
HAVING AGGREGATE_CONDITION;
```

---

#### **Pattern 4: Complete Pattern (WHERE + GROUP BY + HAVING)**
**Keywords**: row filter + "each" + group filter

**Example Question**:
> "Display number of MANAGERS in EACH department where department has MORE THAN 2 managers"

**Recognition**:
- ✅ "MANAGERS" → WHERE clause (row filter)
- ✅ "EACH department" → GROUP BY
- ✅ "MORE THAN 2" → HAVING (group filter)

**Solution Pattern**:
```sql
SELECT COUNT(*), DEPTNO
FROM EMP
WHERE JOB = 'MANAGER'      -- Filter rows first
GROUP BY DEPTNO             -- Create groups
HAVING COUNT(*) > 2;        -- Filter groups
```

**Template**:
```sql
SELECT AGGREGATE_FUNCTION(column), GROUPING_COLUMN
FROM TABLE
WHERE ROW_LEVEL_CONDITION
GROUP BY GROUPING_COLUMN
HAVING GROUP_LEVEL_CONDITION;
```

---

### **WHERE vs HAVING: THE ULTIMATE RULE**

| **Aspect** | **WHERE** | **HAVING** |
|-----------|-----------|-----------|
| **When to use** | Filter individual ROWS | Filter GROUPS |
| **Executes** | BEFORE grouping (row by row) | AFTER grouping (group by group) |
| **Can use aggregates?** | ❌ NO (COUNT, SUM, AVG not allowed) | ✅ YES (COUNT, SUM, AVG allowed) |
| **Example condition** | `WHERE JOB = 'MANAGER'` | `HAVING COUNT(*) > 2` |
| **Filters based on** | Column values | Aggregate results |

**🔥 GOLDEN RULE**:
- If condition checks **INDIVIDUAL ROW** values → WHERE
- If condition checks **AGGREGATE/GROUP** results → HAVING

---

### **COMMON GROUP BY QUESTIONS - SOLVED**

#### **Q1: Display total salary needed to pay EACH JOB**
```sql
SELECT SUM(SAL), JOB
FROM EMP
GROUP BY JOB;
```
**Why**: "EACH JOB" → GROUP BY JOB

---

#### **Q2: Display hire dates on which AT LEAST 3 employees were hired**
```sql
SELECT HIREDATE, COUNT(*)
FROM EMP
GROUP BY HIREDATE
HAVING COUNT(*) >= 3;
```
**Why**: 
- "AT LEAST 3" → HAVING (group filter)
- Grouping by HIREDATE

---

#### **Q3: Display dept number with MORE THAN 2 employees and total salary > 9000**
```sql
SELECT DEPTNO, COUNT(*), SUM(SAL)
FROM EMP
GROUP BY DEPTNO
HAVING COUNT(*) > 2 AND SUM(SAL) > 9000;
```
**Why**:
- "MORE THAN 2 employees" → HAVING COUNT(*) > 2
- "total salary > 9000" → HAVING SUM(SAL) > 9000
- Multiple conditions in HAVING

---

#### **Q4: Number of employees in EACH dept, EXCLUDING those where salary < commission**
```sql
SELECT DEPTNO, COUNT(*), AVG(SAL)
FROM EMP
WHERE SAL >= COMM OR COMM IS NULL  -- Filter rows first
GROUP BY DEPTNO;
```
**Why**:
- "salary < commission" checks INDIVIDUAL rows → WHERE
- "EACH dept" → GROUP BY

---

#### **Q5: Display salaries that have REPETITIONS**
```sql
SELECT SAL, COUNT(*)
FROM EMP
GROUP BY SAL
HAVING COUNT(*) > 1;
```
**Why**:
- "REPETITIONS" means more than 1 occurrence → HAVING COUNT(*) > 1

---

#### **Q6: Display employee names that appear MORE THAN ONCE**
```sql
SELECT ENAME, COUNT(*)
FROM EMP
GROUP BY ENAME
HAVING COUNT(*) > 1;
```
**Why**: Similar to Q5, checking for duplicates

---

#### **Q7: Display dept numbers with AVERAGE salary BETWEEN 2500 AND 3000**
```sql
SELECT DEPTNO, AVG(SAL)
FROM EMP
GROUP BY DEPTNO
HAVING AVG(SAL) BETWEEN 2500 AND 3000;
```
**Why**: "AVERAGE salary" is aggregate → HAVING

---

#### **Q8: Number of employees as MANAGER or ANALYST with annual salary ending in 0, in EACH dept**
```sql
SELECT DEPTNO, COUNT(*)
FROM EMP
WHERE (JOB = 'MANAGER' OR JOB = 'ANALYST')  -- Row filter
  AND MOD(SAL * 12, 10) = 0                  -- Annual sal ends with 0
GROUP BY DEPTNO;
```
**Why**:
- "MANAGER or ANALYST" → WHERE (row condition)
- "annual salary ending 0" → WHERE (can calculate per row)
- "EACH dept" → GROUP BY

---

#### **Q9: Number of CLERKS in EACH department**
```sql
SELECT DEPTNO, COUNT(*)
FROM EMP
WHERE JOB = 'CLERK'
GROUP BY DEPTNO;
```

---

#### **Q10: Highest salary given to MANAGER in EACH department**
```sql
SELECT DEPTNO, MAX(SAL)
FROM EMP
WHERE JOB = 'MANAGER'
GROUP BY DEPTNO;
```

---

#### **Q11: Number of times salaries have repeated**
```sql
SELECT SAL, COUNT(*) AS REPETITION_COUNT
FROM EMP
GROUP BY SAL
HAVING COUNT(*) > 1;
```

---

#### **Q12: Deptno and count EXCEPT dept 10**
```sql
SELECT DEPTNO, COUNT(*)
FROM EMP
WHERE DEPTNO != 10
GROUP BY DEPTNO;
```
**Why**: "EXCEPT dept 10" → WHERE (row filter)

---

#### **Q13: Number of employees getting commission in EACH dept**
```sql
SELECT DEPTNO, COUNT(*)
FROM EMP
WHERE COMM IS NOT NULL AND COMM > 0
GROUP BY DEPTNO;
```

---

#### **Q14: Employees getting salary > 1600 EXCLUDING managers in EACH dept**
```sql
SELECT DEPTNO, COUNT(*)
FROM EMP
WHERE SAL > 1600 AND JOB != 'MANAGER'
GROUP BY DEPTNO;
```

---

#### **Q15: Average salary for employees with reporting manager in EACH job**
```sql
SELECT JOB, AVG(SAL)
FROM EMP
WHERE MGR IS NOT NULL
GROUP BY JOB;
```

---

#### **Q16: Number of employees hired on SAME DAY in SAME DEPT**
```sql
SELECT DEPTNO, HIREDATE, COUNT(*)
FROM EMP
GROUP BY DEPTNO, HIREDATE  -- Multiple column grouping
HAVING COUNT(*) > 1;
```
**Why**: "SAME DAY + SAME DEPT" → GROUP BY both columns

---

#### **Q17: Employees getting SAME SALARY in SAME DEPARTMENT**
```sql
SELECT DEPTNO, SAL, COUNT(*)
FROM EMP
GROUP BY DEPTNO, SAL
HAVING COUNT(*) > 1;
```

---

#### **Q18: Maximum salary in EACH designation EXCLUDING names starting with 'K'**
```sql
SELECT JOB, MAX(SAL)
FROM EMP
WHERE ENAME NOT LIKE 'K%'  -- Row filter
GROUP BY JOB;
```

---

#### **Q19: Number of employees reporting to 7839 in EACH dept**
```sql
SELECT DEPTNO, COUNT(*)
FROM EMP
WHERE MGR = 7839
GROUP BY DEPTNO;
```

---

#### **Q20: Number of employees with names starting with vowel in EACH dept**
```sql
SELECT DEPTNO, COUNT(*)
FROM EMP
WHERE ENAME LIKE 'A%' OR ENAME LIKE 'E%' 
   OR ENAME LIKE 'I%' OR ENAME LIKE 'O%' 
   OR ENAME LIKE 'U%'
GROUP BY DEPTNO;
```

---

## 🎯 **SUBQUERY MASTERY GUIDE**

### **WHAT IS A SUBQUERY?**
A query within another query. Used when:
1. You need data from another table (without JOIN)
2. You need to compare with an unknown value (SCOTT's salary, MAX salary, etc.)
3. You need complex filtering based on aggregates

### **SUBQUERY TYPES & WHEN TO USE**

#### **Type 1: SINGLE ROW SUBQUERY** 
Returns **ONE value** (one row, one column)

**When to use**:
- Comparing with ONE person's data
- Getting MAX, MIN, AVG (returns single value)
- Getting COUNT of something specific

**Operators**: `=`, `>`, `<`, `>=`, `<=`, `!=`

**Pattern Recognition**:
- "salary same as SCOTT"
- "more than SMITH's salary"
- "maximum salary"
- "average salary"

**Example**:
```sql
-- Get employees earning more than SMITH
SELECT * FROM EMP
WHERE SAL > (SELECT SAL FROM EMP WHERE ENAME = 'SMITH');
           -- ↑ Returns single value: 800
```

---

#### **Type 2: MULTIROW SUBQUERY**
Returns **MULTIPLE values** (multiple rows, one column)

**When to use**:
- Comparing with MULTIPLE values
- Getting dept numbers, manager numbers, etc. (multiple results)
- "ANY", "ALL" comparisons

**Operators**: 
- `IN` / `NOT IN` (equals to any value in list)
- `> ANY` / `< ANY` (greater/less than at least one value)
- `> ALL` / `< ALL` (greater/less than all values)

**Pattern Recognition**:
- "same as any SALESMAN"
- "more than all MANAGERS"
- "in departments that have..."
- "NOT in dept 10 or 20" (can also use NOT IN)

**Example**:
```sql
-- Get employees in SALES or RESEARCH dept
SELECT * FROM EMP
WHERE DEPTNO IN (SELECT DEPTNO FROM DEPT 
                 WHERE DNAME IN ('SALES', 'RESEARCH'));
                -- ↑ Returns multiple values: 20, 30

-- Employees earning more than ANY clerk
SELECT * FROM EMP
WHERE SAL > ANY (SELECT SAL FROM EMP WHERE JOB = 'CLERK');
            -- ↑ Returns: 800, 950, 1100, 1300

-- Employees earning more than ALL managers
SELECT * FROM EMP
WHERE SAL > ALL (SELECT SAL FROM EMP WHERE JOB = 'MANAGER');
            -- ↑ Returns: 2450, 2850, 2975
```

---

#### **Type 3: NESTED SUBQUERY**
Subquery within subquery (2+ levels deep)

**When to use**:
- Finding Nth MAX/MIN salary
- Multi-level relationships (manager's manager)
- Complex conditions

**Pattern Recognition**:
- "2nd maximum salary"
- "3rd minimum"
- "manager's manager"
- "employees reporting to BLAKE's manager"

**Example**:
```sql
-- Find 2nd maximum salary
SELECT MAX(SAL) FROM EMP
WHERE SAL < (SELECT MAX(SAL) FROM EMP);
        -- Inner query gets 1st max, outer gets 2nd max

-- Find 3rd minimum salary
SELECT MIN(SAL) FROM EMP
WHERE SAL > (SELECT MIN(SAL) FROM EMP
             WHERE SAL > (SELECT MIN(SAL) FROM EMP));
```

---

#### **Type 4: CORRELATED SUBQUERY**
Inner query references outer query's table

**When to use**:
- Comparing with "same department's average"
- Finding records matching group-level conditions
- "Employees earning more than their dept's average"

**Pattern Recognition**:
- "more than THEIR department's average"
- "highest salary IN THEIR job"
- "RESPECTIVE departments/jobs"

**Example**:
```sql
-- Employees earning > their dept's average
SELECT * FROM EMP E1
WHERE SAL > (SELECT AVG(SAL) FROM EMP E2 
             WHERE E2.DEPTNO = E1.DEPTNO);
            -- ↑ Correlated: uses E1.DEPTNO from outer query
```

---

### **SUBQUERY IN DIFFERENT CLAUSES**

#### **1. Subquery in WHERE clause** (Most common)
```sql
-- Example: Employees in SALES dept
SELECT * FROM EMP
WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE DNAME = 'SALES');
```

#### **2. Subquery in FROM clause** (Inline view)
```sql
-- Example: Avg of department averages
SELECT AVG(DEPT_AVG) 
FROM (SELECT AVG(SAL) AS DEPT_AVG FROM EMP GROUP BY DEPTNO);
```

#### **3. Subquery in SELECT clause** (Scalar subquery)
```sql
-- Example: Show employee with dept name
SELECT ENAME, 
       (SELECT DNAME FROM DEPT WHERE DEPTNO = EMP.DEPTNO) AS DNAME
FROM EMP;
```

#### **4. Subquery in HAVING clause**
```sql
-- Example: Depts with avg salary > company average
SELECT DEPTNO, AVG(SAL)
FROM EMP
GROUP BY DEPTNO
HAVING AVG(SAL) > (SELECT AVG(SAL) FROM EMP);
```

---

### **SUBQUERY SOLVING PATTERNS**

#### **Pattern 1: Getting Department Name/Location**
**Question Pattern**: "Display employees in [DEPARTMENT NAME]" or "Show location of..."

**Why Subquery?**: DNAME and LOC are in DEPT table, not EMP table

**Solution Template**:
```sql
-- Step 1: Get DEPTNO for department name
SELECT DEPTNO FROM DEPT WHERE DNAME = 'SALES';  -- Returns: 30

-- Step 2: Use in main query
SELECT * FROM EMP
WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE DNAME = 'SALES');
```

**Examples**:
```sql
-- Q: Employees in ACCOUNTING dept
SELECT * FROM EMP
WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE DNAME = 'ACCOUNTING');

-- Q: Display location of employees earning commission
SELECT DISTINCT (SELECT LOC FROM DEPT WHERE DEPTNO = EMP.DEPTNO) AS LOCATION
FROM EMP
WHERE COMM IS NOT NULL AND COMM > 0;

-- Alternative:
SELECT DISTINCT LOC FROM DEPT
WHERE DEPTNO IN (SELECT DEPTNO FROM EMP 
                 WHERE COMM IS NOT NULL AND COMM > 0);
```

---

#### **Pattern 2: Comparing with Specific Person**
**Question Pattern**: "Salary same as SCOTT", "More than SMITH", "Less than ALLEN"

**Why Subquery?**: We don't know SCOTT's salary, need to fetch it first

**Solution Template**:
```sql
-- Step 1: Get person's value
SELECT SAL FROM EMP WHERE ENAME = 'SCOTT';  -- Returns: 3000

-- Step 2: Use in comparison
SELECT * FROM EMP
WHERE SAL > (SELECT SAL FROM EMP WHERE ENAME = 'SCOTT');
```

**Examples**:
```sql
-- Q: Employees with salary > MILLER
SELECT * FROM EMP
WHERE SAL > (SELECT SAL FROM EMP WHERE ENAME = 'MILLER');

-- Q: Employees in same dept as SCOTT
SELECT * FROM EMP
WHERE DEPTNO = (SELECT DEPTNO FROM EMP WHERE ENAME = 'SCOTT');

-- Q: Employees with salary between ALLEN and FORD
SELECT * FROM EMP
WHERE SAL > (SELECT SAL FROM EMP WHERE ENAME = 'ALLEN')
  AND SAL < (SELECT SAL FROM EMP WHERE ENAME = 'FORD');
```

---

#### **Pattern 3: Manager/Reporting Hierarchy**
**Question Pattern**: "Employees reporting to JONES", "BLAKE's manager", "Manager's manager"

**Why Subquery?**: Need to find manager's empno first

**Solution Template**:
```sql
-- Step 1: Get manager's EMPNO
SELECT EMPNO FROM EMP WHERE ENAME = 'JONES';  -- Returns: 7566

-- Step 2: Find employees reporting to him
SELECT * FROM EMP
WHERE MGR = (SELECT EMPNO FROM EMP WHERE ENAME = 'JONES');
```

**Examples**:
```sql
-- Q: Employees reporting to BLAKE
SELECT * FROM EMP
WHERE MGR = (SELECT EMPNO FROM EMP WHERE ENAME = 'BLAKE');

-- Q: SMITH's manager's details
SELECT * FROM EMP
WHERE EMPNO = (SELECT MGR FROM EMP WHERE ENAME = 'SMITH');

-- Q: MARTIN's manager's manager (NESTED)
SELECT * FROM EMP
WHERE EMPNO = (SELECT MGR FROM EMP
               WHERE EMPNO = (SELECT MGR FROM EMP 
                              WHERE ENAME = 'MARTIN'));

-- Q: Department name of MARTIN's manager's manager
SELECT DNAME FROM DEPT
WHERE DEPTNO = (SELECT DEPTNO FROM EMP
                WHERE EMPNO = (SELECT MGR FROM EMP
                               WHERE EMPNO = (SELECT MGR FROM EMP 
                                              WHERE ENAME = 'MARTIN')));
```

---

#### **Pattern 4: Using Aggregates (MAX, MIN, AVG)**
**Question Pattern**: "Maximum salary", "Minimum salary", "Average salary"

**Why Subquery?**: Need to calculate aggregate first, then compare

**Solution Template**:
```sql
-- Step 1: Calculate aggregate
SELECT MAX(SAL) FROM EMP;  -- Returns: 5000

-- Step 2: Use in comparison
SELECT * FROM EMP
WHERE SAL = (SELECT MAX(SAL) FROM EMP);
```

**Examples**:
```sql
-- Q: Employee with maximum salary
SELECT * FROM EMP
WHERE SAL = (SELECT MAX(SAL) FROM EMP);

-- Q: Employees earning > average salary
SELECT * FROM EMP
WHERE SAL > (SELECT AVG(SAL) FROM EMP);

-- Q: Employee with maximum salary in SALES dept
SELECT * FROM EMP
WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE DNAME = 'SALES')
  AND SAL = (SELECT MAX(SAL) FROM EMP
             WHERE DEPTNO = (SELECT DEPTNO FROM DEPT 
                             WHERE DNAME = 'SALES'));
```

---

#### **Pattern 5: Nth Maximum/Minimum Salary**
**Question Pattern**: "2nd highest", "3rd minimum", "4th maximum"

**Why Nested Subquery?**: Need to exclude previous max/min values

**Solution Template for 2nd MAX**:
```sql
-- Logic: 2nd max = MAX of (all values < 1st max)
SELECT MAX(SAL) FROM EMP
WHERE SAL < (SELECT MAX(SAL) FROM EMP);
```

**Solution Template for 3rd MAX**:
```sql
-- Logic: 3rd max = MAX of (all values < 2nd max)
SELECT MAX(SAL) FROM EMP
WHERE SAL < (SELECT MAX(SAL) FROM EMP
             WHERE SAL < (SELECT MAX(SAL) FROM EMP));
```

**Examples**:
```sql
-- Q: 2nd maximum salary
SELECT MAX(SAL) FROM EMP
WHERE SAL < (SELECT MAX(SAL) FROM EMP);

-- Q: 3rd minimum salary
SELECT MIN(SAL) FROM EMP
WHERE SAL > (SELECT MIN(SAL) FROM EMP
             WHERE SAL > (SELECT MIN(SAL) FROM EMP));

-- Q: Employee with 2nd maximum salary working in DALLAS
SELECT * FROM EMP
WHERE SAL = (SELECT MAX(SAL) FROM EMP
             WHERE SAL < (SELECT MAX(SAL) FROM EMP)
               AND DEPTNO = (SELECT DEPTNO FROM DEPT 
                             WHERE LOC = 'DALLAS'));

-- Q: Dept name of employee with 3rd max salary
SELECT DNAME FROM DEPT
WHERE DEPTNO = (SELECT DEPTNO FROM EMP
                WHERE SAL = (SELECT MAX(SAL) FROM EMP
                             WHERE SAL < (SELECT MAX(SAL) FROM EMP
                                          WHERE SAL < (SELECT MAX(SAL) 
                                                       FROM EMP))));
```

---

#### **Pattern 6: ANY and ALL Operators**
**Question Pattern**: "More than ANY SALESMAN", "Less than ALL MANAGERS", "Greater than ANY CLERK"

**Concept**:
- `> ANY` means greater than **at least one** (greater than minimum)
- `< ANY` means less than **at least one** (less than maximum)
- `> ALL` means greater than **every single one** (greater than maximum)
- `< ALL` means less than **every single one** (less than minimum)

**Solution Templates**:
```sql
-- More than ANY SALESMAN = More than minimum salesman salary
SELECT * FROM EMP
WHERE SAL > ANY (SELECT SAL FROM EMP WHERE JOB = 'SALESMAN');
-- Equivalent to:
WHERE SAL > (SELECT MIN(SAL) FROM EMP WHERE JOB = 'SALESMAN');

-- More than ALL MANAGERS = More than maximum manager salary
SELECT * FROM EMP
WHERE SAL > ALL (SELECT SAL FROM EMP WHERE JOB = 'MANAGER');
-- Equivalent to:
WHERE SAL > (SELECT MAX(SAL) FROM EMP WHERE JOB = 'MANAGER');
```

**Examples**:
```sql
-- Q: Employees earning more than ANY analyst
SELECT * FROM EMP
WHERE SAL > ANY (SELECT SAL FROM EMP WHERE JOB = 'ANALYST');

-- Q: Employees earning less than ALL managers
SELECT * FROM EMP
WHERE SAL < ALL (SELECT SAL FROM EMP WHERE JOB = 'MANAGER');

-- Q: Employees earning more than ALL clerks
SELECT * FROM EMP
WHERE SAL > ALL (SELECT SAL FROM EMP WHERE JOB = 'CLERK');
```

---

#### **Pattern 7: Department-wise Conditions with Subquery**
**Question Pattern**: "Employees earning > their dept's average", "Maximum in THEIR job"

**Why Correlated?**: Comparison is within same group

**Solution Template**:
```sql
-- Employees earning > their dept's average
SELECT * FROM EMP E1
WHERE SAL > (SELECT AVG(SAL) FROM EMP E2
             WHERE E2.DEPTNO = E1.DEPTNO);
            -- ↑ Correlated: references outer query
```

**Examples**:
```sql
-- Q: Employees earning > average of their dept
SELECT * FROM EMP E1
WHERE SAL > (SELECT AVG(SAL) FROM EMP E2
             WHERE E2.DEPTNO = E1.DEPTNO);

-- Q: Employees with highest salary in their job
SELECT * FROM EMP E1
WHERE SAL = (SELECT MAX(SAL) FROM EMP E2
             WHERE E2.JOB = E1.JOB);

-- Q: Employees in dept 20 earning > avg of dept 30
SELECT * FROM EMP
WHERE DEPTNO = 20
  AND SAL > (SELECT AVG(SAL) FROM EMP WHERE DEPTNO = 30);
```

---

#### **Pattern 8: Multiple Tables (EMP + DEPT) - Complex Subqueries**
**Question Pattern**: Questions involving both employee and department details

**Solution Template**:
```sql
-- General pattern:
SELECT [EMP columns] FROM EMP
WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE [DEPT condition]);

-- Or reverse:
SELECT [DEPT columns] FROM DEPT
WHERE DEPTNO IN (SELECT DEPTNO FROM EMP WHERE [EMP condition]);
```

**Examples**:
```sql
-- Q: Dept names ending with 'S'
SELECT * FROM EMP
WHERE DEPTNO IN (SELECT DEPTNO FROM DEPT WHERE DNAME LIKE '%S');

-- Q: Employees in dept with 2nd character 'O' in name
SELECT * FROM EMP
WHERE DEPTNO IN (SELECT DEPTNO FROM DEPT WHERE DNAME LIKE '_O%');

-- Q: Location of employees earning commission
SELECT DISTINCT LOC FROM DEPT
WHERE DEPTNO IN (SELECT DEPTNO FROM EMP 
                 WHERE COMM IS NOT NULL AND COMM > 0);

-- Q: Dept names having at least 3 salesmen
SELECT DNAME FROM DEPT
WHERE DEPTNO IN (SELECT DEPTNO FROM EMP
                 WHERE JOB = 'SALESMAN'
                 GROUP BY DEPTNO
                 HAVING COUNT(*) >= 3);

-- Q: Locations having > 4 employees
SELECT LOC FROM DEPT
WHERE DEPTNO IN (SELECT DEPTNO FROM EMP
                 GROUP BY DEPTNO
                 HAVING COUNT(*) > 4);
```

---

#### **Pattern 9: Complex Conditions with Multiple Subqueries**
**Question Pattern**: Multiple conditions, each requiring subquery

**Solution Template**:
```sql
-- Use multiple subqueries with AND/OR
SELECT * FROM EMP
WHERE condition1 = (SELECT ... FROM ... WHERE ...)
  AND condition2 > (SELECT ... FROM ... WHERE ...)
  AND condition3 IN (SELECT ... FROM ... WHERE ...);
```

**Examples**:
```sql
-- Q: Job same as SMITH, dept same as JONES, salary > TURNER
SELECT * FROM EMP
WHERE JOB = (SELECT JOB FROM EMP WHERE ENAME = 'SMITH')
  AND DEPTNO = (SELECT DEPTNO FROM EMP WHERE ENAME = 'JONES')
  AND SAL > (SELECT SAL FROM EMP WHERE ENAME = 'TURNER');

-- Q: Name starts with 'S', salary more than ALLEN, less than FORD
SELECT * FROM EMP
WHERE ENAME LIKE 'S%'
  AND SAL > (SELECT SAL FROM EMP WHERE ENAME = 'ALLEN')
  AND SAL < (SELECT SAL FROM EMP WHERE ENAME = 'FORD');

-- Q: Clerks and Analysts NOT working in DALLAS
SELECT * FROM EMP
WHERE JOB IN ('CLERK', 'ANALYST')
  AND DEPTNO NOT IN (SELECT DEPTNO FROM DEPT WHERE LOC = 'DALLAS');
```

---

#### **Pattern 10: Employees NOT Reporting to President**
**Question Pattern**: "Not reporting to PRESIDENT", "Does not report to KING"

**Why Tricky?**: President has no manager (MGR = NULL), need special handling

**Solution Template**:
```sql
-- Employees NOT directly reporting to PRESIDENT
SELECT * FROM EMP
WHERE MGR != (SELECT EMPNO FROM EMP WHERE JOB = 'PRESIDENT')
   OR MGR IS NULL;

-- Or using NOT IN (safer):
SELECT * FROM EMP
WHERE MGR NOT IN (SELECT EMPNO FROM EMP WHERE JOB = 'PRESIDENT');
```

**Examples**:
```sql
-- Q: Employees not reporting to KING directly
SELECT * FROM EMP
WHERE MGR != (SELECT EMPNO FROM EMP WHERE ENAME = 'KING')
   OR MGR IS NULL;

-- Q: Employees with commission, not reporting to president, salary > max clerk
SELECT * FROM EMP
WHERE COMM IS NOT NULL
  AND MGR NOT IN (SELECT EMPNO FROM EMP WHERE JOB = 'PRESIDENT')
  AND SAL > (SELECT MAX(SAL) FROM EMP WHERE JOB = 'CLERK');
```

---

#### **Pattern 11: First/Last Employee**
**Question Pattern**: "First employee", "Last employee", "First hired", "Last hired"

**Solution Template**:
```sql
-- First employee (earliest hiredate)
SELECT * FROM EMP
WHERE HIREDATE = (SELECT MIN(HIREDATE) FROM EMP);

-- Last employee (latest hiredate)
SELECT * FROM EMP
WHERE HIREDATE = (SELECT MAX(HIREDATE) FROM EMP);

-- Last employee by EMPNO (highest empno)
SELECT * FROM EMP
WHERE EMPNO = (SELECT MAX(EMPNO) FROM EMP);
```

**Examples**:
```sql
-- Q: First employee of company
SELECT * FROM EMP
WHERE HIREDATE = (SELECT MIN(HIREDATE) FROM EMP);

-- Q: Last employee hired
SELECT * FROM EMP
WHERE HIREDATE = (SELECT MAX(HIREDATE) FROM EMP);

-- Q: Employees joined after 2 years of first employee
SELECT * FROM EMP
WHERE HIREDATE > ADD_MONTHS((SELECT MIN(HIREDATE) FROM EMP), 24);

-- Q: Employees joined before last person
SELECT * FROM EMP
WHERE HIREDATE < (SELECT MAX(HIREDATE) FROM EMP);
```

---

#### **Pattern 12: Subquery with GROUP BY**
**Question Pattern**: Combining aggregation with subquery conditions

**Solution Template**:
```sql
-- Subquery in WHERE with GROUP BY in main query
SELECT DEPTNO, COUNT(*) FROM EMP
WHERE [subquery condition]
GROUP BY DEPTNO;

-- Subquery in HAVING clause
SELECT DEPTNO, AVG(SAL) FROM EMP
GROUP BY DEPTNO
HAVING AVG(SAL) > (SELECT AVG(SAL) FROM EMP);
```

**Examples**:
```sql
-- Q: Dept 20, 30 with annual salary, having at least 3 employees
SELECT DEPTNO, SAL * 12 AS ANNUAL_SAL FROM EMP
WHERE DEPTNO IN (20, 30)
  AND DEPTNO IN (SELECT DEPTNO FROM EMP
                 GROUP BY DEPTNO
                 HAVING COUNT(*) >= 3);

-- Q: Dept-wise min salary < average of all employees
SELECT DEPTNO, MIN(SAL) FROM EMP
GROUP BY DEPTNO
HAVING MIN(SAL) < (SELECT AVG(SAL) FROM EMP);

-- Q: Depts with avg salary > avg of dept 20
SELECT DEPTNO, AVG(SAL) FROM EMP
GROUP BY DEPTNO
HAVING AVG(SAL) > (SELECT AVG(SAL) FROM EMP WHERE DEPTNO = 20);
```

---

## 🧠 **STEP-BY-STEP PROBLEM SOLVING FRAMEWORK**

### **THE 5-STEP METHOD**

#### **STEP 1: READ & IDENTIFY KEYWORDS** 
Read question carefully and highlight key phrases:
- "EACH", "EVERY", "PER" → GROUP BY
- "MORE THAN", "AT LEAST" → HAVING
- "DEPARTMENT NAME", "LOCATION" → Subquery (DEPT table)
- "SAME AS [person]", "> [person]" → Subquery (comparison)
- "2ND MAX", "3RD MIN" → Nested subquery
- "ANY", "ALL" → Multirow subquery

#### **STEP 2: DETERMINE CONCEPT**
Ask yourself:
1. **Does it need grouping?** (EACH, PER, EVERY)
   - YES → Use GROUP BY
   
2. **Does it filter groups?** (MORE THAN, AT LEAST with aggregates)
   - YES → Use HAVING
   
3. **Does it need another table's data?** (DNAME, LOC)
   - YES → Use Subquery
   
4. **Does it compare with unknown value?** (SCOTT's salary, MAX salary)
   - YES → Use Subquery
   
5. **Is it simple row filtering?** (DEPT = 10, SAL > 1500)
   - YES → Use WHERE clause only

#### **STEP 3: BREAK DOWN THE QUERY**
Write in natural language:
```
Example: "Employees in SALES dept earning > their dept average"

Breakdown:
1. Need dept = SALES → WHERE DEPTNO = (subquery to get SALES deptno)
2. Earning > dept average → WHERE SAL > (subquery to get dept avg)
3. Combine both conditions with AND
```

#### **STEP 4: WRITE SUBQUERIES SEPARATELY**
Test each subquery independently:
```sql
-- Test 1: Get SALES deptno
SELECT DEPTNO FROM DEPT WHERE DNAME = 'SALES';  -- Returns: 30

-- Test 2: Get dept average
SELECT AVG(SAL) FROM EMP WHERE DEPTNO = 30;  -- Returns: 1566.67

-- Combine:
SELECT * FROM EMP
WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE DNAME = 'SALES')
  AND SAL > (SELECT AVG(SAL) FROM EMP 
             WHERE DEPTNO = (SELECT DEPTNO FROM DEPT 
                             WHERE DNAME = 'SALES'));
```

#### **STEP 5: VERIFY & OPTIMIZE**
- Check if query logic matches question
- Test with sample data
- Optimize if needed (avoid unnecessary subqueries)

---

### **COMMON MISTAKES TO AVOID**

#### **Mistake 1: Using WHERE instead of HAVING for aggregates**
❌ **WRONG**:
```sql
SELECT DEPTNO, COUNT(*) FROM EMP
WHERE COUNT(*) > 2  -- ERROR: Can't use aggregate in WHERE
GROUP BY DEPTNO;
```

✅ **CORRECT**:
```sql
SELECT DEPTNO, COUNT(*) FROM EMP
GROUP BY DEPTNO
HAVING COUNT(*) > 2;  -- Use HAVING for aggregates
```

---

#### **Mistake 2: Forgetting GROUP BY when using aggregates**
❌ **WRONG**:
```sql
SELECT DEPTNO, COUNT(*) FROM EMP;  -- ERROR: Missing GROUP BY
```

✅ **CORRECT**:
```sql
SELECT DEPTNO, COUNT(*) FROM EMP
GROUP BY DEPTNO;
```

---

#### **Mistake 3: Using IN instead of = for single value**
❌ **SUBOPTIMAL**:
```sql
SELECT * FROM EMP
WHERE DEPTNO IN (SELECT DEPTNO FROM DEPT WHERE DNAME = 'SALES');
-- Works but suboptimal if only one dept name
```

✅ **BETTER** (if guaranteed single result):
```sql
SELECT * FROM EMP
WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE DNAME = 'SALES');
```

---

#### **Mistake 4: Not handling NULL in MGR column**
❌ **WRONG**:
```sql
SELECT * FROM EMP
WHERE MGR != (SELECT EMPNO FROM EMP WHERE JOB = 'PRESIDENT');
-- Misses employees with MGR = NULL
```

✅ **CORRECT**:
```sql
SELECT * FROM EMP
WHERE MGR NOT IN (SELECT EMPNO FROM EMP WHERE JOB = 'PRESIDENT');
-- OR
WHERE MGR != (SELECT EMPNO FROM EMP WHERE JOB = 'PRESIDENT')
   OR MGR IS NULL;
```

---

#### **Mistake 5: Confusing ANY and ALL**
Remember:
- `> ANY` = Greater than **minimum** (at least one)
- `> ALL` = Greater than **maximum** (all of them)

---

## 📋 **QUICK REFERENCE CHEAT SHEET**

### **DECISION FLOWCHART**
```
Question has "EACH" / "PER"?
    ├─ YES → GROUP BY
    │      └─ Has "MORE THAN" / "AT LEAST"?
    │           ├─ YES → + HAVING
    │           └─ NO → Just GROUP BY
    │
    └─ NO → Check for subquery needs
           ├─ Needs DEPT table data? → Subquery
           ├─ Compares with person? → Subquery
           ├─ Uses MAX/MIN/AVG? → Subquery
           └─ Simple filter? → WHERE clause
```

### **KEYWORD TO CONCEPT MAPPING**
| **Keyword** | **Concept** | **Example** |
|------------|-------------|-------------|
| EACH, EVERY, PER | GROUP BY | "in EACH dept" |
| MORE THAN, AT LEAST (with count/sum) | HAVING | "MORE THAN 2 employees" |
| DEPARTMENT NAME, LOCATION | Subquery (DEPT) | "in SALES department" |
| SAME AS [person] | Subquery (=) | "salary same as SCOTT" |
| MORE/LESS THAN [person] | Subquery (>, <) | "earning > SMITH" |
| ANY | Subquery (ANY) | "more than ANY manager" |
| ALL | Subquery (ALL) | "less than ALL clerks" |
| 2ND MAX, 3RD MIN | Nested Subquery | "2nd highest salary" |
| REPORTING TO [name] | Subquery (MGR) | "reporting to JONES" |
| FIRST/LAST EMPLOYEE | Subquery (MIN/MAX HIREDATE) | "first employee" |

### **AGGREGATE FUNCTIONS**
- `COUNT(*)` → Number of rows
- `SUM(column)` → Total of values
- `AVG(column)` → Average of values
- `MAX(column)` → Maximum value
- `MIN(column)` → Minimum value

### **IMPORTANT ORACLE DATE FUNCTIONS**
- `TO_CHAR(HIREDATE, 'MON')` → Month name (JAN, FEB)
- `TO_CHAR(HIREDATE, 'YYYY')` → Year (1981, 1982)
- `EXTRACT(YEAR FROM HIREDATE)` → Extract year as number
- `ADD_MONTHS(date, n)` → Add n months to date

---

## 🎓 **PRACTICE QUESTIONS WITH SOLUTIONS**

### **SUBQUERY QUESTIONS - CATEGORIZED BY PATTERN**

#### **Category A: Basic Department/Location Queries**

**Q1: Display employees whose dept name ends with 'S'**
```sql
SELECT * FROM EMP
WHERE DEPTNO IN (SELECT DEPTNO FROM DEPT WHERE DNAME LIKE '%S');
```

**Q2: Employee names with max salary in ACCOUNTING dept**
```sql
SELECT ENAME FROM EMP
WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE DNAME = 'ACCOUNTING')
  AND SAL = (SELECT MAX(SAL) FROM EMP
             WHERE DEPTNO = (SELECT DEPTNO FROM DEPT 
                             WHERE DNAME = 'ACCOUNTING'));
```

**Q3: Dept name having highest commission**
```sql
SELECT DNAME FROM DEPT
WHERE DEPTNO = (SELECT DEPTNO FROM EMP
                WHERE COMM = (SELECT MAX(COMM) FROM EMP));
```

**Q4: Employees whose dept name has 2nd character 'O'**
```sql
SELECT * FROM EMP
WHERE DEPTNO IN (SELECT DEPTNO FROM DEPT WHERE DNAME LIKE '_O%');
```

**Q5: Employees in same dept as SCOTT**
```sql
SELECT * FROM EMP
WHERE DEPTNO = (SELECT DEPTNO FROM EMP WHERE ENAME = 'SCOTT');
```

**Q6: Employees in OPERATIONS and ACCOUNTING dept**
```sql
SELECT * FROM EMP
WHERE DEPTNO IN (SELECT DEPTNO FROM DEPT 
                 WHERE DNAME IN ('OPERATIONS', 'ACCOUNTING'));
```

---

#### **Category B: Salary Comparisons**

**Q7: Employees with salary > MILLER**
```sql
SELECT * FROM EMP
WHERE SAL > (SELECT SAL FROM EMP WHERE ENAME = 'MILLER');
```

**Q16: Employees whose job NOT same as ALLEN and salary > MARTIN**
```sql
SELECT * FROM EMP
WHERE JOB != (SELECT JOB FROM EMP WHERE ENAME = 'ALLEN')
  AND SAL > (SELECT SAL FROM EMP WHERE ENAME = 'MARTIN');
```

**Q34: Employees earning less than ANY salesman**
```sql
SELECT * FROM EMP
WHERE SAL < ANY (SELECT SAL FROM EMP WHERE JOB = 'SALESMAN');
-- Or:
WHERE SAL < (SELECT MAX(SAL) FROM EMP WHERE JOB = 'SALESMAN');
```

**Q36: Employees earning more than ANY manager**
```sql
SELECT * FROM EMP
WHERE SAL > ANY (SELECT SAL FROM EMP WHERE JOB = 'MANAGER');
-- Or:
WHERE SAL > (SELECT MIN(SAL) FROM EMP WHERE JOB = 'MANAGER');
```

**Q63: Employees earning more than ANY analyst**
```sql
SELECT ENAME, SAL FROM EMP
WHERE SAL > ANY (SELECT SAL FROM EMP WHERE JOB = 'ANALYST');
```

**Q108: Employees earning more than ALL managers**
```sql
SELECT * FROM EMP
WHERE SAL > ALL (SELECT SAL FROM EMP WHERE JOB = 'MANAGER');
```

---

#### **Category C: Manager/Reporting Hierarchy**

**Q9: Dept name of employees with no reporting manager**
```sql
SELECT DNAME FROM DEPT
WHERE DEPTNO IN (SELECT DEPTNO FROM EMP WHERE MGR IS NULL);
```

**Q10: Employees reporting to JONES**
```sql
SELECT * FROM EMP
WHERE MGR = (SELECT EMPNO FROM EMP WHERE ENAME = 'JONES');
```

**Q17: Employees with location same as ADAM's manager's location**
```sql
SELECT * FROM EMP
WHERE DEPTNO IN (SELECT DEPTNO FROM DEPT
                 WHERE LOC = (SELECT LOC FROM DEPT
                              WHERE DEPTNO = (SELECT DEPTNO FROM EMP
                                              WHERE EMPNO = (SELECT MGR FROM EMP
                                                             WHERE ENAME = 'ADAM'))));
```

**Q18: Job and MGR number of employees working for JONES**
```sql
SELECT JOB, MGR FROM EMP
WHERE MGR = (SELECT EMPNO FROM EMP WHERE ENAME = 'JONES');
```

**Q19: Name, hiredate, comm of FORD's manager**
```sql
SELECT ENAME, HIREDATE, COMM FROM EMP
WHERE EMPNO = (SELECT MGR FROM EMP WHERE ENAME = 'FORD');
```

**Q26: Employees reporting to BLAKE and have commission**
```sql
SELECT * FROM EMP
WHERE MGR = (SELECT EMPNO FROM EMP WHERE ENAME = 'BLAKE')
  AND COMM IS NOT NULL AND COMM > 0;
```

**Q41: MARTIN's manager's manager's dept name and location**
```sql
SELECT DNAME, LOC FROM DEPT
WHERE DEPTNO = (SELECT DEPTNO FROM EMP
                WHERE EMPNO = (SELECT MGR FROM EMP
                               WHERE EMPNO = (SELECT MGR FROM EMP
                                              WHERE ENAME = 'MARTIN')));
```

**Q81: SMITH's manager's manager's hiredate**
```sql
SELECT HIREDATE FROM EMP
WHERE EMPNO = (SELECT MGR FROM EMP
               WHERE EMPNO = (SELECT MGR FROM EMP
                              WHERE ENAME = 'SMITH'));
```

---

#### **Category D: Aggregate Functions (MAX, MIN, AVG)**

**Q13: Location of employee with minimum salary but salary > 2000**
```sql
SELECT LOC FROM DEPT
WHERE DEPTNO = (SELECT DEPTNO FROM EMP
                WHERE SAL = (SELECT MIN(SAL) FROM EMP WHERE SAL > 2000));
```

**Q20: Number of employees with salary less than BLAKE's manager's salary**
```sql
SELECT COUNT(*) FROM EMP
WHERE SAL < (SELECT SAL FROM EMP
             WHERE EMPNO = (SELECT MGR FROM EMP WHERE ENAME = 'BLAKE'));
```

**Q25: Dept name of employee with max salary and no reporting manager**
```sql
SELECT DNAME FROM DEPT
WHERE DEPTNO = (SELECT DEPTNO FROM EMP
                WHERE SAL = (SELECT MAX(SAL) FROM EMP)
                  AND MGR IS NULL);
```

**Q43: Employee details with annual salary who earn max commission**
```sql
SELECT *, SAL * 12 AS ANNUAL_SAL FROM EMP
WHERE COMM = (SELECT MAX(COMM) FROM EMP);
```

**Q55: Employees with salary > average of dept 30**
```sql
SELECT * FROM EMP
WHERE SAL > (SELECT AVG(SAL) FROM EMP WHERE DEPTNO = 30);
```

**Q65: Employee with min salary in RESEARCH dept**
```sql
SELECT ENAME FROM EMP
WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE DNAME = 'RESEARCH')
  AND SAL = (SELECT MIN(SAL) FROM EMP
             WHERE DEPTNO = (SELECT DEPTNO FROM DEPT 
                             WHERE DNAME = 'RESEARCH'));
```

---

#### **Category E: Nth Maximum/Minimum**

**Q35: 3rd minimum salary**
```sql
SELECT MIN(SAL) FROM EMP
WHERE SAL > (SELECT MIN(SAL) FROM EMP
             WHERE SAL > (SELECT MIN(SAL) FROM EMP));
```

**Q106: 2nd maximum salary**
```sql
SELECT MAX(SAL) FROM EMP
WHERE SAL < (SELECT MAX(SAL) FROM EMP);
```

**Q107: Dept name of employee with 3rd max salary**
```sql
SELECT DNAME FROM DEPT
WHERE DEPTNO = (SELECT DEPTNO FROM EMP
                WHERE SAL = (SELECT MAX(SAL) FROM EMP
                             WHERE SAL < (SELECT MAX(SAL) FROM EMP
                                          WHERE SAL < (SELECT MAX(SAL) FROM EMP))));
```

**Q70: Employee with 2nd max salary working in DALLAS**
```sql
SELECT ENAME FROM EMP
WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE LOC = 'DALLAS')
  AND SAL = (SELECT MAX(SAL) FROM EMP
             WHERE SAL < (SELECT MAX(SAL) FROM EMP
                          WHERE DEPTNO = (SELECT DEPTNO FROM DEPT 
                                          WHERE LOC = 'DALLAS'))
               AND DEPTNO = (SELECT DEPTNO FROM DEPT WHERE LOC = 'DALLAS'));
```

---

#### **Category F: GROUP BY with Subquery**

**Q8: Dept names having at least 3 salesmen**
```sql
SELECT DNAME FROM DEPT
WHERE DEPTNO IN (SELECT DEPTNO FROM EMP
                 WHERE JOB = 'SALESMAN'
                 GROUP BY DEPTNO
                 HAVING COUNT(*) >= 3);
```

**Q15: Locations having > 4 employees**
```sql
SELECT LOC FROM DEPT
WHERE DEPTNO IN (SELECT DEPTNO FROM EMP
                 GROUP BY DEPTNO
                 HAVING COUNT(*) > 4);
```

**Q60: Dept names with at least 3 but not more than 5 employees**
```sql
SELECT DNAME FROM DEPT
WHERE DEPTNO IN (SELECT DEPTNO FROM EMP
                 GROUP BY DEPTNO
                 HAVING COUNT(*) >= 3 AND COUNT(*) <= 5);
```

**Q67: Dept names having at least 3 employees**
```sql
SELECT DNAME FROM DEPT
WHERE DEPTNO IN (SELECT DEPTNO FROM EMP
                 GROUP BY DEPTNO
                 HAVING COUNT(*) >= 3);
```

**Q75: Dept-wise min salary < average salary of all employees**
```sql
SELECT DEPTNO, MIN(SAL) FROM EMP
GROUP BY DEPTNO
HAVING MIN(SAL) < (SELECT AVG(SAL) FROM EMP);
```

---

#### **Category G: Complex Multi-Condition Queries**

**Q12: Dept name of employee with name not starting with 'S' and salary 1500-3000**
```sql
SELECT DNAME FROM DEPT
WHERE DEPTNO IN (SELECT DEPTNO FROM EMP
                 WHERE ENAME NOT LIKE 'S%'
                   AND SAL BETWEEN 1500 AND 3000);
```

**Q21: Employees in CHICAGO with zero commission**
```sql
SELECT * FROM EMP
WHERE DEPTNO IN (SELECT DEPTNO FROM DEPT WHERE LOC = 'CHICAGO')
  AND (COMM = 0 OR COMM IS NULL);
```

**Q22: Employees in SALES dept with salary > dept average**
```sql
SELECT * FROM EMP
WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE DNAME = 'SALES')
  AND SAL > (SELECT AVG(SAL) FROM EMP
             WHERE DEPTNO = (SELECT DEPTNO FROM DEPT 
                             WHERE DNAME = 'SALES'));
```

**Q28: Clerks reporting to BLAKE with salary < MARTIN's salary, show dept name and location**
```sql
SELECT DNAME, LOC FROM DEPT
WHERE DEPTNO IN (SELECT DEPTNO FROM EMP
                 WHERE JOB = 'CLERK'
                   AND MGR = (SELECT EMPNO FROM EMP WHERE ENAME = 'BLAKE')
                   AND SAL < (SELECT SAL FROM EMP WHERE ENAME = 'MARTIN'));
```

**Q101: Job same as SMITH, dept same as JONES, salary > TURNER**
```sql
SELECT * FROM EMP
WHERE JOB = (SELECT JOB FROM EMP WHERE ENAME = 'SMITH')
  AND DEPTNO = (SELECT DEPTNO FROM EMP WHERE ENAME = 'JONES')
  AND SAL > (SELECT SAL FROM EMP WHERE ENAME = 'TURNER');
```

**Q102: Name starts with 'S', salary > ALLEN, salary < FORD**
```sql
SELECT * FROM EMP
WHERE ENAME LIKE 'S%'
  AND SAL > (SELECT SAL FROM EMP WHERE ENAME = 'ALLEN')
  AND SAL < (SELECT SAL FROM EMP WHERE ENAME = 'FORD');
```

**Q103: Clerks and analysts NOT working in DALLAS**
```sql
SELECT * FROM EMP
WHERE JOB IN ('CLERK', 'ANALYST')
  AND DEPTNO NOT IN (SELECT DEPTNO FROM DEPT WHERE LOC = 'DALLAS');
```

---

#### **Category H: First/Last Employee**

**Q30: Employees joined after first employee + 2 years, salary > BLAKE**
```sql
SELECT * FROM EMP
WHERE HIREDATE > ADD_MONTHS((SELECT MIN(HIREDATE) FROM EMP), 24)
  AND SAL > (SELECT SAL FROM EMP WHERE ENAME = 'BLAKE');
```

**Q35: Employees joined before last person**
```sql
SELECT * FROM EMP
WHERE HIREDATE < (SELECT MAX(HIREDATE) FROM EMP);
```

**Q37: Employees joined after first employee + 4 years, salary < BLAKE**
```sql
SELECT * FROM EMP
WHERE HIREDATE > ADD_MONTHS((SELECT MIN(HIREDATE) FROM EMP), 48)
  AND SAL < (SELECT SAL FROM EMP WHERE ENAME = 'BLAKE');
```

**Q47: Last employee record with 25% salary hike**
```sql
SELECT *, SAL * 1.25 AS HIKED_SAL FROM EMP
WHERE HIREDATE = (SELECT MAX(HIREDATE) FROM EMP);
```

**Q54: Last employee record by EMPNO**
```sql
SELECT * FROM EMP
WHERE EMPNO = (SELECT MAX(EMPNO) FROM EMP);
```

**Q115: First employee based on hiredate**
```sql
SELECT * FROM EMP
WHERE HIREDATE = (SELECT MIN(HIREDATE) FROM EMP);
```

---

#### **Category I: Advanced Complex Queries**

**Q29: Employees not reporting to president, have commission, salary > max clerk salary**
```sql
SELECT * FROM EMP
WHERE MGR NOT IN (SELECT EMPNO FROM EMP WHERE JOB = 'PRESIDENT')
  AND COMM IS NOT NULL AND COMM > 0
  AND SAL > (SELECT MAX(SAL) FROM EMP WHERE JOB = 'CLERK');
```

**Q73: Commission > max salesman salary, not reporting to KING directly**
```sql
SELECT * FROM EMP
WHERE COMM > (SELECT MAX(SAL) FROM EMP WHERE JOB = 'SALESMAN')
  AND MGR != (SELECT EMPNO FROM EMP WHERE ENAME = 'KING');
```

**Q78: Employees from dept 10 with salary > all employees in other depts**
```sql
SELECT ENAME FROM EMP
WHERE DEPTNO = 10
  AND SAL > ALL (SELECT SAL FROM EMP WHERE DEPTNO != 10);
```

**Q79: Employees earning highest salary in their respective jobs**
```sql
SELECT * FROM EMP E1
WHERE SAL = (SELECT MAX(SAL) FROM EMP E2 WHERE E2.JOB = E1.JOB);
```

**Q80: Clerk earning highest salary among clerks**
```sql
SELECT EMPNO, ENAME FROM EMP
WHERE JOB = 'CLERK'
  AND SAL = (SELECT MAX(SAL) FROM EMP WHERE JOB = 'CLERK');
```

---

## 🎯 **FINAL TIPS & TRICKS**

### **1. Always Start with Simple Queries**
Before writing complex subqueries, test individual parts:
```sql
-- Instead of writing directly:
SELECT * FROM EMP WHERE DEPTNO = (SELECT DEPTNO FROM DEPT WHERE DNAME = 'SALES');

-- First test:
SELECT DEPTNO FROM DEPT WHERE DNAME = 'SALES';  -- Returns 30
-- Then use it:
SELECT * FROM EMP WHERE DEPTNO = 30;
-- Finally combine them
```

### **2. Use Aliases for Clarity**
```sql
SELECT E.ENAME, D.DNAME
FROM EMP E, DEPT D
WHERE E.DEPTNO = D.DEPTNO;  -- Clearer than without aliases
```

### **3. Handle NULL Values Carefully**
```sql
-- NULL comparisons always return FALSE
WHERE MGR != 7839  -- Won't include MGR = NULL
-- Use:
WHERE MGR != 7839 OR MGR IS NULL
-- Or:
WHERE MGR NOT IN (7839) -- This automatically handles NULL
```

### **4. Test with Small Dataset First**
Add ROWNUM limit to test logic:
```sql
SELECT * FROM EMP
WHERE DEPTNO = 30
AND ROWNUM <= 5;  -- Test with only 5 rows
```

### **5. Use DISTINCT When Needed**
```sql
-- To avoid duplicate department names:
SELECT DISTINCT DNAME FROM DEPT
WHERE DEPTNO IN (SELECT DEPTNO FROM EMP WHERE COMM > 0);
```

### **6. Remember Order of Execution**
```
FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY
```
This helps understand why some columns can't be used in WHERE but can in HAVING.

---

## 🚀 **MASTERY CHECKLIST**

### **You've mastered GROUP BY & HAVING when you can:**
- ✅ Instantly recognize "EACH" keyword → GROUP BY
- ✅ Distinguish between WHERE (row filter) and HAVING (group filter)
- ✅ Write aggregate functions without error
- ✅ Combine WHERE, GROUP BY, and HAVING correctly
- ✅ Solve any grouping question within 2 minutes

### **You've mastered SUBQUERIES when you can:**
- ✅ Recognize when subquery is needed vs simple WHERE
- ✅ Write single-row subqueries (=, >, <)
- ✅ Write multirow subqueries (IN, ANY, ALL)
- ✅ Write nested subqueries (2nd max, 3rd min)
- ✅ Write correlated subqueries (comparing within groups)
- ✅ Solve department + employee combined questions
- ✅ Handle manager hierarchy questions
- ✅ Solve ANY complex subquery question within 5 minutes

---

## 📖 **CONCLUSION**

This guide covers:
1. ✅ Pattern recognition for all question types
2. ✅ Decision trees to choose correct concept
3. ✅ WHERE vs HAVING clarity
4. ✅ All subquery types with templates
5. ✅ 100+ solved examples categorized
6. ✅ Step-by-step solving framework
7. ✅ Common mistakes and how to avoid them

**PRACTICE STRATEGY**:
1. Start with GROUP BY questions (easier)
2. Move to basic subqueries
3. Practice nested subqueries
4. Master complex multi-condition queries
5. Time yourself - aim for 2-5 minutes per question

**Remember**: 
- Read carefully, identify keywords
- Break down complex questions
- Test subqueries independently
- Verify logic before finalizing

---

## 📞 **NEED MORE HELP?**

If stuck on any question:
1. Identify the pattern from this guide
2. Find similar solved example
3. Modify template for your question
4. Test step by step

**Happy Learning! Master SQL with confidence! 🎓**

---

*Created: 2025-10-28*  
*Version: 1.0 - Comprehensive SQL Guide*
