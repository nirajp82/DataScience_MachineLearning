```python
import pandas as pd
```
```python
ecom = pd.read_csv('Ecommerce Purchases')
```

**Check the head of the DataFrame.**
```python
ecom.head()
```
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Address</th>
      <th>Lot</th>
      <th>AM or PM</th>
      <th>Browser Info</th>
      <th>Company</th>
      <th>Credit Card</th>
      <th>CC Exp Date</th>
      <th>CC Security Code</th>
      <th>CC Provider</th>
      <th>Email</th>
      <th>Job</th>
      <th>IP Address</th>
      <th>Language</th>
      <th>Purchase Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>16629 Pace Camp Apt. 448\nAlexisborough, NE 77...</td>
      <td>46 in</td>
      <td>PM</td>
      <td>Opera/9.56.(X11; Linux x86_64; sl-SI) Presto/2...</td>
      <td>Martinez-Herman</td>
      <td>6011929061123406</td>
      <td>02/20</td>
      <td>900</td>
      <td>JCB 16 digit</td>
      <td>pdunlap@yahoo.com</td>
      <td>Scientist, product/process development</td>
      <td>149.146.147.205</td>
      <td>el</td>
      <td>98.14</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9374 Jasmine Spurs Suite 508\nSouth John, TN 8...</td>
      <td>28 rn</td>
      <td>PM</td>
      <td>Opera/8.93.(Windows 98; Win 9x 4.90; en-US) Pr...</td>
      <td>Fletcher, Richards and Whitaker</td>
      <td>3337758169645356</td>
      <td>11/18</td>
      <td>561</td>
      <td>Mastercard</td>
      <td>anthony41@reed.com</td>
      <td>Drilling engineer</td>
      <td>15.160.41.51</td>
      <td>fr</td>
      <td>70.73</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Unit 0065 Box 5052\nDPO AP 27450</td>
      <td>94 vE</td>
      <td>PM</td>
      <td>Mozilla/5.0 (compatible; MSIE 9.0; Windows NT ...</td>
      <td>Simpson, Williams and Pham</td>
      <td>675957666125</td>
      <td>08/19</td>
      <td>699</td>
      <td>JCB 16 digit</td>
      <td>amymiller@morales-harrison.com</td>
      <td>Customer service manager</td>
      <td>132.207.160.22</td>
      <td>de</td>
      <td>0.95</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7780 Julia Fords\nNew Stacy, WA 45798</td>
      <td>36 vm</td>
      <td>PM</td>
      <td>Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_0 ...</td>
      <td>Williams, Marshall and Buchanan</td>
      <td>6011578504430710</td>
      <td>02/24</td>
      <td>384</td>
      <td>Discover</td>
      <td>brent16@olson-robinson.info</td>
      <td>Drilling engineer</td>
      <td>30.250.74.19</td>
      <td>es</td>
      <td>78.04</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23012 Munoz Drive Suite 337\nNew Cynthia, TX 5...</td>
      <td>20 IE</td>
      <td>AM</td>
      <td>Opera/9.58.(X11; Linux x86_64; it-IT) Presto/2...</td>
      <td>Brown, Watson and Andrews</td>
      <td>6011456623207998</td>
      <td>10/25</td>
      <td>678</td>
      <td>Diners Club / Carte Blanche</td>
      <td>christopherwright@gmail.com</td>
      <td>Fine artist</td>
      <td>24.140.33.94</td>
      <td>es</td>
      <td>77.82</td>
    </tr>
  </tbody>
</table>
</div>

** How many rows and columns are there? **
```python
ecom.info()
```
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 10000 entries, 0 to 9999
    Data columns (total 14 columns):
    Address             10000 non-null object
    Lot                 10000 non-null object
    AM or PM            10000 non-null object
    Browser Info        10000 non-null object
    Company             10000 non-null object
    Credit Card         10000 non-null int64
    CC Exp Date         10000 non-null object
    CC Security Code    10000 non-null int64
    CC Provider         10000 non-null object
    Email               10000 non-null object
    Job                 10000 non-null object
    IP Address          10000 non-null object
    Language            10000 non-null object
    Purchase Price      10000 non-null float64
    dtypes: float64(1), int64(2), object(11)
    memory usage: 1.1+ MB
    

** What is the average Purchase Price? **


```python
ecom['Purchase Price'].mean()
```
    50.34730200000025
** What were the highest and lowest purchase prices? **

```python
ecom['Purchase Price'].max()
```

    99.989999999999995

```python
ecom['Purchase Price'].min()
```

    0.0

** How many people have English 'en' as their Language of choice on the website? **

```python
ecom[ecom['Language']=='en'].count()
```

  Address             1098
  Lot                 1098
  AM or PM            1098
  Browser Info        1098
  Company             1098
  Credit Card         1098
  CC Exp Date         1098
  CC Security Code    1098
  CC Provider         1098
  Email               1098
  Job                 1098
  IP Address          1098
  Language            1098
  Purchase Price      1098
  dtype: int64
** How many people have the job title of "Lawyer" ? **
```python
ecom[ecom['Job'] == 'Lawyer'].info()
```

  <class 'pandas.core.frame.DataFrame'>
  Int64Index: 30 entries, 470 to 9979
  Data columns (total 14 columns):
  Address             30 non-null object
  Lot                 30 non-null object
  AM or PM            30 non-null object
  Browser Info        30 non-null object
  Company             30 non-null object
  Credit Card         30 non-null int64
  CC Exp Date         30 non-null object
  CC Security Code    30 non-null int64
  CC Provider         30 non-null object
  Email               30 non-null object
  Job                 30 non-null object
  IP Address          30 non-null object
  Language            30 non-null object
  Purchase Price      30 non-null float64
  dtypes: float64(1), int64(2), object(11)
  memory usage: 3.5+ KB

** How many people made the purchase during the AM and how many people made the purchase during PM ? **

**(Hint: Check out [value_counts()](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.value_counts.html) ) **
```python
ecom['AM or PM'].value_counts()
```
    PM    5068
    AM    4932
    Name: AM or PM, dtype: int64

** What are the 5 most common Job Titles? **

```python
ecom['Job'].value_counts().head(5)
```
    Interior and spatial designer    31
    Lawyer                           30
    Social researcher                28
    Purchasing manager               27
    Designer, jewellery              27
    Name: Job, dtype: int64

** Someone made a purchase that came from Lot: "90 WT" , what was the Purchase Price for this transaction? **
```python
ecom[ecom['Lot']=='90 WT']['Purchase Price']
```

    513    75.1
    Name: Purchase Price, dtype: float64

** What is the email of the person with the following Credit Card Number: 4926535242672853 **


```python
ecom[ecom["Credit Card"] == 4926535242672853]['Email'] 
```
    1234    bondellen@williams-garza.com
    Name: Email, dtype: object
** How many people have American Express as their Credit Card Provider *and* made a purchase above $95 ?**


```python
ecom[(ecom['CC Provider']=='American Express') & (ecom['Purchase Price']>95)].count()
```
    Address             39
    Lot                 39
    AM or PM            39
    Browser Info        39
    Company             39
    Credit Card         39
    CC Exp Date         39
    CC Security Code    39
    CC Provider         39
    Email               39
    Job                 39
    IP Address          39
    Language            39
    Purchase Price      39
    dtype: int64

** Hard: How many people have a credit card that expires in 2025? **

```python
sum(ecom['CC Exp Date'].apply(lambda x: x[3:]) == '25')
```
    1033

** Hard: What are the top 5 most popular email providers/hosts (e.g. gmail.com, yahoo.com, etc...) **

```python
ecom['Email'].apply(lambda x: x.split('@')[1]).value_counts().head(5)
```

hotmail.com     1638
yahoo.com       1616
gmail.com       1605
smith.com         42
williams.com      37
Name: Email, dtype: int64
