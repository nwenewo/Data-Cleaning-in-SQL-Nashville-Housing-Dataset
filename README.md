# 🧹 Data Cleaning in SQL – Nashville Housing Dataset

## 📌 Project Overview

This project focuses on **data cleaning using SQL**. The dataset used is the **Nashville Housing dataset**, which contains property sales information. The goal was to prepare the raw dataset for analysis by handling missing values, standardizing formats, splitting columns, and removing duplicates.

## 🎯 Objectives

* Standardize **date formats** for consistency.
* Populate **missing property addresses**.
* Split combined columns (Address, City, State) into individual fields.
* Normalize categorical values (e.g., converting `Y/N` to `Yes/No`).
* Identify and remove **duplicate records**.
* Drop unnecessary columns for a cleaner dataset.

## 🛠️ Tools & Technologies

* **SQL Server** (T-SQL)
* **Nashville Housing Dataset**

## 🔑 Key Steps

1. **Date Standardization**

   * Converted `SaleDate` to a uniform `DATE` format.

2. **Handling Missing Data**

   * Populated `PropertyAddress` by matching records with the same `ParcelID`.

3. **Splitting Columns**

   * Extracted `PropertySplitAddress` and `PropertySplitCity` from `PropertyAddress`.
   * Split `OwnerAddress` into `OwnerSplitAddress`, `OwnerSplitCity`, and `OwnerSplitState`.

4. **Data Standardization**

   * Replaced `Y` and `N` values in `SoldAsVacant` with `Yes` and `No`.

5. **Removing Duplicates**

   * Used `ROW_NUMBER()` with `PARTITION BY` to identify duplicate rows, keeping only unique entries.

6. **Dropping Unused Columns**

   * Removed redundant fields (`OwnerAddress`, `TaxDistrict`, `PropertyAddress`, `SaleDate`) to optimize the table.

## 📊 Example Queries

```sql
-- Identify duplicate rows
WITH RowNumCTE AS (
    SELECT *,
        ROW_NUMBER() OVER (
            PARTITION BY ParcelID, PropertyAddress, SalePrice, SaleDate, LegalReference
            ORDER BY UniqueID
        ) AS row_num
    FROM PortfolioProject.dbo.NashvilleHousing
)
SELECT *
FROM RowNumCTE
WHERE row_num > 1;
```
