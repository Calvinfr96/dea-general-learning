# Pandas DataFrame Fundamentals

## Introduction to Pandas Library
- Pandas is a popular python library used for working with structured data and provides easy-to-use tools for data manipulation and analysis.
- Pandas is typically used for:
  - Handling large datasets efficiently.
  - Cleaning and transforming data.
  - Analyzing and summarizing data.
  - Working with structured and unstructured data.
- Pandas can be installed using the following command line prompt:
  ```
  pip install pandas
  ```
- Pandas can be imported in order to be used in your code as follows:
  ```
  import pandas as pd (alias optional)
  ```
- Pandas makes it easy to perform the following tasks:
  - Load data from csv files and databases.
  - Handle missing values.
  - Filter and transform data.
  - Group and summarize data.
- Example Code: Using Pandas to Create a DataFrame From a Dictionary:
  ```
  import pandas as pd

  data = {
      'Name': ['Alice', 'Bob', 'Charlie'],
      'Age': [25, 30, 35],
      'City': ['New York', 'San Francisco', 'Los Angeles']
  }

  # Create DataFrame from Dictionary
  df = pd.DataFrame(data)

  # Display the DataFrame
  print(df)
  ```

## Series Creation
- A series in pandas is a one-dimensional, labeled array that can hold data of any type, including integers, floats, strings, and objects. Each element in a series has a value and an index.
- A series in pandas is created from a list as follows:
  ```
  import pandas as pd

  data = [10, 20, 30, 40]
  index = ['a', 'b', 'c', 'd']
  series = pd.Series(data, index=index)
  print(series)

  # Output
  a    10
  b    20
  c    30
  d    40
  dtype: int64
  ```
  - The first parameter is the data that will be stored in the series and is required.
  - The second parameter is the label for each data element and is optional. The default index is a zero-based, numerical index.
- A series can also be created from a dictionary:
  ```
  import pandas as pd

  data = {'Alice': 25, 'Bob': 30, 'Charlie': 35}
  series = pd.Series(data)
  print(series)

  # Output
  Alice      25
  Bob        30
  Charlie    35
  dtype: int64
  ```
- When a series is made from a scalar value, all indexes are assigned the scalar value:
  ```
  import pandas as pd

  value = 5
  index = ['a', 'b', 'c']
  series = pd.Series(value, index=index)
  print(series)

  # Output
  a    5
  b    5
  c    5
  dtype: int64
  ```
- Accessing series properties:
  - `series.index` returns the index of the series.
  - `series.values` returns the values of the series.
  - `series.dtype` returns the data type of the series.

### Accessing Elements in a Series
- Pandas allows you to access elements in a series using either index positions (similar to python indexing) and index labels (custom labels assigned during series creation). For example:
  ```
  import pandas as pd

  data = [10, 20, 30, 40]
  series = pd.Series(data)

  # Access first element
  print(series[0]) # Outputs 10

  # Access second element
  print(series[1]) # Outputs 20
  ```
  ```
  import pandas as pd

  data = [100, 200, 300, 400]
  index = ['a', 'b', 'c', 'd']
  series = pd.Series(data, index=index)

  # Access element with label 'b'
  print(series['b']) # Outputs 200

  # Access element with label 'd'
  print(series['d']) # Outputs 400

  # Access last element
  print(series[-1]) # Will fail since this only works with numerical indexing. Custom indexing was assigned in this case.
  ```
- You can access multiple elements within a series using a list of indexes. For example:
  ```
  import pandas as pd

  data = [100, 200, 300, 400]
  index = ['a', 'b', 'c', 'd']
  series = pd.Series(data, index=index)

  # Access elements with labels 'a' and 'c'
  print(series[['a', 'c']]) # Note the double brackets. You need to pass the indexes as one list, not multiple arguments.

  # Output
  a    100
  c    300
  dtype: int64
  ```
- A portion of a series can be extracted using the `[start:stop]` syntax similar to python. For example:
  ```
  import pandas as pd

  data = [10, 20, 30, 40, 50]
  series = pd.Series(data)

  # Slice from index 1 to 3
  print(series[1:4])

  # Output
  1    20
  2    30
  3    40
  dtype: int64
  ```
  ```
  import pandas as pd

  data = [100, 200, 300, 400]
  index = ['a', 'b', 'c', 'd']
  series = pd.Series(data, index=index)

  # Slice from label 'b' to 'd'
  print(series['b':'d'])

  # Output
  b    200
  c    300
  d    400
  dtype: int64 # Note that, when using custom indexing, the output includes the ending index.
  ```
- Data can be filtered from a series as follows:
  ```
  import pandas as pd

  data = [10, 20, 30, 40, 50]
  series = pd.Series(data)

  # Select values greater than 25
  print(series[series > 25])

  # Output
  2    30
  3    40
  4    50
  dtype: int64
  ```
- The `get()` method can also be used to access elements in a series. It will return `None` if the index is not found, instead of throwing an error. For example:
  ```
  import pandas as pd

  data = [10, 20, 30, 40]
  index = ['a', 'b', 'c', 'd']
  series = pd.Series(data, index=index)

  # Get value with label 'b'
  print(series.get('b')) # Outputs 20

  # Attempt to get value with label 'x' (returns None)
  print(series.get('x')) # Outputs None
  ```
- Comprehensive Example:
  ```
  import pandas as pd

  numbers = [5, 10, 15, 20, 25]
  numbers_series = pd.Series(numbers)

  first = numbers_series[0]
  last = numbers_series[len(numbers_series) -1]
  elements = numbers_series[[1, 3]] # Accesses elements 2 and 4
  elements = numbers_series[1:4] # Accesses the elements, 2, 3, and 4
  print(first)
  print(last)
  print(elements)

  fruits = {'apple': 100, 'banana': 50, 'orange': 80}
  fruits_series = pd.Series(fruits)

  banana = fruits_series['banana']
  sliced = fruits_series['banana':'orange']
  values = fruits_series[fruits_series > 70]
  apple = fruits_series.get('apple')
  mango = fruits_series.get('mango')
  print(banana)
  print(sliced)
  print(values)
  print(apple)
  print(mango)
  ```

### Operations on a Series
- Pandas allows you to perform a wide range of operations directly on a series, including mathematical, statistical, and element-wise operations.
- Mathematical Operations:
  ```
  import pandas as pd

  data = [10, 20, 30, 40]
  series = pd.Series(data)

  # Add 5 to each element
  result = series + 5
  print(result)

  # Output
  0    15
  1    25
  2    35
  3    45
  dtype: int64
  ```
  ```
  import pandas as pd

  data = [10, 20, 30, 40]
  series = pd.Series(data)

  # Divide each element by 5
  result = series / 5
  print(result) # The division converts the int to a float

  # Output
  0    2.0
  1    4.0
  2    6.0
  3    8.0
  dtype: float64
  ```
- Statistical Operations:
  ```
  import pandas as pd

  data = [10, 20, 30, 40]
  series = pd.Series(data)

  # Calculate the mean of the Series
  mean = series.mean()
  print(mean) # Outputs 25.0

  # Calculate the sum of all elements
  total = series.sum()
  print(total) # Outputs 100

  # Get the minimum and maximum values
  minimum = series.min()
  maximum = series.max()
  print(minimum, maximum) # Outputs 10 40

  # Count the number of elements
  count = series.count()
  print(count) # Outputs 4

  # Calculate the standard deviation
  std_dev = series.std()
  print(std_dev) # Outputs 12.909944487358056

  # Calculate the median
  median = series.median()
  print(median) # Outputs 25.0
  ```
- Element-Wise Operations:
  ```
  import pandas as pd

  data = [10, 20, 30, 40]
  series = pd.Series(data)

  # Double each value using apply()
  result = series.apply(lambda x: x * 2)
  print(result)

  # Output
  0    20
  1    40
  2    60
  3    80
  dtype: int64

  # Square each value using map()
  result = series.map(lambda x: x ** 2)
  print(result)

  # Output
  0     100
  1     400
  2     900
  3    1600
  dtype: int64

  # Replace values in a Series
  result = series.replace({10: 100, 30: 300})
  print(result)

  # Output
  0    100
  1     20
  2    300
  3     40
  dtype: int64
  ```
  - The `apply()` method accepts an anonymous function that will be applied to each element in the series.
  - The `map()` method also accepts an anonymous function that will be applied to each element in the series. The primary differences between `apply()` and `map()` are:
    - `map()` only works on series while `apply()` works on series and data frames.
    - `map()` accepts functions, dictionaries, and series while `apply()` only accepts functions.
    - `map()` performs element-wise transformations and substitutions while `apply()` can also perform more complex aggregations.
    - `map()` performs faster for simple, element-wise operations on a series or dictionary.
- Operations Between Series:
  ```
  import pandas as pd

  series1 = pd.Series([1, 2, 3, 4])
  series2 = pd.Series([10, 20, 30, 40])

  # Add two Series
  result = series1 + series2
  print(result)

  # Output
  0    11
  1    22
  2    33
  3    44
  dtype: int64
  ```
  - Series must be the same length to perform these operations.
- Comprehensive Example:
  ```
  import pandas as pd

  numbers = [2, 4, 6, 8, 10]
  numbers_series = pd.Series(numbers)

  add_5 = numbers_series + 5
  print(add_5)

  multiply_3 = numbers_series * 3
  print(multiply_3)

  mean = numbers_series.mean()
  std_dev = numbers_series.std()
  print(mean)
  print(std_dev)

  series1 = pd.Series([10, 20, 30])
  series2 = pd.Series([5, 15, 25])
  series_sum = series1 + series2
  print(series_sum)

  series3 = pd.Series([10, 20, 30, 40])
  square_series3 = series3.apply(lambda x: x ** 2)
  modify_series3 = series3.replace({20: 200})
  print(square_series3)
  print(modify_series3)
  ```

## DataFrame Creation
- A data frame is a two-dimensional, labeled data structure similar to a table in a relational database or spreadsheet.
  - Rows and columns have labels (index and column names).
  - Can hold different data types.
  - Missing values are handled as `NaN`.
- A data frame consists of:
  - Index - Acts as a label for rows.
  - Column - The column labels.
  - Data - The values stored in the table.
- Example:
  ```
  Index	Name	   Age	City
  0	    Alice	   25	  New York
  1	    Bob	     30	  Chicago
  2	    Charlie	 35	  Boston
  ```
- The syntax for creating a data frame in pandas is as follows:
  ```
  pd.DataFrame(data, index=[row labels], columns=[column labels])
  ```
  - `data` - Data from the list, dictionary, or array.
  - `index` - Labels for the rows (optional). Zero-based index label by default.
  - `columns` - Labels for the columns (optional). Zero-based index label by default.
- DataFrame Creation Example:
  ```
  import pandas as pd

  data = [[1, 'Alice', 25], [2, 'Bob', 30], [3, 'Charlie', 35]]
  df = pd.DataFrame(data, columns=['ID', 'Name', 'Age'])
  print(df)

  # Output
    ID     Name  Age
  0   1    Alice   25
  1   2      Bob   30
  2   3  Charlie   35
  ```
  ```
  import pandas as pd

  data = {
      'ID': [1, 2, 3],
      'Name': ['Alice', 'Bob', 'Charlie'],
      'Age': [25, 30, 35]
  }
  df = pd.DataFrame(data)
  print(df)

  # Output
    ID     Name  Age
  0   1    Alice   25
  1   2      Bob   30
  2   3  Charlie   35
  ```
  ```
  import pandas as pd

  data = [
      {'ID': 1, 'Name': 'Alice', 'Age': 25},
      {'ID': 2, 'Name': 'Bob', 'Age': 30},
      {'ID': 3, 'Name': 'Charlie', 'Age': 35}
  ]
  df = pd.DataFrame(data)
  print(df)

  # Output
    ID     Name  Age
  0   1    Alice   25
  1   2      Bob   30
  2   3  Charlie   35
  ```
  ```
  import pandas as pd
  import numpy as np

  data = np.array([[1, 'Alice', 25], [2, 'Bob', 30], [3, 'Charlie', 35]])
  df = pd.DataFrame(data, columns=['ID', 'Name', 'Age'])
  print(df)

  # Output
    ID     Name Age
  0  1    Alice  25
  1  2      Bob  30
  2  3  Charlie  35
  ```
  ```
  import pandas as pd

  data = pd.Series([100, 200, 300], index=['a', 'b', 'c'])
  df = pd.DataFrame(data, columns=['Value'])
  print(df)

  # Output
    Value
  a    100
  b    200
  c    300
  ```
- Defining Custom Index and Columns:
  ```
  import pandas as pd

  data = [[1, 'Alice', 25], [2, 'Bob', 30], [3, 'Charlie', 35]]
  df = pd.DataFrame(data, index=['row1', 'row2', 'row3'], columns=['ID', 'Name', 'Age'])
  print(df)

  # Output
        ID     Name  Age
  row1    1    Alice   25
  row2    2      Bob   30
  row3    3  Charlie   35
  ```
- Adding Columns to an Existing DataFrame:
  ```
  df['City'] = ['New York', 'Chicago', 'Boston']
  print(df)

  # Output
        ID     Name  Age      City
  row1    1    Alice   25  New York
  row2    2      Bob   30   Chicago
  row3    3  Charlie   35    Boston
  ```
- Adding Rows to an Existing DataFrame:
  ```
  df.loc['row4'] = [4, 'David', 28, 'Seattle']
  print(df)

  # Output
        ID     Name  Age      City
  row1    1    Alice   25  New York
  row2    2      Bob   30   Chicago
  row3    3  Charlie   35    Boston
  row4    4    David   28   Seattle
  ```
- Deleting a Column:
  ```
  df.drop('City', axis=1, inplace=True)
  print(df)

  # Output
        ID     Name  Age
  row1    1    Alice   25
  row2    2      Bob   30
  row3    3  Charlie   35
  row4    4    David   28
  ```
- Deleting a Row:
  ```
  df.drop('row4', axis=0, inplace=True)
  print(df)

  # Output
        ID     Name  Age
  row1    1    Alice   25
  row2    2      Bob   30
  row3    3  Charlie   35
  ```
- Comprehensive Example:
  ```
  import pandas as pd

  people = [[101, 'John', 29], [102, 'Anna', 25], [103, 'Peter', 32]]
  people_frame = pd.DataFrame(people, columns=['ID', 'Name', 'Age'])
  people_frame['City'] = ['NY', 'LA', 'Chicago']
  print(people_frame)

  products = {'Product': ['A', 'B', 'C'], 'Price': [100, 200, 150]}
  products_frame = pd.DataFrame(products)
  products_frame.loc[3] = ['D', 180]
  products_frame.drop(2, axis=0, inplace=True)
  print(products_frame)
  ```

### Removing Duplicates
- A duplicate row in a data frame refers to two or more rows that match **exactly** with one another. Duplicate rows can be identified using the `duplicated()` method as follows:
  ```
  DataFrame.duplicated(subset=None, keep='first')
  ```
  - `subset` refers to the list of columns to check for duplicates (all columns by default).
  - `keep` refers to the occurrence that should be kept (marked as `False`. `first` by default). `first` keeps the first occurrence. `last` keeps the last occurrence. `False` marks all duplicates as `True`.
- Identifying Duplicates in a DataFrame:
  ```
  import pandas as pd

  data = {
      'ID': [1, 2, 1, 3, 4, 4],
      'Name': ['Alice', 'Bob', 'Alice', 'Charlie', 'David', 'David'],
      'Age': [25, 30, 25, 35, 40, 40]
  }

  df = pd.DataFrame(data)

  # Identify duplicates
  print(df.duplicated()) # subset = None, keep='first' by default.

  # Output
  0    False
  1    False
  2     True
  3    False
  4    False
  5     True
  dtype: bool
  ```
  ```
  # Check for duplicates based only on the 'Name' column
  print(df.duplicated(subset=['Name'])) # keep='first' by default.

  # Output
  0    False
  1    False
  2     True
  3    False
  4    False
  5     True
  dtype: bool
  ```
  ```
  # Mark all but the last occurrence as duplicate
  print(df.duplicated(keep='last'))

  # Output
  0     True
  1    False
  2    False
  3    False
  4     True
  5    False
  dtype: bool
  ```
- Duplicate rows can in a data frame be removed using the `drop_duplicates()` method as follows:
  ```
  DataFrame.drop_duplicates(subset=None, keep='first', inplace=False)
  ```
  - `subset` refers to the list of columns to check for duplicates (all columns by default).
  - `keep` refers to the occurrence that should be kept (marked as `False`. `first` by default). `first` keeps the first occurrence. `last` keeps the last occurrence. `False` marks all duplicates as `True`.
  - `inplace` refers to the modification of the data frame (`False` by default). `True`modifies the data frame directly.
- Removing Duplicates in a DataFrame:
  ```
  import pandas as pd

  data = {
      'ID': [1, 2, 1, 3, 4, 4],
      'Name': ['Alice', 'Bob', 'Alice', 'Charlie', 'David', 'David'],
      'Age': [25, 30, 25, 35, 40, 40]
  }

  df = pd.DataFrame(data)

  # Remove all duplicate rows
  df_cleaned = df.drop_duplicates()
  print(df_cleaned)

  # Output
    ID     Name  Age
  0   1    Alice   25
  1   2      Bob   30
  3   3  Charlie   35
  4   4    David   40
  ```
  ```
  # Remove duplicates based on the 'Name' column
  df_cleaned = df.drop_duplicates(subset=['Name'])
  print(df_cleaned)

  # Output
    ID     Name  Age
  0   1    Alice   25
  1   2      Bob   30
  3   3  Charlie   35
  4   4    David   40
  ```
  ```
  # Remove duplicates based on 'Name' and 'Age'
  df_cleaned = df.drop_duplicates(subset=['Name', 'Age'])
  print(df_cleaned)

  # Output
    ID     Name  Age
  0   1    Alice   25
  1   2      Bob   30
  3   3  Charlie   35
  4   4    David   40
  ```
  ```
  # Keep the last occurrence of duplicates
  df_cleaned = df.drop_duplicates(keep='last')
  print(df_cleaned)

  # Output
    ID     Name  Age
  1   2      Bob   30
  2   1    Alice   25
  3   3  Charlie   35
  5   4    David   40
  ```
  ```
  # Remove all instances of duplicates
  df_cleaned = df.drop_duplicates(keep=False)
  print(df_cleaned)

  # Output
    ID     Name  Age
  1   2      Bob   30
  3   3  Charlie   35
  ```
- Duplicate rows in a data frame can be counted using the `sum()` function as follows:
  ```
  # Count the number of duplicates
  num_duplicates = df.duplicated().sum()
  print(f"Number of duplicate rows: {num_duplicates}") # Outputs 2 for the 2 sets of duplicate rows
  ```
- Comprehensive Example:
  ```
  import pandas as pd

  data = {
      'ID': [1, 2, 1, 3, 2],
      'Name': ['Alice', 'Bob', 'Alice', 'Charlie', 'Bob'],
      'Age': [25, 30, 25, 35, 30],
      'City': ['New York', 'Chicago', 'New York', 'Boston', 'Chicago']
  }

  df = pd.DataFrame(data)
  duplicates = df.duplicated()
  df_cleaned = df.drop_duplicates()
  df_cleaned_name = df.drop_duplicates(subset=['Name'], keep='last')
  duplicate_count = df.duplicated().sum()

  print(duplicates)
  print(df_cleaned)
  print(df_cleaned_name)
  print(duplicate_count)
  ```

## Slicing and Indexing
- Slicing and indexing are methods used to access specific rows, columns, or subsets of data in a data frame or series.
- Indexing allows you to access elements or specific groups of elements using row and column labels or numeric positions.
- Slicing allows you to access a range of rows or columns in a data frame or series.
- Selecting a Single Column:
  ```
  import pandas as pd

  data = {
      'Name': ['Alice', 'Bob', 'Charlie', 'David'],
      'Age': [25, 30, 35, 40],
      'City': ['New York', 'Chicago', 'Boston', 'Seattle']
  }

  df = pd.DataFrame(data)

  # Select a single column
  print(df['Name'])

  # Using dot notation
  print(df.Age)

  # Output
  0     Alice
  1       Bob
  2   Charlie
  3     David
  Name: Name, dtype: object

  0    25
  1    30
  2    35
  3    40
  Name: Age, dtype: int64
  ```
- Selecting Multiple Columns:
  ```
  # Select multiple columns
  print(df[['Name', 'Age']])

  # Output
        Name  Age
  0    Alice   25
  1      Bob   30
  2  Charlie   35
  3    David   40
  ```
- Selecting a Row by Index:
  ```
  # Select the first row using iloc
  print(df.iloc[0])

  # Select row using label with loc
  print(df.loc[0])

  # Output
  Name       Alice
  Age           25
  City    New York
  Name: 0, dtype: object
  ```
  - The `iloc[]` method allows you to slice rows or columns using the numeric index position.
  - The `loc[]` method allows you to slice rows or columns using labels.
- Slicing Rows by Index Position:
  ```
  # Slice rows from index 1 to 2 (excludes index 3)
  print(df.iloc[1:3])

  # Output
        Name  Age    City
  1      Bob   30  Chicago
  2  Charlie   35   Boston
  ```
- Slicing Rows by Labels:
  ```
  # Slice rows from label 1 to 2 (inclusive)
  print(df.loc[1:2])

  # Output
        Name  Age    City
  1      Bob   30  Chicago
  2  Charlie   35   Boston
  ```
- Slicing Columns by Position:
  ```
  # Slice the first two columns
  print(df.iloc[:, 0:2])

  # Output
        Name  Age
  0    Alice   25
  1      Bob   30
  2  Charlie   35
  3    David   40
  ```
- Slicing Columns by Labels:
  ```
  # Slice specific columns by label
  print(df.loc[:, ['Name', 'City']])

  # Output
        Name      City
  0    Alice  New York
  1      Bob   Chicago
  2  Charlie    Boston
  3    David   Seattle
  ```
- Conditional Selection of Rows:
  ```
  # Select rows where Age > 30
  print(df[df['Age'] > 30])

  # Output
        Name  Age    City
  2  Charlie   35   Boston
  3    David   40  Seattle
  ```
  ```
  # Select rows where Age > 30 AND City is Boston
  print(df[(df['Age'] > 30) & (df['City'] == 'Boston')])

  # Output
        Name  Age    City
  2  Charlie   35   Boston
  ```
- The `isin()` method can be used to match values from a list. For example:
  ```
  # Select rows where City is in ['Chicago', 'Boston']
  print(df[df['City'].isin(['Chicago', 'Boston'])])

  # Output
        Name  Age    City
  1      Bob   30  Chicago
  2  Charlie   35   Boston
  ```
- The index of a data frame can be reset using the `reset_index()` method as follows:
  ```
  # Reset index
  df.reset_index(drop=True, inplace=True)
  print(df)
  ```
- The index of a data frame can be set using the `set_index()` method as follows:
  ```
  # Set 'Name' as the index
  df.set_index('Name', inplace=True)
  print(df)

  # Output
  Name    Age      City
                   
  Alice     25  New York
  Bob       30   Chicago
  Charlie   35    Boston
  David     40   Seattle
  ```
- Rows can be filtered using the `query()` method as follows:
  ```
  # Select rows where Age > 30
  print(df.query('Age > 30'))

  # Output
  Name     Age    City
                
  Charlie   35   Boston
  David     40  Seattle
  ```
- Comprehensive Example:
  ```
  import pandas as pd

  data = {
      'Name': ['Alice', 'Bob', 'Charlie', 'David'],
      'Age': [25, 30, 35, 40],
      'City': ['New York', 'Chicago', 'Boston', 'Seattle']
  }

  df = pd.DataFrame(data)
  ages = df.Age
  rows1_3 = df.iloc[1:3]
  rows_age_over_30 = df[df['Age'] > 30]
  names_and_cities = df.iloc[:, [0, 2]]
  filtered_rows = df[df['City'].isin(['Boston', 'Chicago'])]
  print(ages)
  print(rows1_3)
  print(rows_age_over_30)
  print(names_and_cities)
  print(filtered_rows)
  ```

## Indexing Operations
- Indexing in pandas allows you to select specific rows and columns from a data frame or series using labels or numeric positions.
- The `loc[]` method allows you to select rows and columns using **label-based** indexing. It includes the start and end index in slicing. This method also supports boolean indexing or conditional selection. The syntax is as follows:
  ```
  DataFrame.loc[row_label, column_label]
  ```
- Selecting Rows and Columns by Label:
  ```
  import pandas as pd

  data = {
      'Name': ['Alice', 'Bob', 'Charlie', 'David'],
      'Age': [25, 30, 35, 40],
      'City': ['New York', 'Chicago', 'Boston', 'Seattle']
  }

  df = pd.DataFrame(data, index=['a', 'b', 'c', 'd'])

  # Select a single row using loc
  print(df.loc['a'])

  # Output
  Name       Alice
  Age           25
  City    New York
  Name: a, dtype: object

  # Select multiple rows using loc
  print(df.loc[['a', 'c']])

  # Output
        Name  Age      City
  a    Alice   25  New York
  c  Charlie   35    Boston

  # Select rows 'a' and 'c' and columns 'Name' and 'Age'
  print(df.loc[['a', 'c'], ['Name', 'Age']])

  # Output
        Name  Age
  a    Alice   25
  c  Charlie   35

  # Slice rows from 'b' to 'd' and select columns from 'Name' to 'Age'
  print(df.loc['b':'d', 'Name':'Age'])

  # Output
        Name  Age
  b      Bob   30
  c  Charlie   35
  d    David   40

  # Select rows where Age > 30
  print(df.loc[df['Age'] > 30])

  # Output
        Name  Age    City
  c  Charlie   35  Boston
  d    David   40  Seattle
  ```
- The `iloc[]` method allows you to select rows and columns based on their **integer position**. Indexes start at zero and the end index is excluded. The syntax is as follows:
  ```
  DataFrame.iloc[row_index, column_index]
  ```
- Selecting Rows and Columns by Index:
  ```
  # Select the first row
  print(df.iloc[0])

  # Output
  Name       Alice
  Age           25
  City    New York
  Name: a, dtype: object

  # Select the first and third rows
  print(df.iloc[[0, 2]])

  # Output
        Name  Age    City
  a    Alice   25  New York
  c  Charlie   35   Boston

  # Select the first and third rows and the first two columns
  print(df.iloc[[0, 2], [0, 1]])

  # Output
        Name  Age
  a    Alice   25
  c  Charlie   35

  # Slice rows from index 1 to 3 and columns from index 0 to 2
  print(df.iloc[1:3, 0:2])

  # Output
        Name  Age
  b      Bob   30
  c  Charlie   35

  # Select rows where Age > 30 using iloc
  print(df.iloc[(df['Age'] > 30).values])

  # Output
        Name  Age    City
  c  Charlie   35  Boston
  d    David   40  Seattle
  ```
  - You cannot use direct conditional selection with `iloc[]`, but you can combine `iloc[]` with boolean indexing.
- Differences Between `loc[]` and `iloc[]`:
  - `loc[]` uses label-based (row and column names) indexing while `iloc[]` uses position-based (integer position) indexing.
  - Conditional selection is only directly supported with `loc[]`. `iloc[]` requires boolean indexing.
- Updating Value With `loc[]`:
  ```
  # Update Age for Bob
  df.loc['b', 'Age'] = 32
  print(df)
  ```
- Updating Value With `iloc[]`:
  ```
  # Update Age for second row (Bob)
  df.iloc[1, 1] = 33
  print(df)
  ```
- Comprehensive Example:
  ```
  import pandas as pd

  data = {
      'Name': ['Alice', 'Bob', 'Charlie', 'David'],
      'Age': [25, 30, 35, 40],
      'City': ['New York', 'Chicago', 'Boston', 'Seattle']
  }

  df = pd.DataFrame(data)
  charlie = df.loc[2]
  print(charlie)
  second_row = df.iloc[1]
  print(second_row)
  two_rows = df.iloc[1:3]
  print(two_rows)
  over_30 = df.loc[df['Age'] > 30]
  print(over_30)
  two_columns = df.iloc[:, :2]
  print(two_columns)
  df.loc[1, 'Age'] = 32
  print(df)
  ```