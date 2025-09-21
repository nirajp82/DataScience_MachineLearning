# 📊 Pandas Quick Reference Cheatsheet

------------------------------------------------------------------------

## 🟢 Section 1: Pandas Series

``` python
import pandas as pd

s = pd.Series([10, 20, 30], index=['A', 'B', 'C'])
print(s)
```

Output:

    A    10
    B    20
    C    30
    dtype: int64

### Quick Reference -- Pandas Series

  -------------------------------------------------------------------------------------------------------
  Action       Code Example                                   Output Type        Example Output
  ------------ ---------------------------------------------- ------------------ ------------------------
  Create from  `pd.Series([10,20,30])`                        Series             0 10; 1 20; 2 30
  list                                                                           

  Create with  `pd.Series([10,20,30], index=['A','B','C'])`   Series             A 10; B 20; C 30
  labels                                                                         

  Create from  `pd.Series({'A':10,'B':20,'C':30})`            Series             A 10; B 20; C 30
  dict                                                                           

  Access by    `s['A']`                                       Scalar             10
  label                                                                          

  Access by    `s[0] or s.iloc[0]`                            Scalar             10
  position                                                                       

  Slice by     `s['A':'B']`                                   Series             A 10; B 20
  label                                                                          

  Boolean      `s[s>15]`                                      Series             B 20; C 30
  filter                                                                         

  Vectorized   `s + pd.Series({'A':1,'C':99})`                Series             A 11; B NaN; C 129
  ops (aligns                                                                    
  by index)                                                                      

  Inspect      `s.values`                                     ndarray            \[10 20 30\]
  values                                                                         

  Inspect      `s.index`                                      Index              Index(\['A','B','C'\])
  index                                                                          

  Check dtype  `s.dtype`                                      dtype              int64

  Count        `s.size`                                       int                3
  elements                                                                       

  Handle       `s.fillna(0)`                                  Series             fills NaN with 0
  missing                                                                        
  (fill)                                                                         

  Drop missing `s.dropna()`                                   Series             removes NaN rows

  Reindex      `s.reindex(['A','B','C','D'])`                 Series             adds D NaN

  Summary      `s.describe()`                                 Series             count 3.0; mean 20.0;
  stats                                                                          std 10.0; min 10.0; max
                                                                                 30.0

  Value counts `s.value_counts()`                             Series             10 1; 20 1; 30 1

  Sort by      `s.sort_index()`                               Series             sorted by labels
  index                                                                          

  Sort by      `s.sort_values()`                              Series             sorted numerically
  values                                                                         

  Convert      `s.astype(float)`                              Series             10.0; 20.0; 30.0
  dtype                                                                          

  To dict      `s.to_dict()`                                  dict               {'A':10,'B':20,'C':30}

  Unique       `s.unique()`                                   ndarray            \[10 20 30\]
  values                                                                         

  Number       `s.nunique()`                                  int                3
  unique                                                                         

  Head / Tail  `s.head(2) / s.tail(2)`                        Series             first 2 / last 2 rows
  -------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------

## 🟢 Section 2: DataFrame Basics

``` python
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 35],
    'City': ['New York', 'Los Angeles', 'Chicago']
}
emp_df = pd.DataFrame(data)
print(emp_df)
```

Output:

          Name  Age         City
    0    Alice   25     New York
    1      Bob   30  Los Angeles
    2  Charlie   35      Chicago

### Quick Reference -- DataFrame

  ---------------------------------------------------------------------------------------------------------------------------
  Action         Code Example                           Output Type        Example Output
  -------------- -------------------------------------- ------------------ --------------------------------------------------
  Select single  `emp_df['Name']`                       Series             0 Alice; 1 Bob; 2 Charlie
  column                                                                   

  Select         `emp_df[['Name','Age']]`               DataFrame          \[\['Alice',25\],\['Bob',30\],\['Charlie',35\]\]
  multiple                                                                 
  columns                                                                  

  Check type of  `type(emp_df['Name'])`                 Series             `<class 'pandas.core.series.Series'>`
  selection                                                                

  Add new column `emp_df['New'] = emp_df['Age'] + 5`    DataFrame          Adds "New" column with values \[30, 35, 40\]

  Drop column    `emp_df.drop('New', axis=1)`           DataFrame          Returns DataFrame without "New"
  (not inplace)                                                            

  Drop row       `emp_df.drop(1, axis=0)`               DataFrame          Removes Bob's row

  Shape of       `emp_df.shape`                         Tuple              (3, 3)
  DataFrame                                                                

  Select row by  `emp_df.loc[0]`                        Series             Alice row
  label                                                                    

  Select row by  `emp_df.iloc[2]`                       Series             Charlie row
  position                                                                 

  Subset         `emp_df.loc[[0,2], ['Name','City']]`   DataFrame          Alice + Charlie
  rows/columns                                                             
  ---------------------------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------

## 🟢 Section 3: Boolean Filtering

  -----------------------------------------------------------------------------------------------------------------------
  Action        Code Example                                                    Output Type        Example Output
  ------------- --------------------------------------------------------------- ------------------ ----------------------
  Boolean mask  `emp_df > 25`                                                   DataFrame          True/False per cell

  Conditional   `emp_df[emp_df['Age'] > 25]`                                    DataFrame          Bob & Charlie
  selection                                                                                        

  Multiple      `emp_df[(emp_df['Age'] > 25) & (emp_df['City']=="Chicago")]`    DataFrame          Charlie only
  conditions                                                                                       

  OR condition  `emp_df[(emp_df['Age'] > 25) | (emp_df['City']=="New York")]`   DataFrame          Alice, Bob, Charlie

  Filter +      `emp_df[emp_df['Age'] > 25]['Name']`                            Series             Bob, Charlie
  select column                                                                                    

  Reset index   `emp_df.reset_index()`                                          DataFrame          index reset
  -----------------------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------

## 🟢 Section 4: MultiIndex DataFrame

``` python
arrays = [
    ['New York','New York','New York','Los Angeles','Los Angeles','Chicago','Chicago'],
    ['Alice','Bob','Bob','Charlie','David','Eva','Frank']
]
index = pd.MultiIndex.from_arrays(arrays, names=('City','Name'))

emp_df_multi = pd.DataFrame({
    'Age': [25, 30, 31, 35, 28, 40, 32],
    'Score': [88, 92, 85, 79, 85, 95, 90]
}, index=index)

print(emp_df_multi)
```

Output:

                         Age  Score
    City        Name              
    New York    Alice    25     88
                Bob      30     92
                Bob      31     85
    Los Angeles Charlie  35     79
                David    28     85
    Chicago     Eva      40     95
                Frank    32     90

### Quick Reference -- MultiIndex

  ----------------------------------------------------------------------------------------------------------------------
  Action          Code Example                                                 Output Type        Example Output
  --------------- ------------------------------------------------------------ ------------------ ----------------------
  Create          `pd.MultiIndex.from_arrays(arrays, names=('City','Name'))`   MultiIndex         \[('New
  multi-index                                                                                     York','Alice'), ...\]

  Access outer    `emp_df_multi.loc['New York']`                               DataFrame          Alice & Bob rows
  index                                                                                           

  Access inner    `emp_df_multi.loc['Chicago'].loc['Eva']`                     Series             Age 40, Score 95
  index                                                                                           

  Cross-section   `emp_df_multi.xs('Bob', level='Name')`                       DataFrame          Rows where Name=Bob
  ----------------------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------

## 🟢 Section 5: Missing Data

``` python
import numpy as np
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eva'],
    'Age': [25, np.nan, 30, np.nan, 40],
    'City': ['New York', 'Los Angeles', np.nan, 'Chicago', 'Chicago']
}
df = pd.DataFrame(data)
print(df)
```

Output:

          Name   Age         City
    0    Alice  25.0     New York
    1      Bob   NaN  Los Angeles
    2  Charlie  30.0         NaN
    3    David   NaN      Chicago
    4      Eva  40.0      Chicago

### Quick Reference -- Missing Data

  --------------------------------------------------------------------------------------------
  Action      Code Example                           Output Type        Example Output
  ----------- -------------------------------------- ------------------ ----------------------
  Drop rows   `df.dropna()`                          DataFrame          Only Alice & Eva rows
  with NaN                                                              

  Drop        `df.dropna(axis=1)`                    DataFrame          Only Name column
  columns                                                               
  with NaN                                                              

  Drop rows   `df.dropna(thresh=2)`                  DataFrame          Keeps rows with ≥2
  with ≥2                                                               valid values
  non-null                                                              

  Fill        `df.fillna('Unknown')`                 DataFrame          Replaces NaN
  missing                                                               
  constant                                                              

  Fill with   `df['Age'].fillna(df['Age'].mean())`   Series             Fills NaN with 31.67
  mean                                                                  

  Forward     `df.fillna(method='ffill')`            DataFrame          Propagates last value
  Fill                                                                  

  Backward    `df.fillna(method='bfill')`            DataFrame          Propagates next value
  Fill                                                                  
  --------------------------------------------------------------------------------------------

------------------------------------------------------------------------

## 🟢 Section 6: GroupBy

``` python
group_data = {
    'Company': ['Google','Google','Microsoft','Microsoft','Facebook','Facebook'],
    'Employee': ['Sam','Charlie','Amy','Vanessa','Carl','Sarah'],
    'Sales': [200,120,340,124,243,350]
}
df = pd.DataFrame(group_data)
print(df)
```

Output:

         Company Employee  Sales
    0     Google      Sam    200
    1     Google  Charlie    120
    2  Microsoft      Amy    340
    3  Microsoft  Vanessa    124
    4   Facebook     Carl    243
    5   Facebook    Sarah    350

### Quick Reference -- GroupBy

  -----------------------------------------------------------------------------------------------------
  Action      Code Example                                    Output Type        Example Output
  ----------- ----------------------------------------------- ------------------ ----------------------
  Create      `df.groupby('Company')`                         GroupBy            GroupBy object
  GroupBy                                                                        
  object                                                                         

  Mean of     `df.groupby('Company').mean()`                  DataFrame          Avg sales per company
  groups                                                                         

  Sum of      `df.groupby('Company').sum()`                   DataFrame          Total sales per
  groups                                                                         company

  Std         `df.groupby('Company').std()`                   DataFrame          Spread of sales
  deviation                                                                      

  Count       `df.groupby('Company').count()`                 DataFrame          Counts per company
  values                                                                         

  Min / Max   `df.groupby('Company').min()`                   DataFrame          Min per company
  values                                                                         

  Access      `df.groupby('Company').sum().loc['Facebook']`   Series             Totals for Facebook
  single                                                                         
  group                                                                          

  Describe    `df.groupby('Company').describe()`              DataFrame          Stats per company
  groups                                                                         
  -----------------------------------------------------------------------------------------------------

------------------------------------------------------------------------

## 🟢 Section 7: Merge & Join

``` python
df1 = pd.DataFrame({'Name':['Alice','Bob','Charlie'],'Age':[25,30,28],'City':['New York','Chicago','Boston']})
df2 = pd.DataFrame({'Name':['Alice','Bob','Eva'],'Salary':[70000,80000,95000]})
```

### Quick Reference -- Merge & Join

  -------------------------------------------------------------------------------------------------------------
  Action        Code Example                                          Output Type        Example Output
  ------------- ----------------------------------------------------- ------------------ ----------------------
  Concatenate   `pd.concat([df1, df2])`                               DataFrame          Rows stacked
  rows                                                                                   

  Concatenate   `pd.concat([df1, df2], axis=1)`                       DataFrame          Side-by-side
  cols                                                                                   

  Merge inner   `pd.merge(df1, df2, on='Name')`                       DataFrame          Alice, Bob with salary

  Merge outer   `pd.merge(df1, df2, on='Name', how='outer')`          DataFrame          Includes Charlie & Eva

  Join on index `df1.set_index('Name').join(df2.set_index('Name'))`   DataFrame          Joins by Name index
  -------------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------

# ✅ Key Takeaways

-   `Series` = one-dimensional labeled array (like a column).
-   `DataFrame` = table of rows and columns.
-   Indexing with `.loc` (labels) vs `.iloc` (positions).
-   Handle missing values with `.dropna()`, `.fillna()`.
-   Use `.groupby()` for aggregation.
-   Combine datasets with `concat`, `merge`, `join`.
