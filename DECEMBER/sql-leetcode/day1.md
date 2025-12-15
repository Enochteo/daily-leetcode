## Duplicate Emails

**Understand**

Find emails appearing more than once.

**Match**

Use GROUP BY + HAVING COUNT > 1.

**Plan**

Group by email, filter groups with count > 1.

**Implement**

```sql
SELECT email
FROM Person
GROUP BY email
HAVING COUNT(email) > 1;
```

**Evaluate**

Classic duplicate-detection SQL pattern.

## Combine Two Tables

**Understand**

Return each person's name with their city/state. Missing address → NULL.

**Match**

Use LEFT JOIN from Person → Address.

**Plan**

Join on personId, select needed fields.

**_Implement_**

```sql
SELECT p.firstName, p.lastName, a.city, a.state
FROM Person p
LEFT JOIN Address a ON p.personId = a.personId;
```

**Evaluate**

## Employees Earning more than their managers

**Understand**

Find employees whose salary is greater than their manager's salary.

**Match**

Do a self-join:

e2 = employee

e1 = manager
Join on e1.id = e2.managerId.

Compare salaries.

**Plan**

Join employee table to itself.

Filter where employee salary > manager salary.

Return employee name.

**Implement**

```sql
SELECT e2.name AS Employee
FROM Employee e1
INNER JOIN Employee e2
    ON e1.id = e2.managerId
WHERE e2.salary > e1.salary;
```

**Evaluate**

Self-join pattern for hierarchical comparisons.
