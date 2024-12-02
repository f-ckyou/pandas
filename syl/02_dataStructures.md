### 2. **Pandas Data Structures (Expanded)**

Pandas revolves around two primary data structures, **Series** and **DataFrame**, which are essential for data manipulation and analysis. 
They are designed to handle large datasets efficiently and provide a wide array of functions to operate on them.

---

#### **2.1 Series**

A **Series** is a one-dimensional array-like object in Pandas that can hold any data type (integers, strings, floats, etc.) and is labeled by an index. It’s similar to a column in a spreadsheet or a database table. The index, which labels each element in the series, adds a layer of flexibility and power over regular arrays.

##### **Key Features of a Series:**
- **Homogeneous**: All elements in a `Series` must be of the same type (e.g., all integers or all floats).
- **Labeled Index**: Unlike NumPy arrays, a `Series` has an associated index that allows for easy data retrieval and manipulation.
- **Missing Data Support**: `Series` can handle missing values, represented as `NaN` (Not a Number), and offers various methods to handle or fill these gaps.
- **Vectorized Operations**: Operations on `Series` are typically vectorized, meaning that applying operations like addition, multiplication, or filtering happens element-wise across the series.

##### **2.1.1 Creating a Series**
- **From a list**:
    ```python
    import pandas as pd
    data = [10, 20, 30, 40]
    series = pd.Series(data)
    print(series)
    ```

- **From a dictionary**:
    ```python
    data = {'a': 10, 'b': 20, 'c': 30}
    series = pd.Series(data)
    print(series)
    ```

- **From scalar values (with index)**:
    ```python
    series = pd.Series(5, index=['a', 'b', 'c', 'd'])
    print(series)
    ```

##### **2.1.2 Accessing Elements in a Series**
- **Using index labels**:
    ```python
    print(series['b'])  # Access element using label
    ```

- **Using integer-based index**:
    ```python
    print(series[1])  # Access element by its position
    ```

##### **2.1.3 Operations on Series**
- **Arithmetic operations (element-wise)**:
    ```python
    series1 = pd.Series([1, 2, 3, 4])
    series2 = pd.Series([10, 20, 30, 40])
    result = series1 + series2
    print(result)
    ```

- **Filtering elements**:
    ```python
    print(series[series > 15])  # Filter elements greater than 15
    ```

##### **2.1.4 Handling Missing Data in a Series**
Pandas treats missing data using the `NaN` (Not a Number) representation. You can check for and manage missing data using various methods:

- **Identifying missing data**:
    ```python
    series = pd.Series([1, 2, None, 4])
    print(series.isnull())  # Returns True for NaN values
    ```

- **Handling missing data**:
    ```python
    series = pd.Series([1, 2, None, 4])
    filled_series = series.fillna(0)  # Replace NaN values with 0
    print(filled_series)
    ```

##### **2.1.5 Indexing in a Series**
- **Custom Index**: Pandas allows assigning meaningful labels to each element in a Series, making it easier to track and manipulate data.
    ```python
    series = pd.Series([10, 20, 30], index=['a', 'b', 'c'])
    print(series)
    ```

- **Automatic Indexing**: If no index is provided, Pandas automatically assigns integers starting from 0 as the index.
    ```python
    series = pd.Series([100, 200, 300])
    print(series)
    ```

##### **2.1.6 Additional Features**
- **Alignment**: When performing operations on two Series, Pandas automatically aligns the indexes.
    ```python
    series1 = pd.Series([1, 2, 3], index=['a', 'b', 'c'])
    series2 = pd.Series([10, 20, 30], index=['b', 'c', 'd'])
    print(series1 + series2)  # Automatic alignment by index
    ```

- **Index Uniqueness**: A `Series` index does not need to be unique; this can be useful when analyzing categorical data or repeating labels.

---

#### **2.2 DataFrame**

A **DataFrame** is a two-dimensional, size-mutable, and heterogeneous tabular data structure with labeled axes (rows and columns). It’s the most commonly used data structure in Pandas and is similar to a table in a relational database or an Excel spreadsheet.

##### **Key Features of a DataFrame:**
- **Heterogeneous Data**: Unlike a `Series`, a `DataFrame` can hold multiple data types (integers, floats, strings) across its columns.
- **Size-Mutable**: You can dynamically add or remove rows and columns without affecting the overall structure.
- **Labeled Axes**: Both rows and columns have labels, making it easy to manipulate, aggregate, and query data.
- **Missing Data Support**: Like Series, `DataFrames` also handle missing data effectively.
- **Multiple Indexes**: DataFrames support multi-level indexing (hierarchical indexing), which can make complex data analysis more intuitive.

##### **2.2.1 Creating a DataFrame**
You can create a DataFrame in multiple ways:

- **From a dictionary of lists**:
    ```python
    data = {'Name': ['Alice', 'Bob', 'Charlie'],
            'Age': [25, 30, 35],
            'Salary': [50000, 60000, 70000]}
    df = pd.DataFrame(data)
    print(df)
    ```

- **From a list of dictionaries**:
    ```python
    data = [{'Name': 'Alice', 'Age': 25}, {'Name': 'Bob', 'Age': 30}]
    df = pd.DataFrame(data)
    print(df)
    ```

- **From a NumPy array**:
    ```python
    import numpy as np
    data = np.array([[1, 2], [3, 4], [5, 6]])
    df = pd.DataFrame(data, columns=['Column1', 'Column2'])
    print(df)
    ```

##### **2.2.2 Accessing Data in a DataFrame**
- **Accessing columns**:
    ```python
    print(df['Name'])  # Returns a Series
    ```

- **Accessing rows using `.loc[]`** (label-based indexing):
    ```python
    print(df.loc[0])  # Access the first row by its index label
    ```

- **Accessing rows using `.iloc[]`** (integer-based indexing):
    ```python
    print(df.iloc[1])  # Access the second row by its position
    ```

- **Accessing both rows and columns**:
    ```python
    print(df.loc[0, 'Name'])  # Access a specific value by row and column
    ```

##### **2.2.3 DataFrame Operations**
- **Adding new columns**:
    ```python
    df['Bonus'] = [1000, 1500, 2000]  # Adds a new 'Bonus' column
    ```

- **Deleting columns**:
    ```python
    df.drop('Bonus', axis=1, inplace=True)  # Removes the 'Bonus' column
    ```

- **Renaming columns**:
    ```python
    df.rename(columns={'Name': 'Employee Name', 'Age': 'Employee Age'}, inplace=True)
    ```

##### **2.2.4 Handling Missing Data in a DataFrame**
Handling missing data in DataFrames is similar to Series:
- **Filling missing values**:
    ```python
    df['Salary'].fillna(0, inplace=True)  # Replace missing values with 0
    ```

- **Dropping rows/columns with missing values**:
    ```python
    df.dropna(inplace=True)  # Drops rows with any missing values
    ```

##### **2.2.5 DataFrame Indexing**
- **Setting a column as the index**:
    ```python
    df.set_index('Name', inplace=True)  # Set the 'Name' column as the index
    ```

- **Resetting the index**:
    ```python
    df.reset_index(inplace=True)  # Reset to default integer-based index
    ```

##### **2.2.6 Advanced Features**
- **Hierarchical Indexing (MultiIndex)**: Allows multiple levels of indexing, useful for representing complex data relationships:
    ```python
    arrays = [['Group1', 'Group1', 'Group2', 'Group2'], ['a', 'b', 'a', 'b']]
    df = pd.DataFrame({'Data': [1, 2, 3, 4]}, index=arrays)
    print(df)
    ```

- **Pivoting and Reshaping**: DataFrames support pivoting operations to reorganize data, which is especially useful for multi-dimensional analysis.

- **Efficient Operations**: Operations such as filtering, grouping, merging, and joining datasets are optimized for performance, making Pandas
