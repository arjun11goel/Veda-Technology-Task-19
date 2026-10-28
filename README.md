# Task 19: Filter Dataset Records

## Project Overview
This project demonstrates how to retrieve and filter relevant records from a dataset using single and multiple conditional statements in **Pandas**. Using the **Titanic Dataset**, we explore basic boolean indexing, multi-condition filtering using logical operators, and standard pandas selection methods.

---

## Tools Used
* **Python 3**
* **Pandas**
* **Seaborn** (for dataset loading)
* **Jupyter Notebook**

---

## Execution & Code Examples

### 1. Load Dataset
```python
import pandas as pd
import seaborn as sns

# Load the Titanic dataset
df = sns.load_dataset('titanic')

print("Dataset Shape:", df.shape)
df.head()
```
**Output Summary:**
* **Dataset Shape:** `(891, 15)`

---

### 2. Example 1: Filtering with a Single Condition
Filter for passengers who were traveling in **First Class** (`pclass == 1`).

```python
# Filter passengers in First Class
first_class_passengers = df[df['pclass'] == 1]

print(f"Total First Class passengers: {len(first_class_passengers)}")
first_class_passengers.head()
```
**Result Summary:**
* **Total First Class passengers:** `216`

---

### 3. Example 2: Filtering with Multiple Conditions (`AND`)
Filter for passengers who were **female**, in **First Class**, AND **survived** (`sex == 'female'`, `pclass == 1`, `survived == 1`).

```python
# Filter using multiple conditions with the bitwise & operator
survived_first_class_females = df[(df['sex'] == 'female') & (df['pclass'] == 1) & (df['survived'] == 1)]

print(f"Total matching records: {len(survived_first_class_females)}")
survived_first_class_females.head()
```
**Result Summary:**
* **Total matching records:** `91`

---

### 4. Example 3: Filtering Using `.isin()` Method
Filter for passengers who embarked from either **Cherbourg ('C')** or **Queenstown ('Q')**.

```python
# Filter using .isin() method for clean OR matching
embarked_c_or_q = df[df['embarked'].isin(['C', 'Q'])]

print(f"Total matching records: {len(embarked_c_or_q)}")
embarked_c_or_q[['embarked', 'class', 'fare']].head()
```
**Result Summary:**
* **Total matching records:** `245`

---

## Interview Questions & Answers

### Q1: How do you filter rows in Pandas?
**Answer:**  
Rows in Pandas are primarily filtered using **Boolean Indexing**. You pass a condition inside square brackets (e.g., `df[df['age'] > 30]`), which returns a DataFrame containing only rows where the condition evaluates to `True`. Alternatively, `.loc[]` can be used (e.g., `df.loc[df['age'] > 30]`), which allows simultaneous filtering of rows and selection of specific columns.

### Q2: How do you combine multiple conditions?
**Answer:**  
Multiple conditions are combined using bitwise logical operators:
* **`&` (AND):** Evaluates to `True` only when all conditions are met.
* **`|` (OR):** Evaluates to `True` when at least one condition is met.
* **`~` (NOT):** Inverts the boolean condition.
* **`.isin()`:** Useful when matching a single column against a list of target values.

### Q3: Why are parentheses important in Pandas conditions?
**Answer:**  
In Python, bitwise operators (`&`, `|`, `~`) have a higher operator precedence than comparison operators (`==`, `>`, `<`, `!=`). Without surrounding each individual condition in parentheses `()`, Python evaluates the bitwise operators first, leading to a `ValueError` or logical errors in condition evaluation.
