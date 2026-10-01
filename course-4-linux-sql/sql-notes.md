# Course 4, Module 4 — SQL

**Status: in progress.** These are AI-assisted revision notes with newly authored examples. They are not a completed Coursera lab or a claim that the module has been passed. No database execution results are presented.

## Relational data and query structure

A relational database organizes data into tables with columns and rows. A primary key identifies a row uniquely. A foreign key can express a relationship to a key in another table. A security investigation might query sign-in records, device inventories, or account information.

`SELECT` chooses expressions or columns, `FROM` identifies a source, and `WHERE` filters rows. `ORDER BY` requests a defined sort order; without it, a particular output order is not guaranteed. Choose the columns required for the question instead of automatically exporting every field. [PostgreSQL query introduction](https://www.postgresql.org/docs/current/tutorial-select.html)

## Original practice schema

The examples assume these fictional tables. They are separate from the course's datasets and contain no actual customer or employee records:

| Table | Assumed columns |
|---|---|
| `login_events` | `event_id` (integer primary key), `user_id` (integer, may be NULL), `event_time` (timestamp), `outcome` (text), `source_ip` (text) |
| `employees` | `user_id` (integer primary key), `department` (text) |

In this example, `login_events.user_id` is an optional reference to `employees.user_id`. All timestamps are interpreted in UTC. The queries use PostgreSQL-compatible syntax; check the actual engine and schema in a lab.

### Select failed sign-ins during one day

```sql
SELECT event_id, user_id, event_time, source_ip
FROM login_events
WHERE outcome = 'failure'
  AND event_time >= TIMESTAMP '2026-09-01 00:00:00'
  AND event_time < TIMESTAMP '2026-09-02 00:00:00'
ORDER BY event_time, event_id;
```

The lower bound includes the start of the day; the exclusive upper bound stops at the next day. This avoids assuming a particular precision for the final second of a day. The result would identify records worth inspecting, not automatically prove malicious activity.

## Text, number, date, and Boolean filters

| Expression | Meaning |
|---|---|
| `outcome = 'failure'` | Exact comparison to the supplied text value |
| `event_id >= 100` | Numeric comparison |
| `department LIKE 'Support%'` | Pattern beginning with `Support`; case behavior depends on database settings and operator |
| `A AND B` | Both conditions must be true |
| `A OR B` | At least one condition must be true |
| `NOT A` | Negates a condition, with SQL NULL behavior still relevant |
| `user_id IS NULL` | Test for a missing value |

In `LIKE`, `%` matches any sequence of characters and `_` matches one character. Parentheses make combinations of `AND` and `OR` explicit. `NULL` represents a missing or unknown value; use `IS NULL` rather than `= NULL`. `WHERE` retains rows for which the condition is true; unknown is not true. [PostgreSQL pattern matching](https://www.postgresql.org/docs/current/functions-matching.html), [comparisons](https://www.postgresql.org/docs/current/functions-comparison.html)

```sql
SELECT user_id, department
FROM employees
WHERE (department = 'Support' OR department = 'Operations')
  AND user_id >= 100
ORDER BY user_id;
```

The parentheses show that the identifier condition applies to either department. A query can be syntactically valid while answering the wrong question, so read the condition in plain language before relying on it.

## Joins

An inner join returns row combinations that satisfy the join condition. A left join also retains unmatched rows from its left table, filling right-side columns with NULL. A right join retains unmatched right-side rows. If a key matches several rows, a join may produce several results; do not assume one output row per input row. [PostgreSQL join tutorial](https://www.postgresql.org/docs/current/tutorial-join.html)

```sql
SELECT l.event_id, l.event_time, l.user_id, e.department
FROM login_events AS l
LEFT JOIN employees AS e
  ON l.user_id = e.user_id
WHERE l.outcome = 'failure'
ORDER BY l.event_time, l.event_id;
```

The left join keeps failed events whose `user_id` is NULL. Such rows would have no matching employee. An inner join would omit them. In the stated schema, the employee key is unique, so each event can match at most one employee.

A condition on the right table in `WHERE`, such as `e.department = 'Support'`, would remove rows where that column is NULL. Choose the join and filter location to match the actual question. [PostgreSQL table expressions](https://www.postgresql.org/docs/current/queries-table-expressions.html)

## Completing a useful SQL lab record

Record the real schema, the question, your query, a permitted excerpt of its result, and why the result answers the question. Check date boundaries, NULLs, duplicates, and join behavior. Explain an error and its correction if one occurred.

The next portfolio milestone is the current module's filtering activity with personal outputs. These examples provide revision support; they are not that submission. [Lab template](../templates/LAB-RECORD.md)
