# Power BI ETL Project: Sales & GDP Data Analysis

## Project Overview
This Power BI ETL project consolidates sales and employee data, performs transformations, merges datasets, and computes key metrics. Additionally, it imports GDP data from a web source for contextual analysis. The setup supports **dynamic folder paths** to automatically include new monthly sales files.

---

## Data Sources

1. **Web Data:** GDP of countries.
2. **Folder Import:** Sales files (Jan, Feb, Mar, and dynamic import for new months).
3. **Excel File:** Employee data.

---

## ETL Steps and Transformations

### 1. Data Import
- Imported web GDP data.
- Folder import of sales data (Jan, Feb, Mar).  
- Employee data Excel import.

### 2. Clean and Format Data
- Removed blanks and promoted first row to headers.
- Renamed columns to meaningful names.
- Changed data types as required.

---

### 3. Text Transformations
| Function | Purpose | Example Usage |
|----------|--------|---------------|
| **UPPER()** | Uniform text format | Region column → “North / north / NORTH” → `NORTH`<br>Employee Name → uppercase all names |
| **LOWER()** | Standardize lowercase | CustomerID → `CUST001` → `cust001` |
| **TRIM()** | Remove extra spaces | Employee Name → `" Employee_1 "` → `Employee_1`<br>Region → `" North "` → `North` |
| **CLEAN()** | Remove non-printable characters | Employee Name and Region columns to fix hidden characters |

- **Replace Values:** Replaced `--` with `N/A`.
- **Split Column:** Split file format and file name from folder import.

---

### 4. Date and Derived Columns
- Extracted **Day, Month, Year, Quarter** from `OrderDate`.
- Added **Fiscal Month** column in sales data.
- Added **Age** column in employee data.

---

### 5. Conditional Columns
- Created **Sales Category** in sales data based on thresholds (e.g., High, Medium, Low).

---

### 6. Data Merging
- Merged **Sales** and **Employee** data using `Region` (Inner Join).

---

### 7. Data Appending
- Appended **Jan and Mar sales data** for consolidated analysis.

---

### 8. Aggregation
- Created a **copy of sales** table for grouping.
- Used **Group By** to compute:
  - **Total Sales** → Sum of `SalesAmount`
  - **Transaction Count** → Count of orders
  - **Average Order Value** → `TotalSales / TransactionCount`

---

### 9. Data Profiling
- Checked **Column Profile, Distribution, and Quality** in Power Query.
- Ensured consistency, completeness, and accuracy.

---

### 10. Dynamic Folder Path
- Created a **parameter** for folder path:
  - Name: `FolderPath`
  - Type: Text
  - Current Value: Folder containing sales files
- All folder queries reference this parameter.
- Credentials configured via **Data Source Settings**.

---

### 11. Monthly File Simulation
- Added **Sales_Apr.xlsx** to folder.
- Refreshed all queries.
- Verified transformations and aggregations applied automatically.

---

## Metrics Summary

| Metric            | Description                                |
|------------------|--------------------------------------------|
| TotalSales        | Sum of `SalesAmount` by Region             |
| TransactionCount  | Number of orders (`OrderID`)               |
| AvgOrderValue     | `TotalSales / TransactionCount`           |

---

## Best Practices
- Ensure consistent file structure across months.
- Refresh after adding new files.
- Use text transformations to avoid duplicates or formatting issues.
- Keep parameters updated for dynamic folder paths.

---

## Author
Aryan Dhanwani
