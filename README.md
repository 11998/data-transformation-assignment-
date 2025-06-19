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

