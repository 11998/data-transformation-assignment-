# Part 1: SQL-Based Table Comparison

## Objective
Compare two product catalog tables (`products_day1.csv` and `products_day2.csv`) to identify:
- Full rows that were **added or removed**
- **Column-level changes** (e.g., changes in `price`) for matching `product_id`s


## Input Files
- `products_day1.csv`
- `products_day2.csv`


## Steps Followed

1. **Loaded CSVs** using `pandas` and converted them into SQL tables using `sqlite3` (in-memory database).
2. **Created two SQL tables**: `products_day1` and `products_day2`.
3. **Used SQL queries** to:
   - Identify `product_id`s present in only one of the tables (added/removed rows).
   - Compare matching `product_id`s to check for changes in `price` 
4. **Generated two output result sets**:
   - A full-row difference table with a `change_type` column (`ADDED` or `REMOVED`).
   - A column-level change table showing `product_id`, `column_changed`, `old_value`, and `new_value`.

---

##  Output

### 1. Full Row Changes
| product_id | name          | category   | price | stock | change_type |
|------------|---------------|------------|-------|-------|-------------|
| 106        | Notebook      | Stationery | 2.99  | 300   | REMOVED     |
| 107        | Smart Watch   | Wearables  | 99.00 | 50    | ADDED       |

### 2. Column-Level Changes
| product_id | column_changed | old_value | new_value |
|------------|----------------|-----------|-----------|
| 101        | price          | 25.99     | 23.99     |
| 102        | stock          | 200       | 180       |
| 105        | price          | 35.00     | 37.00     |



## Folder Contents

- `products_day1.csv`
- `products_day2.csv`
- `sql_based.ipynb` – notebook containing the entire process
- `README.md` – this file


# Part 2: Python-Based Data Cleaning and Transformation

## Objective

Clean and transform messy sales data using Python:
- Validate schema and formats
- Handle missing or incorrect data
- Compute a derived column (`total_price`)

---

## Input File

**File**: `raw_sales.csv`  
Contains messy sales records with inconsistent formats.

### Sample Input:

| order_id | product_id | quantity | price_per_unit | order_date   |
|----------|------------|----------|----------------|--------------|
| 1        | 101        | "2"      | 20.00          | 2025/06/01   |
| 2        | 102        | -1       | "15.50"        | 2025-06-01   |
| "3"      | 103        | 1        | 35             | "2025-06-01" |
| 4        | 104        | 3        | 20             | 2025-06-02   |
| 5        | 105        | ""       | 99.00          | 06-03-2025   |
| 6        | 106        | 2        | 25.99          | 2025-06-03   |

---

##  Tasks Performed

1. Loaded the dataset using `pandas`
2. Created utility functions (UDFs) to:
   - Convert `order_id`, `product_id`, `quantity` to integers
   - Convert `price_per_unit` to float
   - Convert `order_date` to datetime
   - Fill blank or missing values with 0
3. Defined a UDF to compute:
   - `total_price = quantity * price_per_unit`
4. Added `total_price` column to the cleaned DataFrame
5. Saved the output as `cleaned_sales.csv`

---

## Output File

**File**: `cleaned_sales.csv`

### Sample Output:

| order_id | product_id | quantity | price_per_unit | order_date | total_price |
|----------|------------|----------|----------------|------------|-------------|
| 1        | 101        | 2        | 20.00          | 2025-06-01 | 40.00       |
| 2        | 102        | -1       | 15.50          | 2025-06-01 | -15.50      |
| 3        | 103        | 1        | 35.00          | 2025-06-01 | 35.00       |
| 4        | 104        | 3        | 20.00          | 2025-06-02 | 60.00       |
| 5        | 105        | 0        | 99.00          | 2025-06-03 | 0.00        |
| 6        | 106        | 2        | 25.99          | 2025-06-03 | 51.98       |

---



## Folder Contents

- `raw_sales.csv` – messy input data
- `python_based.py` – Python script for cleaning and transformation
- `cleaned_sales.csv` – cleaned and enriched output
- `README.md` – task summary (this file)

