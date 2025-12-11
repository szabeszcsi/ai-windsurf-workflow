# SQL Coding Standards

SQL Server / T-SQL conventions and patterns.

---

## Formatting

```sql
-- UPPERCASE keywords
SELECT 
    e.EmployeeID,
    e.FirstName,
    e.LastName,
    d.DepartmentName
FROM Employees AS e
INNER JOIN Departments AS d 
    ON e.DepartmentID = d.DepartmentID
WHERE e.IsActive = 1
    AND e.HireDate >= '2020-01-01'
ORDER BY e.LastName, e.FirstName;
```

**Rules:**
- Keywords: UPPERCASE
- Table/column names: PascalCase
- Aliases: lowercase, meaningful
- One column per line in SELECT
- JOIN conditions on new line, indented

---

## CTEs Over Subqueries

```sql
-- ✅ Good: CTE is readable
WITH ActiveEmployees AS (
    SELECT EmployeeID, DepartmentID, Salary
    FROM Employees
    WHERE IsActive = 1
),
DepartmentTotals AS (
    SELECT 
        DepartmentID,
        SUM(Salary) AS TotalSalary,
        COUNT(*) AS EmployeeCount
    FROM ActiveEmployees
    GROUP BY DepartmentID
)
SELECT 
    d.DepartmentName,
    dt.TotalSalary,
    dt.EmployeeCount
FROM DepartmentTotals AS dt
INNER JOIN Departments AS d 
    ON dt.DepartmentID = d.DepartmentID;

-- ❌ Bad: Nested subqueries
SELECT d.DepartmentName, sub.TotalSalary
FROM (
    SELECT DepartmentID, SUM(Salary) AS TotalSalary
    FROM (
        SELECT EmployeeID, DepartmentID, Salary
        FROM Employees
        WHERE IsActive = 1
    ) AS active
    GROUP BY DepartmentID
) AS sub
INNER JOIN Departments AS d ON sub.DepartmentID = d.DepartmentID;
```

---

## Stored Procedures

```sql
CREATE PROCEDURE [dbo].[usp_GetEmployeesByDepartment]
    @DepartmentID INT,
    @IncludeInactive BIT = 0
AS
BEGIN
    SET NOCOUNT ON;
    
    -- Validate input
    IF @DepartmentID IS NULL
    BEGIN
        RAISERROR('DepartmentID cannot be NULL', 16, 1);
        RETURN;
    END
    
    -- Main query
    SELECT 
        e.EmployeeID,
        e.FirstName,
        e.LastName,
        e.Email
    FROM Employees AS e
    WHERE e.DepartmentID = @DepartmentID
        AND (@IncludeInactive = 1 OR e.IsActive = 1)
    ORDER BY e.LastName;
END
GO
```

---

## Naming Conventions

| Object | Prefix | Example |
|--------|--------|---------|
| Tables | (none) | `Employees` |
| Views | vw_ | `vw_ActiveEmployees` |
| Stored Procedures | usp_ | `usp_GetEmployees` |
| Functions | fn_ | `fn_CalculateTax` |
| Indexes | IX_ | `IX_Employees_DepartmentID` |
| Primary Keys | PK_ | `PK_Employees` |
| Foreign Keys | FK_ | `FK_Employees_Department` |

---

## Performance Patterns

```sql
-- ✅ Use EXISTS instead of COUNT for existence check
IF EXISTS (SELECT 1 FROM Orders WHERE CustomerID = @CustomerID)
BEGIN
    ...
END

-- ❌ Don't use COUNT for existence
IF (SELECT COUNT(*) FROM Orders WHERE CustomerID = @CustomerID) > 0

-- ✅ Use specific columns
SELECT EmployeeID, FirstName, LastName FROM Employees;

-- ❌ Avoid SELECT *
SELECT * FROM Employees;

-- ✅ Use WHERE before GROUP BY to filter early
SELECT DepartmentID, COUNT(*) AS EmpCount
FROM Employees
WHERE IsActive = 1  -- Filter first
GROUP BY DepartmentID
HAVING COUNT(*) > 5;  -- Then aggregate filter
```

---

## Transactions

```sql
BEGIN TRANSACTION;
BEGIN TRY
    -- Operation 1
    UPDATE Accounts 
    SET Balance = Balance - @Amount 
    WHERE AccountID = @FromAccount;
    
    -- Operation 2
    UPDATE Accounts 
    SET Balance = Balance + @Amount 
    WHERE AccountID = @ToAccount;
    
    -- Log transaction
    INSERT INTO TransactionLog (FromAccount, ToAccount, Amount, TransactionDate)
    VALUES (@FromAccount, @ToAccount, @Amount, GETDATE());
    
    COMMIT TRANSACTION;
END TRY
BEGIN CATCH
    ROLLBACK TRANSACTION;
    
    -- Log error
    INSERT INTO ErrorLog (ErrorMessage, ErrorDate)
    VALUES (ERROR_MESSAGE(), GETDATE());
    
    -- Re-raise
    THROW;
END CATCH
```

---

## Common Pitfalls

```sql
-- ❌ Implicit conversion (kills performance)
SELECT * FROM Orders WHERE OrderID = '12345';  -- OrderID is INT

-- ✅ Use correct type
SELECT * FROM Orders WHERE OrderID = 12345;

-- ❌ Functions on indexed columns
SELECT * FROM Orders WHERE YEAR(OrderDate) = 2024;

-- ✅ Use range instead
SELECT * FROM Orders 
WHERE OrderDate >= '2024-01-01' 
  AND OrderDate < '2025-01-01';

-- ❌ Not handling NULLs
SELECT * FROM Employees WHERE ManagerID <> 5;  -- Excludes NULLs!

-- ✅ Explicit NULL handling
SELECT * FROM Employees 
WHERE ManagerID <> 5 OR ManagerID IS NULL;
```

---

## Index Hints (Use Sparingly)

```sql
-- Only when optimizer makes wrong choice AND you've verified
SELECT *
FROM Orders WITH (INDEX(IX_Orders_CustomerID))
WHERE CustomerID = @CustomerID;
```

Generally, let the optimizer decide. Only hint when you have evidence.
