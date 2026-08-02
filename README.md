<img width="1824" height="9814" alt="bda task 3" src="https://github.com/user-attachments/assets/7e7b23ee-719f-41b4-8179-8f964ac97c20" /># Superstore Sales — Data Understanding, Cleaning & Exploratory Analysis

A data analysis project on the **Sample Superstore** dataset, covering data inspection, cleaning, feature engineering, summary statistics, and exploratory visualizations using Python (Pandas, Matplotlib, Seaborn).

---

## Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Project Structure](#project-structure)
- [Requirements](#requirements)
- [How to Run](#how-to-run)
- [Workflow](#workflow)
  - [1. Data Loading & Initial Understanding](#1-data-loading--initial-understanding)
  - [2. Data Cleaning](#2-data-cleaning)
  - [3. Feature Engineering](#3-feature-engineering)
  - [4. Summary Statistics](#4-summary-statistics)
  - [5. Exploratory Data Analysis](#5-exploratory-data-analysis)
- [Key Observations](#key-observations)
- [Author](#author)

---

## Overview

This project performs a full first-pass analysis of retail order data from a fictional superstore. The goal is to understand the shape and quality of the data, clean it where needed, and surface early insights on sales performance across categories, sub-categories, regions, and customer segments.

The analysis is implemented as a Jupyter Notebook (`Task_1_BDA.ipynb`), originally built and run in Google Colab.

## Dataset

- **File:** `samplesuperstore.csv`
- **Rows:** 10,194 orders
- **Columns:** 21

| Column | Description |
|---|---|
| `Row ID` | Unique row identifier |
| `Order ID` | Unique order identifier |
| `Order Date` | Date the order was placed |
| `Ship Date` | Date the order was shipped |
| `Ship Mode` | Shipping method (Standard Class, First Class, Second Class, Same Day) |
| `Customer ID` / `Customer Name` | Customer identifiers |
| `Segment` | Customer segment (Consumer, Corporate, Home Office) |
| `Country/Region`, `City`, `State/Province`, `Postal Code`, `Region` | Geographic details |
| `Product ID` / `Product Name` | Product identifiers |
| `Category` | Top-level product category (Furniture, Office Supplies, Technology) |
| `Sub-Category` | Product sub-category (17 unique values, e.g. Chairs, Binders, Phones) |
| `Sales` | Sale amount |
| `Quantity` | Units ordered |
| `Discount` | Discount applied |
| `Profit` | Profit earned |

No missing values or duplicate rows were found in the raw dataset.

## Project Structure

```
.
├── samplesuperstore.csv     # Raw dataset
├── Task_1_BDA.ipynb         # Main analysis notebook
└── README.md                 # Project documentation
```

## Requirements

- Python 3.8+
- pandas
- numpy
- matplotlib
- seaborn

Install dependencies:

```bash
pip install pandas numpy matplotlib seaborn
```

## How to Run

**Option A — Google Colab**
1. Upload `samplesuperstore.csv` to the Colab session (`/content/samplesuperstore.csv`).
2. Open `Task_1_BDA.ipynb` in Colab.
3. Run all cells (`Runtime > Run all`).

**Option B — Local Jupyter**
1. Place `samplesuperstore.csv` in the same directory as the notebook.
2. Update the file path in the "Load the Data" cell from `/content/samplesuperstore.csv` to `samplesuperstore.csv`.
3. Launch Jupyter and run all cells:
   ```bash
   jupyter notebook Task_1_BDA.ipynb
   ```

## Workflow

### 1. Data Loading & Initial Understanding
- Load the CSV with `pandas.read_csv`.
- Inspect the data using `.head()`, `.info()`, and `.describe()` to understand structure, data types, and value ranges.
- Confirm dataset shape and column names.

### 2. Data Cleaning
- **Missing values & duplicates:** Checked with `.isnull().sum()` and `.duplicated().sum()` — none found.
- **Datetime conversion:** `Order Date` and `Ship Date` converted from string to proper `datetime64` objects using `pd.to_datetime()`.
- **Text formatting cleanup:** `Category`, `Sub-Category`, and `Segment` are stripped of leading/trailing whitespace and standardized to title case (`.str.strip().str.title()`) to prevent inconsistent groupings from formatting variants (e.g. `" office supplies "` vs `"Office Supplies"`).

### 3. Feature Engineering
- **`Delivery Days`:** Derived as the difference in days between `Ship Date` and `Order Date`, giving a measure of fulfillment speed per order.

### 4. Summary Statistics
Computed for all key numerical attributes — `Sales`, `Quantity`, `Discount`, `Profit`, `Delivery Days`:
- Full descriptive statistics via `.describe()` (count, mean, std, min, quartiles, max).
- A condensed summary table of Mean, Median, Standard Deviation, Min, and Max for quick reference.

### 5. Exploratory Data Analysis
- **Sales by Category** — bar chart comparing total sales across Furniture, Office Supplies, and Technology.
- **Sales Distribution** — histogram (with KDE) showing the overall shape and skew of order sales values.
- **Sales by Sub-Category** — horizontal bar chart ranking all 17 sub-categories by total sales.
- **Sales by Segment** — pie chart showing sales share across Consumer, Corporate, and Home Office segments.
- **Correlation Heatmap** — correlation matrix across Sales, Quantity, Discount, Profit, and Delivery Days.

## Key Observations

- The dataset is clean out of the box: **no missing values** and **no duplicate rows**.
- Total sales by category (highest to lowest):
  1. **Technology** — ~$839.9K
  2. **Furniture** — ~$754.7K
  3. **Office Supplies** — ~$731.9K
- Sales values are **right-skewed** — most orders are lower-value, with a long tail of high-value outliers.
- Orders span four `Region`s (Central, East, South, West) and four `Ship Mode`s (Standard Class, First Class, Second Class, Same Day).
- Categorical fields were already internally consistent, but the cleaning step guards against inconsistent casing/whitespace in future data loads.

## Author

**Ganesh Ram**
Student, Kamaraj College, Thoothukudi

![Superstore Sales Analysis](<img width="1824" height="9814" alt="bda task 3" src="https://github.com/user-attachments/assets/70db10b1-cca2-4c64-baa7-5625a4d19f25" />
)

