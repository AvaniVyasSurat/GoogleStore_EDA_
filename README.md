# Google Play Store Apps — Data Cleaning & EDA

A data cleaning and exploratory analysis project on the Google Play Store apps dataset (10,841 apps) using **Python**, **Pandas**, **Matplotlib**, and **Seaborn**, focused on handling messy real-world data: missing values, bad rows, and columns stored as text that should be numeric.

## 📊 About the Dataset

File: `4-googleplaystore.csv` — 10,841 rows × 13 columns (10,840 after cleaning).

| Column | Description |
|---|---|
| App | App name |
| Category | App category |
| Rating | User rating (out of 5) |
| Reviews | Number of reviews |
| Size | App size |
| Installs | Number of installs |
| Type | Free or Paid |
| Price | App price |
| Content Rating | Age/content rating |
| Genres | Genre(s) |
| Last Updated | Date the app was last updated |
| Current Ver | Current app version |
| Android Ver | Minimum Android version required |

**Missing values (before cleaning):** `Rating` (1,474), `Type` (1), `Content Rating` (1), `Current Ver` (8), `Android Ver` (3).

**Data cleaning performed:**
- Filled missing `Rating` with `0`.
- Filled missing `Current Ver`, `Android Ver`, and `Content Rating` with `"NA"`.
- Found and removed a corrupted row (index 10472) where a shifted/malformed record had `"Free"` in the `Installs` column instead of a number.
- Stripped `+` and `,` from `Installs` to prepare it for numeric conversion.
- Stripped `$` from `Price` to prepare it for numeric conversion.
- Binned `Rating` into 5 categories using `pd.cut()`: Very Bad, Bad, Average, Good, Very Good.

## 🎯 Purpose

To practice a realistic end-to-end data cleaning workflow on a famously messy public dataset — identifying missing values, corrupted rows, and columns that look numeric but are stored as text, and working through the cleaning steps needed before any reliable analysis can be done.

## 🛠️ Approach

1. **Load and inspect** the dataset — shape, `info()`, missing value counts.
2. **Handle missing values** — fill `Rating`, `Current Ver`, `Android Ver`, and `Content Rating`.
3. **Find and remove bad data** — locate the row with `"Free"` in the `Installs` column (a classic data-shift error) and drop it.
4. **Clean numeric-looking text columns** — strip `+`/`,` from `Installs` and `$` from `Price` in preparation for type conversion.
5. **Attempt type conversions** — convert `Installs`, `Price`, and `Reviews` to numeric types.
6. **Analyze** — unique app count, installs by category, the app with the most reviews, rating distribution via binning.

## ❓ Questions Answered

- What is the shape and structure of the raw dataset?
- Which columns have missing values, and how many?
- Which row has a data-entry error in the `Installs` column?
- How many unique apps are in the dataset?
- What do the summary statistics for `Rating` look like?
- How is `Installs` distributed across app categories?
- Which app has the highest number of reviews?
- How does the cleaned `Rating` column break down into Very Bad / Bad / Average / Good / Very Good bins?
- What is the maximum value in `Price` and `Reviews` (and why does it return a misleading result before proper type conversion)?
- Which apps are priced at exactly `$1.00`?

## 🗄️ Tech Stack

- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Seaborn**
- **Jupyter Notebook**

## 📁 Repository Structure

```
├── 4_googleplaystore.ipynb   # Notebook with code, outputs, and explanations
├── Project_Report.docx       # Full project report
└── README.md
```

## 🚀 How to Run

1. Install the requirements:
   ```
   pip install pandas numpy matplotlib seaborn jupyter
   ```
2. Place `4-googleplaystore.csv` in the working directory (update the file path in the notebook if needed — the original path points to a Google Drive mount).
3. Open and run the notebook:
   ```
   jupyter notebook 4_googleplaystore.ipynb
   ```

**Note:** Several cells in the original notebook call `.astype()` on `Installs`, `Price`, and `Reviews` without assigning the result back to the DataFrame (e.g., `store['Installs'].astype(int)` instead of `store['Installs'] = store['Installs'].astype(int)`). As a result, these columns remain as text (`object`) type throughout the rest of the notebook, which is why operations like `.max()` on `Price` return a lexicographically-sorted string (`'9.99'`) rather than the true numeric maximum. This is flagged for correction before relying on these columns for numeric analysis.

## 📌 Key Findings

- The dataset originally had **10,841 apps**; after removing one corrupted row, **10,840 apps** remain, with **9,659 unique app names**.
- **Rating** had the most missing values (**1,474**) of any column — filled with `0` for this analysis.
- A single row (index 10472) had **"Free"** mistakenly recorded in the `Installs` column due to a column-shift data error, and was dropped.
- The app with the **most reviews** is **GollerCepte Live Score** (9,992 reviews, SPORTS category, 4.2 rating).
- The average app rating (including the imputed zeros) is **~3.62**, with a true maximum of 5.0.
- Because `Price` was never converted to a true numeric type, its reported "maximum" (`'9.99'`) is a string comparison result, not a reliable numeric answer — illustrating why type conversion must be completed, not just attempted, before analysis.

---
*A data cleaning and exploratory analysis project on the Google Play Store apps dataset.*
