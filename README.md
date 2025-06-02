# task-1
This repository contains a cleaned restaurant sales dataset along with detailed Excel-based data cleaning steps. It covers missing value imputation, validation, and formatting to prepare the data for analysis.
# 🍽️ Restaurant Sales Data Cleaning

This repository contains the cleaned version of **`RESTAURANT SALES DATA.xlsx`** and documentation of the data cleaning process.

The dataset includes restaurant sales transactions with information like order details, customer info, items, pricing, and payment methods. The goal was to clean missing or inconsistent values to make the data ready for analysis.

---

## 📁 Dataset Overview

**File:** `RESTAURANT SALES DATA.xlsx`

**Columns:**
- `Order ID` – Unique order identifier
- `Customer ID` – Unique customer identifier
- `Category` – Item category (e.g., Starters, Main Dishes)
- `Item` – Specific item ordered
- `Price` – Item price
- `Quantity` – Number of items ordered
- `Order Total` – Total cost (Price × Quantity)
- `Order Date` – Date of order
- `Payment Method` – e.g., Credit Card, Cash

🔎 A reference table (Columns K:M) contains `Category`, `Item`, and `Price` for validation.


## 🧹 Data Cleaning Steps

### 1. Filling Missing `Item` Values
- **Issue:** Some rows had missing items.
- **Fix:** Matched `Category` and `Price` with the reference table to find the correct item.
- **Formula Used:**
  ```excel
  =IF(D2<>"", D2, IFERROR(INDEX($L$2:$L$21, MATCH(1, ($K$2:$K$21=C2)*($M$2:$M$21=E2), 0)), "Unknown_" & C2))
  ```
- Items not found in the reference table were labeled like `Unknown_Desserts`.

### 2. Filling Missing `Payment Method`
- **Issue:** Some payment methods were blank.
- **Fix:** Replaced with `"Credit Card"` (most common value).
- **Formula Used:**
  ```excel
  =IF(I2<>"", I2, "Credit Card")
  ```

### 3. Removing Nulls in Critical Columns
- **Issue:** Some rows had missing `Order ID` or `Category`.
- **Fix:** Removed those rows as they are essential for analysis.

### 4. Calculating Missing `Price`, `Quantity`, or `Order Total`
- **Issue:** Some rows had one of the three values missing.
- **Fix:** Used the relationship:  
  `Order Total = Price × Quantity` to calculate the missing value.
- **Formula Used:**
  ```excel
          =E2*F2

### 5. Verifying and Correcting `Order Total`
- **Issue:** Some totals didn’t match Price × Quantity.
- **Fix:** Recalculated and corrected them.
- **Check Formula:**
  ```excel
  =IF(G2=E2*F2, "Valid", "Error")
  ```

### 6. Fixing `Order Date` Format
- **Issue:** Dates were in inconsistent formats.
- **Fix:** Standardized all to `MM/DD/YYYY`.
- **Formula Used:**
  ```excel
  =TEXT(H2, "mm/dd/yyyy")
  ```

## ✅ Output File

- **Cleaned File:** `Cleaned_Restaurant_Sales_Data.xlsx`
- **Key Fixes:**
  - All missing `Item` and `Payment Method` values handled
  - All Order Totals verified
  - Date format standardized

## 🔎 Validation Samples

- `ORD_146656` → Item: `Grilled Chicken`
- `ORD_743636` → Payment Method: `Credit Card`
- Totals match Price × Quantity
- Dates like `06/02/2025` are consistent



