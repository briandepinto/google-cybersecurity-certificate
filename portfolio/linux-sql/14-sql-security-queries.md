# SQL Security Queries: Log Analysis and Access Control

**Context:** Security investigation using employee login and machine data
**Database tables used:** `log_in_attempts`, `employees`
**Date:** [Date]
**Prepared By:** Security Analyst

---

## Query 1: After-Hours Failed Login Attempts

**Objective:** Identify all failed login attempts that occurred after business hours (after 18:00) to investigate potential unauthorized access.

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00:00'
  AND success = 0;
```

**Explanation:**
- `login_time > '18:00:00'` filters for logins occurring after 6:00 PM.
- `success = 0` filters for failed attempts only (0 = failure, 1 = success).
- The `AND` operator requires both conditions to be true.

---

## Query 2: Login Attempts on Specific Dates

**Objective:** Retrieve all login attempts from May 8 and May 9, 2022 to investigate activity around a suspected incident date.

```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09'
   OR login_date = '2022-05-08';
```

**Explanation:**
- The `OR` operator returns rows where either condition is true, capturing both dates in a single query.
- Date format follows ISO 8601 (`YYYY-MM-DD`).

---

## Query 3: Login Attempts Outside Mexico

**Objective:** Retrieve all login attempts originating from countries other than Mexico to investigate potentially suspicious foreign access.

```sql
SELECT *
FROM log_in_attempts
WHERE country NOT LIKE 'MEX%';
```

**Explanation:**
- `NOT LIKE` excludes rows matching the pattern.
- `'MEX%'` matches both `MEX` and `MEXICO` — the `%` wildcard matches any characters following `MEX`.
- This ensures both abbreviated and full country name entries are excluded.

---

## Query 4: Employees in Marketing — East Building

**Objective:** Retrieve all Marketing department employees located in East building offices for a targeted security update.

```sql
SELECT *
FROM employees
WHERE department = 'Marketing'
  AND office LIKE 'East%';
```

**Explanation:**
- `department = 'Marketing'` filters for the Marketing team.
- `office LIKE 'East%'` matches any office beginning with "East" (e.g., East-170, East-320).
- Both conditions must be satisfied — the `AND` operator is used.

---

## Query 5: Employees in Finance or Sales

**Objective:** Retrieve all employees in the Finance or Sales departments for a department-specific security patch rollout.

```sql
SELECT *
FROM employees
WHERE department = 'Finance'
   OR department = 'Sales';
```

**Explanation:**
- The `OR` operator returns rows where the employee is in either department.
- This is more efficient than running two separate queries.

---

## Query 6: Employees Not in Information Technology

**Objective:** Retrieve all employees outside the IT department to deploy a security update that IT has already received.

```sql
SELECT *
FROM employees
WHERE department NOT LIKE 'Information Technology';
```

**Explanation:**
- `NOT LIKE` excludes rows where the department matches the specified string.
- All employees in departments other than Information Technology are returned.
- An exact string match (`!=` or `<>`) could also be used here if department names are consistent: `WHERE department != 'Information Technology'`.
