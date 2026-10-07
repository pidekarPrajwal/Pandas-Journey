Sure — here’s a ready-to-use Markdown file for the repo, covering the **basic knowledge of Pandas**.

 Pandas Basics

# Pandas Basics

 Pandas is a popular Python library used for **data analysis and data manipulation**. It provides easy-to-use data structures and functions for working with structured data such as CSV files, Excel sheets, databases, and JSON data.

 ## 1\. Installing Pandas

 Install Pandas using `pip`:

```
pip install pandas
```

 Import Pandas in Python:

```
import pandas as pd
```

 The `pd` alias is the standard convention used for Pandas.

---

 ## 2\. Pandas Data Structures

 Pandas mainly provides two important data structures:

 - **Series** — One-dimensional data
- **DataFrame** — Two-dimensional tabular data

 ### Series

 A Series is similar to a single column in a table.

```
import pandas as pd

numbers = pd.Series([10, 20, 30, 40])

print(numbers)
```

 Output:

```
0    10
1    20
2    30
3    40
dtype: int64
```

 You can also specify custom indexes:

```
marks = pd.Series(
    [85, 90, 78],
    index=["Alice", "Bob", "Charlie"]
)

print(marks)
```

 Access an element:

```
print(marks["Alice"])
```

---

 ## 3\. DataFrame

 A DataFrame is the most commonly used Pandas data structure.

 It represents data in rows and columns, similar to a spreadsheet or database table.

```
data = {
    "Name": ["Alice", "Bob", "Charlie"],
    "Age": [20, 21, 19],
    "Marks": [85, 90, 78]
}

df = pd.DataFrame(data)

print(df)
```

 Output:

```
      Name  Age  Marks
0    Alice   20     85
1      Bob   21     90
2  Charlie   19     78
```

---

 ## 4\. Inspecting a DataFrame

 ### View the first rows

```
df.head()
```

 By default, `head()` returns the first 5 rows.

```
df.head(3)
```

 Returns the first 3 rows.

 ### View the last rows

```
df.tail()
```

 ### Get the shape

```
df.shape
```

 Example output:

```
(3, 3)
```

 This means:

```
3 rows
3 columns
```

 ### Get column names

```
df.columns
```

 ### Get index

```
df.index
```

 ### Get data types

```
df.dtypes
```

 ### Get basic information

```
df.info()
```

 ### Get statistical summary

```
df.describe()
```

---

 ## 5\. Selecting Columns

 Select a single column:

```
df["Name"]
```

 Select multiple columns:

```
df[["Name", "Marks"]]
```

---

 ## 6\. Selecting Rows

 ### Using `loc`

 `loc` is used for label-based selection.

```
df.loc[0]
```

 Select specific rows and columns:

```
df.loc[0:1, ["Name", "Marks"]]
```

 ### Using `iloc`

 `iloc` is used for position-based selection.

```
df.iloc[0]
```

 Select the first two rows:

```
df.iloc[0:2]
```

 Select the first row and first two columns:

```
df.iloc[0, 0:2]
```

---

 ## 7\. Filtering Data

 Pandas makes it easy to filter rows based on conditions.

 For example, find students whose marks are greater than 80:

```
df[df["Marks"] > 80]
```

 Multiple conditions can be combined.

 ### AND condition

 Use `&`:

```
df[(df["Age"] > 19) & (df["Marks"] > 80)]
```

 ### OR condition

 Use `|`:

```
df[(df["Age"] == 19) | (df["Marks"] > 85)]
```

 Each condition should be wrapped in parentheses.

---

 ## 8\. Adding a Column

 You can create a new column by assigning values to it.

```
df["Passed"] = df["Marks"] >= 40
```

 You can also create calculated columns:

```
df["Marks_10"] = df["Marks"] / 10
```

---

 ## 9\. Updating a Column

 You can modify an existing column:

```
df["Age"] = df["Age"] + 1
```

 You can also update specific values:

```
df.loc[0, "Marks"] = 95
```

---

 ## 10\. Deleting Columns

 Use `drop()`:

```
df = df.drop("Marks_10", axis=1)
```

 Another common approach:

```
df.drop(columns=["Marks_10"], inplace=True)
```

 `axis=1` means columns.

 `axis=0` means rows.

 
 ## 11\. Adding Rows

 A common way to add a row is with `loc`:

```
df.loc[len(df)] = ["David", 22, 88]
```

 For larger applications, prefer combining DataFrames with `pd.concat()` rather than repeatedly adding rows.

---

 ## 12\. Handling Missing Values

 Missing data is common in real-world datasets.

 Example:

```
data = {
    "Name": ["Alice", "Bob", "Charlie"],
    "Age": [20, None, 19],
    "Marks": [85, 90, None]
}

df = pd.DataFrame(data)
```

 ### Check for missing values

```
df.isnull()
```

 Count missing values:

```
df.isnull().sum()
```

 ### Remove missing values

```
df.dropna()
```

 ### Fill missing values

```
df["Age"] = df["Age"].fillna(0)
```

 You can also fill with the mean:

```
df["Marks"] = df["Marks"].fillna(df["Marks"].mean())
```

---

 ## 13\. Sorting Data

 Sort by one column:

```
df.sort_values("Marks")
```

 Descending order:

```
df.sort_values("Marks", ascending=False)
```

 Sort by multiple columns:

```
df.sort_values(["Age", "Marks"])
```

---

 ## 14\. Reading Data from CSV

 CSV files are one of the most common data sources.

```
df = pd.read_csv("data.csv")
```

 View the data:

```
print(df.head())
```

 ### Save DataFrame to CSV

```
df.to_csv("output.csv", index=False)
```

 `index=False` prevents Pandas from writing the DataFrame index as an extra column.

---

 ## 15\. Reading Excel Files

 Read an Excel file:

```
df = pd.read_excel("data.xlsx")
```

 Write to Excel:

```
df.to_excel("output.xlsx", index=False)
```

 You may need an additional Excel engine such as `openpyxl`:

```
pip install openpyxl
```

---


---
