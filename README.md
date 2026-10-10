

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

---

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

 ## 16\. Reading JSON

 Pandas can also work with JSON data:

```
df = pd.read_json("data.json")
```

 Save as JSON:

```
df.to_json("output.json")
```

---

 ## 17\. Handling Duplicate Data

 Find duplicate rows:

```
df.duplicated()
```

 Count duplicates:

```
df.duplicated().sum()
```

 Remove duplicates:

```
df.drop_duplicates()
```

---

 ## 18\. Renaming Columns

 Rename specific columns:

```
df.rename(
    columns={
        "Name": "Student_Name",
        "Marks": "Score"
    },
    inplace=True
)
```

---

 ## 19\. Changing Data Types

 Check data types:

```
df.dtypes
```

 Convert a column:

```
df["Age"] = df["Age"].astype(int)
```

 For safer conversion when data may contain invalid values:

```
df["Age"] = pd.to_numeric(df["Age"], errors="coerce")
```

---

 ## 20\. Grouping Data

 `groupby()` is useful for analyzing groups of data.

 Example:

```
data = {
    "Department": ["IT", "IT", "HR", "HR"],
    "Salary": [50000, 60000, 45000, 55000]
}

df = pd.DataFrame(data)
```

 Calculate the average salary by department:

```
df.groupby("Department")["Salary"].mean()
```

 Calculate multiple statistics:

```
df.groupby("Department")["Salary"].agg(
    ["mean", "min", "max"]
)
```

---

 ## 21\. Basic Aggregation Functions

 Common aggregation functions include:

```
df["Marks"].mean()
df["Marks"].sum()
df["Marks"].min()
df["Marks"].max()
df["Marks"].median()
df["Marks"].count()
```

---

 ## 22\. Value Counts

 `value_counts()` counts how frequently each value appears.

```
df["Department"].value_counts()
```

 This is useful for understanding categorical data.

---

 ## 23\. Applying Functions

 Use `apply()` when you want to apply a function to values.

```
df["Marks"] = df["Marks"].apply(lambda x: x + 5)
```

 You can also define your own function:

```
def add_bonus(marks):
    return marks + 5

df["Marks"] = df["Marks"].apply(add_bonus)
```

---

 ## 24\. Combining DataFrames

 ### Concatenation

```
df1 = pd.DataFrame({
    "Name": ["Alice", "Bob"]
})

df2 = pd.DataFrame({
    "Name": ["Charlie", "David"]
})

result = pd.concat([df1, df2], ignore_index=True)
```

 ### Merging

 `merge()` is similar to a SQL JOIN.

```
students = pd.DataFrame({
    "Student_ID": [1, 2, 3],
    "Name": ["Alice", "Bob", "Charlie"]
})

marks = pd.DataFrame({
    "Student_ID": [1, 2, 3],
    "Marks": [85, 90, 78]
})

result = pd.merge(
    students,
    marks,
    on="Student_ID"
)
```

---

 ## 25\. Resetting and Setting Index

 Set a column as the index:

```
df = df.set_index("Name")
```

 Reset the index:

```
df = df.reset_index()
```

---

 ## 26\. Basic Data Analysis Workflow

 A typical Pandas workflow looks like this:

```
import pandas as pd

# 1. Read data
df = pd.read_csv("data.csv")

# 2. Inspect data
print(df.head())
print(df.info())
print(df.describe())

# 3. Check missing values
print(df.isnull().sum())

# 4. Remove duplicates
df = df.drop_duplicates()

# 5. Filter data
filtered = df[df["Marks"] > 80]

# 6. Sort data
filtered = filtered.sort_values("Marks", ascending=False)

# 7. Save results
filtered.to_csv("filtered_data.csv", index=False)
```

---

 ## 27\. Important Pandas Functions

 | Function | Purpose |
| --- | --- |
| `pd.DataFrame()` | Create a DataFrame |
| `pd.Series()` | Create a Series |
| `pd.read_csv()` | Read CSV |
| `pd.read_excel()` | Read Excel |
| `pd.read_json()` | Read JSON |
| `df.head()` | First rows |
| `df.tail()` | Last rows |
| `df.info()` | DataFrame information |
| `df.describe()` | Statistical summary |
| `df.shape` | Rows and columns |
| `df.columns` | Column names |
| `df.dtypes` | Data types |
| `df.isnull()` | Find missing values |
| `df.dropna()` | Remove missing values |
| `df.fillna()` | Fill missing values |
| `df.drop_duplicates()` | Remove duplicates |
| `df.sort_values()` | Sort data |
| `df.groupby()` | Group data |
| `df.merge()` | Merge DataFrames |
| `pd.concat()` | Combine DataFrames |
| `df.to_csv()` | Save CSV |
| `df.to_excel()` | Save Excel |
| `df.to_json()` | Save JSON |

---

 ## 28\. Quick Example

 Here is a small complete example:

```
import pandas as pd

data = {
    "Name": ["Alice", "Bob", "Charlie", "David"],
    "Age": [20, 21, 19, 22],
    "Marks": [85, 72, 91, 65]
}

df = pd.DataFrame(data)

# Display data
print(df)

# Students with marks above 80
high_scorers = df[df["Marks"] > 80]

print(high_scorers)

# Average marks
average_marks = df["Marks"].mean()

print("Average Marks:", average_marks)

# Sort by marks
df = df.sort_values("Marks", ascending=False)

print(df)
```

---

 ## 29\. Key Concepts to Learn Next

 After learning these basics, the next useful Pandas topics are:

 - Advanced indexing with `loc` and `iloc`
- `groupby()` and advanced aggregation
- `merge()`, `join()`, and `concat()`
- Working with dates and times
- String operations
- Pivot tables
- Data cleaning
- Data transformation
- Handling large datasets
- Integration with NumPy
- Data visualization with Matplotlib and Seaborn

 ## Summary

 Pandas is mainly used to:

 1. Load data.
2. Inspect data.
3. Clean data.
4. Filter and transform data.
5. Analyze data.
6. Combine datasets.
7. Export processed data.

 The two most important Pandas objects to understand are **Series** and **DataFrame**. Once these are clear, functions such as `read_csv()`, `loc`, `iloc`, `groupby()`, `merge()`, `dropna()`, and `fillna()` form the foundation for practical data analysis with Pandas.
