# DAX Coding Standards

DAX / Power BI conventions and patterns.

---

## Formatting with Variables

```dax
Revenue YTD = 
VAR _CurrentDate = MAX('Date'[Date])
VAR _YearStart = DATE(YEAR(_CurrentDate), 1, 1)
VAR _Result = 
    CALCULATE(
        [Total Revenue],
        'Date'[Date] >= _YearStart,
        'Date'[Date] <= _CurrentDate
    )
RETURN
    _Result
```

**Rules:**
- Use VAR for intermediate calculations
- Prefix variables with underscore: `_VariableName`
- One RETURN at the end
- Indent nested functions

---

## Naming Conventions

| Element | Convention | Example |
|---------|------------|---------|
| Measures | Title Case | `Total Revenue` |
| Columns | Title Case | `[Product Name]` |
| Variables | _PascalCase | `_CurrentDate` |
| Tables | Title Case | `'Sales Data'` |
| Calc Columns | Title Case | `[Full Name]` |

---

## CALCULATE Patterns

```dax
-- Basic filter modification
Revenue USA = 
CALCULATE(
    [Total Revenue],
    'Geography'[Country] = "USA"
)

-- Multiple filters (AND)
Revenue USA 2024 = 
CALCULATE(
    [Total Revenue],
    'Geography'[Country] = "USA",
    'Date'[Year] = 2024
)

-- Remove filter
Revenue All Products = 
CALCULATE(
    [Total Revenue],
    REMOVEFILTERS('Product')
)

-- Keep only specific filter
Revenue Current Product Only = 
CALCULATE(
    [Total Revenue],
    REMOVEFILTERS('Geography'),
    REMOVEFILTERS('Date')
)
```

---

## Time Intelligence

```dax
-- Year-to-Date
Revenue YTD = 
CALCULATE(
    [Total Revenue],
    DATESYTD('Date'[Date])
)

-- Previous Year
Revenue PY = 
CALCULATE(
    [Total Revenue],
    SAMEPERIODLASTYEAR('Date'[Date])
)

-- Year-over-Year Change
Revenue YoY % = 
VAR _Current = [Total Revenue]
VAR _PY = [Revenue PY]
VAR _Result = 
    DIVIDE(
        _Current - _PY,
        _PY,
        BLANK()
    )
RETURN
    _Result

-- Rolling 12 Months
Revenue R12M = 
CALCULATE(
    [Total Revenue],
    DATESINPERIOD(
        'Date'[Date],
        MAX('Date'[Date]),
        -12,
        MONTH
    )
)
```

---

## DIVIDE vs Division

```dax
-- ✅ Always use DIVIDE for division
Profit Margin = 
DIVIDE(
    [Total Profit],
    [Total Revenue],
    0  -- Default when dividing by zero
)

-- ❌ Never use raw division (can error)
Profit Margin = [Total Profit] / [Total Revenue]
```

---

## Handling BLANKs

```dax
-- Check for BLANK
Revenue Display = 
VAR _Revenue = [Total Revenue]
RETURN
    IF(
        ISBLANK(_Revenue),
        0,
        _Revenue
    )

-- Treat BLANK as zero in calculation
Total = 
VAR _Value1 = [Measure1] + 0  -- BLANK becomes 0
VAR _Value2 = [Measure2] + 0
RETURN
    _Value1 + _Value2
```

---

## Iterator Functions

```dax
-- SUMX - sum with row context
Weighted Average Price = 
DIVIDE(
    SUMX(
        'Sales',
        'Sales'[Quantity] * 'Sales'[Unit Price]
    ),
    SUM('Sales'[Quantity])
)

-- AVERAGEX - average with row context
Average Order Value = 
AVERAGEX(
    VALUES('Sales'[OrderID]),
    [Total Revenue]
)

-- MAXX/MINX
Latest Sale Date = 
MAXX(
    'Sales',
    'Sales'[Sale Date]
)
```

---

## Performance Tips

```dax
-- ✅ Use variables to avoid recalculation
Good Measure = 
VAR _Total = [Total Revenue]
RETURN
    IF(
        _Total > 1000000,
        _Total * 1.1,
        _Total
    )

-- ❌ Recalculates measure multiple times
Bad Measure = 
IF(
    [Total Revenue] > 1000000,
    [Total Revenue] * 1.1,
    [Total Revenue]
)

-- ✅ Use KEEPFILTERS when appropriate
Revenue in Context = 
CALCULATE(
    [Total Revenue],
    KEEPFILTERS('Product'[Category] = "Electronics")
)
```

---

## Common Pitfalls

```dax
-- ❌ IF with many conditions
Status = 
IF([Value] < 10, "Low",
    IF([Value] < 50, "Medium",
        IF([Value] < 100, "High", "Very High")))

-- ✅ Use SWITCH instead
Status = 
SWITCH(
    TRUE(),
    [Value] < 10, "Low",
    [Value] < 50, "Medium",
    [Value] < 100, "High",
    "Very High"
)

-- ❌ Comparing to BLANK with =
Wrong = IF([Measure] = BLANK(), ...)

-- ✅ Use ISBLANK
Correct = IF(ISBLANK([Measure]), ...)
```

---

## Documentation

```dax
-- Add comments for complex measures
/*
    Revenue YTD
    Calculates year-to-date revenue based on the current filter context.
    Uses the Date table for time intelligence.
    Returns BLANK if no dates are selected.
*/
Revenue YTD = 
VAR _CurrentDate = MAX('Date'[Date])
...
```
