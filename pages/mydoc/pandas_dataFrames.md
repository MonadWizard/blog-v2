---
title: Pandas Data-Frames 
keywords: Pandas Bangla Tutorials, bangla Pandas, Bangla Python, Data Preprocessing Bangla, Monad wizard
last_updated: July 20, 2020
tags: [getting_started]
summary: "I have used this theme for Bangla Python Library that I've worked on as a professional technical writer."
sidebar: mydoc_sidebar
permalink: pandas_dataFrames.html
folder: mydoc
---



#  DataFrame 


[প্রয়োজনীয় data-set যা এই post এ ব্যবহার করা হয়েছে DOWNLOAD ](https://github.com/dust-nk-org/pandasDataSet/archive/master.zip)


DataFrame একটি table বা 2D-array জাতীয় কাঠামো, যাতে প্রতিটি কলামে একটি variable এর মান থাকে এবং বেশ কিছু row তে প্রতিটি column থেকে মানগুলির একটি set থাকে। 


Data হল তথ্যের স্বতন্ত্র টুকরো যা সাধারণত একটি বিশেষ উপায়ে format করা হয়। সমস্ত software দুটি সাধারণ বিভাগে বিভক্ত: ডেটা এবং প্রোগ্রাম। প্রোগ্রামগুলি ডেটা ম্যানিপুলেট করার জন্য নির্দেশাবলীর সংগ্রাহক।

আমার মতে, তথ্যটি কাঠামোগত উপায়ে, কাঠামোগত উপাত্তের তুলনায় উপলব্ধ থাকলে data বোঝা সহজ। এখন, data-frame সারি এবং কলামগুলির সাথে একটি কাঠামোগত ডেটা সরবরাহ করে। সুতরাং, আমরা সারি এবং কলামের উপর ভিত্তি করে data সহজেই বের করতে পারি এবং কাঠামোগত ডেটা বোঝাও খুব সহজ। এজন্য ডেটা data-frame এ রূপান্তর করা খুব জরুরি।

একটি data-frame Hard-Disk এর পরিবর্তে RAM ব্যবহার করে যার অর্থ এটি দ্রুত অস্থায়ী স্টোরেজ ব্যবহার করে যা কম্পিউটার বন্ধ হয়ে যাওয়ার পরে অদৃশ্য হয়ে যায়।

এখন চলুন <font color="green"> implement part </font> এ যাই।

আমরা <font color="green"> Churn_Modelling.csv </font> data-set ব্যবহার করব। 
আমরা data-frame এর columns এবং row এর details pandas এর দ্বারা দেখতে পারি। যা আমাদের prediction এ অনেক কাজ এ লাগতে পারে। big-data এর visualization অনেক সময় সাপেক্ষ আবার অনেক সময় সম্ভব হয় না। তাই আমরা Pandas এর কিছু function ব্যবহার করে সমস্ত data-frame এর সম্পর্কে জানতে পারি। এখন এই সব Shared Method এবং attributes এর সম্পর্কে দেখি। 

##  Shared Methods and Attributes 

<font color="green"> dataframe.columns </font> ব্যবহার করে আমরা সকল columns এর নাম দেখতে পারি। 

```python

import pandas as pd
cm = pd.read_csv("Churn_Modelling.csv",squeeze = True)

print("display all columns:\t", cm.columns,"\n")

```


<font color="blue"> output </font>


    display all columns:     Index(['RowNumber', 'CustomerId', 'Surname', 'CreditScore', 'Geography','Gender', 'Age', 'Tenure', 'Balance', 'NumOfProducts', 'HasCrCard', 'IsActiveMember', 'EstimatedSalary', 'Exited'],dtype='object') 



----


<font color="green"> dataframe.index </font> ব্যবহার করে আমরা সকল index দেখতে পারি। numaric data এর ক্ষেত্রে Range function এর parameter দ্বারা total index দেখতে পারি। আর categorical data এর ক্ষেত্রে row গুলোর নাম display দিবে। 



```python

import pandas as pd
cm = pd.read_csv("Churn_Modelling.csv",squeeze = True)

print("display all index:\t", cm.index,"\n")

```

<font color="blue"> output </font>


    display all index:       RangeIndex(start=0, stop=10000, step=1) 



----



আমরা python এর default <font color="green"> len </font> function ব্যবহার করে total  index বা colunms এর পরিমাণ integer value তে দেখতে পারি। 



```python

import pandas as pd
cm = pd.read_csv("Churn_Modelling.csv",squeeze = True)

print("total index length:\t", len(cm.index),"\n")
print("total columns length:\t", len(cm.columns),"\n")

```

<font color="blue"> output </font>


    total index length:      10000 
    total columns length:    14 



----




আমরা <font color="green"> dataframe.shape </font> ব্যবহার করে data-frame এর total rows এবং columns দেখতে পারি। 



```python

import pandas as pd
cm = pd.read_csv("Churn_Modelling.csv",squeeze = True)

print("Rows, Columns:\t", cm.shape)

```

<font color="blue"> output </font>


    Rows, Columns:   (10000, 14)



----





আমরা <font color="green"> dataframe.dtypes </font> ব্যবহার করে data-frame এর প্রত্যেক column এর data type দেখতে পারি। 



```python

import pandas as pd
cm = pd.read_csv("Churn_Modelling.csv",squeeze = True)

print("DataType:\n", cm.dtypes)

```


<font color="blue"> output </font>

DataType:

|   |    |
|------------------------|------|
| RowNumber |  int64 |
| CustomerId |  int64|
| Surname |  object|
| CreditScore |  int64|
| Geography |  object |
| Gender |      object|
| Age |  int64|
| Tenure |  int64|
| Balance | float64  |
| NumOfProducts |   int64   |
| HasCrCard |  int64 |
| IsActiveMember |   int64|
| EstimatedSalary | float64  |
| Exited |      int64|

dtype: object 



-------



আমরা <font color="green"> dataframe.axes </font> ব্যবহার করে ও data-frame এর প্রত্যেক row এবং column  এর নাম দেখতে পারি। 



```python

import pandas as pd
cm = pd.read_csv("Churn_Modelling.csv",squeeze = True)

print("Rows, Columns:\n", cm.axes)   # RangeIndex is  row , Index([colunms]) is Columns

```


<font color="blue"> output </font>

    Rows, Columns:
    [RangeIndex(start=0, stop=10000, step=1), Index(['RowNumber', 'CustomerId', 'Surname', 'CreditScore', 'Geography', 'Gender', 'Age', 'Tenure', 'Balance', 'NumOfProducts', 'HasCrCard', 'IsActiveMember', 'EstimatedSalary', 'Exited'],
    dtype='object')]





------



এইবার আমরা খুব useful <font color="green"> dataframe.info() </font> ব্যবহার করব। <font color="green"> .info() </font> ব্যবহার করে data-frame এর total information দেখতে পারি। যেমন: column position, column-name, total-data with null status , data-type, length of data-type, memory-usage, summery.  



```python

import pandas as pd
cm = pd.read_csv("Churn_Modelling.csv",squeeze = True)

print("Summery:\n", cm.info())  # most usefull......

```


<font color="blue"> output </font>

DataType:

| #  |  Column  |  Non-Null Count  |  Dtype  |
|-----------|---------|-----------|------|
|0| RowNumber |  10000 non-null  |  int64 |
|1| CustomerId | 10000 non-null | int64|
|2| Surname | 10000 non-null | object|
|3| CreditScore | 10000 non-null | int64|
|4| Geography | 10000 non-null |  object |
|5| Gender |  10000 non-null  |    object|
|6| Age | 10000 non-null | int64|
|7| Tenure | 10000 non-null | int64|
|8| Balance | 10000 non-null | float64  |
|9| NumOfProducts | 10000 non-null |  int64   |
|10| HasCrCard | 10000 non-null | int64 |
|11| IsActiveMember | 10000 non-null |  int64|
|12| EstimatedSalary | 10000 non-null | float64  |
|13| Exited |  10000 non-null  |   int64|

dtype: float64(2), int64(9), object(3)

memory usage: 1.1+ MB

Summery:

None

----


 <font color="green"> dataframe.sum() </font> ব্যবহার করে আমরা rows বা columns এর সমস্ত মান এক সঙ্ঘে যোগ করতে পারি।

 <font color="green"> dataframe.sum(o) </font> দ্বারা সমস্ত <font color="red"> rows  </font> এর মানগুলোর যোগফল আলাদা আলাদা ভাবে দেখতে পাই।


```python

import pandas as pd
cm = pd.read_csv("Churn_Modelling.csv",squeeze = True)

# only work with dataFrame not for serires
print(cm.sum(0)) # 0 means row

```


<font color="blue"> output </font>

|  |   |
|-----------|---------
| RowNumber | 50005000 | 
|  CustomerId | 156909405694 | 
| Surname | HargraveHill... |
| CreditScore | 6505288 |
| Geography | FranceSpainF... |
| Gender | FemaleFemale... |
| Age | 389218| 
| Tenure | 50128 |
| Balance | 7.64859e+08 |
| NumOfProducts | 15302 |
| HasCrCard | 7055 |
| IsActiveMember | 5151 |
| EstimatedSalary | 1.0009e+09 |
| Exited | 2037 |

dtype: object



---- 



<font color="green"> dataframe.sum(o) </font> দ্বারা সমস্ত <font color="red"> Columns  </font> এর মানগুলোর যোগফল আলাদা আলাদা ভাবে দেখতে পাই।


```python

import pandas as pd
cm = pd.read_csv("Churn_Modelling.csv",squeeze = True)

# only work with dataFrame not for serires
print(cm.sum(1)) # 1 means column

```


<font color="blue"> output </font>

|   |    |
|-----------|---------
| 0 | 15736618.88 |
| 1 | 15844315.44 | 
| 2 | 15893456.37 | 
| 3 | 15795925.63 |
| 4 | 15943385.92 |

. . .

|   |    |
|-----------|---------
| 9997 | 15637370.58 |
| 9998 | 15861138.83 |
| 9999 | 15807478.57| 

dtype: object


---- 


যদি কখনো dataframe এর কোন একটা column কে series বানানোর প্রয়োজন হয় বা dataframe এর একটা column আলাদা করতে হয় তবে আমরা <font color="green"> dataframe.column_name </font> ব্যবহার করে তা করতে পারি। অথবা আমরা list এর দ্বারা define করতে পারি। <font color="green"> dataframe[column_name] </font> .


```python

import pandas as pd
cm = pd.read_csv("Churn_Modelling.csv",squeeze = True)
print(cm.Balance) # convert to a series
# or 
print(cm["Balance"].head())


```


<font color="blue"> output </font>

|   |    |
|-----------|---------
| 0 | 0.00 |
| 1 | 83807.86 | 
| 2 | 159660.80 | 
| 3 |  0.00 |
| 4 | 125510.82 |

. . .

|   |    |
|-----------|---------
| 9997 |  0.00 |
| 9998 | 75075.31 |
| 9999 | 130142.79 | 

Name: Balance, Length: 10000, dtype: float64


---- 


Dataframe থেকে একটা column select করার মাধ্যমে আমরা series বানায়ে থাকি। তাই আমাদের আলাদা columns এর data-type : "Series"


```python

import pandas as pd
cm = pd.read_csv("Churn_Modelling.csv",squeeze = True)
print(type(cm["Balance"]))

```

<font color="blue"> output </font>
```
    <class 'pandas.core.series.Series'>

```


এই বার আমরা ২ বার তার অধিক columns আলাদা করা জানবো। 
যদি আমরা multi-dimention data থেকে multiple row বা columns আলাদা করতে চাই তা হইলে আমাদের double parentisis ব্যবহার করতে হয়। <font color="green"> dataframe[[column_name]] </font> 

```python

import pandas as pd
cm = pd.read_csv("Churn_Modelling.csv",squeeze = True)

print(cm[["Surname","Balance"]].head())
print(type(cm[["Surname","Balance"]]))


```


<font color="blue"> output </font>

|  | Surname  | Balance   |
|-----------|---------|------|
| 0 | Hargrave | 0.00 |
| 1 | Hill | 83807.86 | 
| 2 | Onio | 159660.80 | 
| 3 | Boni | 0.00 |
| 4 | Mitchell | 125510.82 |
 

<class 'pandas.core.frame.DataFrame'>


---- 


আমরা তো data-set থেকে অনেক columns আলাদা করলাম। এখন তরয় করি dataFrame এ কি করে new column যোগ করা যায়। 
খুব easy একটা ব্যপার। আমাদের just column এর নাম এবং data-List add করে দিতে হবে। <font color="green"> dataframe[column_name] = 'data' </font> . আমরা new_column এর location ও define করে দিতে পারি। এর জন্য <font color="green"> dataFrame.insert(position, column = "NAME", value = "Value") </font> .


```python

import pandas as pd
cm = pd.read_csv("Churn_Modelling.csv",squeeze = True)

cm["new_row"] = "New value"
print(cm)

cm.insert(1, column = "NewC", value = "NewC Value")
print(cm)


```


<font color="blue"> output </font>


|  | RowNumber  | CustomerId   | ... | Exited | new_row |
|-----------|---------|------|------|------|--------|
| 0 | 1 | 15634602 |... | 1 | New value |
| 1 | 2 | 15647311 |... | 0 | New value |
| 2 | 3 | 15619304 |... | 1 | New value |
| 3 | 4 | 15701354 |... | 0 | New value | 
| 4 | 5 | 15737888 |... | 0 | New value |
| ... | ... | ... | ... | ... | ... |

<class 'pandas.core.frame.DataFrame'>



|  | RowNumber | NewC | CustomerId   | ... | Exited | new_row |
|-------|-----|---------|------|------|------|--------|
| 0 | 1 | NewC Value | 15634602 |... | 1 | New value |
| 1 | 2 | NewC Value |  15647311 |... | 0 | New value |
| 2 | 3 | NewC Value |  15619304 |... | 1 | New value |
| 3 | 4 | NewC Value |  15701354 |... | 0 | New value | 
| 4 | 5 | NewC Value |  15737888 |... | 0 | New value |
| ... | ... | ... | ... | ... | ... | ... |

<class 'pandas.core.frame.DataFrame'>

---- 


##  Broadcasting Operations : 

Data-preprocessing এ অনেক সময় column এর সমস্ত value একটি specific মান দ্বারা "operation(+-*/)" calculation করতে হয়। তাই কোন column এর সব value update করতে আমরা List ব্যবহার করতে পারি। <font color="green"> dataframe[column_name].operation(value
) </font> অথবা  <font color="green"> dataframe[column_name]+-*/ value  </font> ব্যবহার করতে পারি।



```python

import pandas as pd
cm = pd.read_csv("Churn_Modelling.csv",squeeze = True)

print(cm["CustomerId"].add(10).head())
# or
print(cm["CustomerId"]+ 10)


print(cm["CustomerId"].sub(10).head())
# or
print(cm["CustomerId"]- 10)


print(cm["CustomerId"].mul(10).head())
# or
cm["CustomerId_New"] = cm["CustomerId"]* 10
print(cm["CustomerId_New"].head())
print(cm.head())


cm["CustomerId_New"] = cm["CustomerId"].div(1000000)
print(cm.head())



```


<font color="blue"> output </font>

for add 10 : 

|  |   |
|-----------|---------|
| 0 | 15634612 |
| 1 | 15647321 |
| 2 | 15619314 |
| 3 | 15701364 |
| 4 | 15737898 |
| ... | ... |

Name: CustomerId, dtype: int64

একটা `output` দেখানো হল। বাকি গুলো try করলেই দেখতে এবং বুঝতে পারবেন। 

----- 


##  .value_counts() 
একটি column এ কত রকমের এবং কতগুলো value আছে তা <font color="green"> dataframe[column_name].value_counts() </font> এর দ্বারা জানতে পারা যায়। 

```python

import pandas as pd
cm = pd.read_csv("Churn_Modelling.csv",squeeze = True)

print(cm["Gender"].value_counts())

```


<font color="blue"> output </font>

```

    Male      5457
    Female    4543
    Name: Gender, dtype: int64

```
Name: CustomerId, dtype: int64

একটা `output` দেখানো হল। বাকি গুলো try করলেই দেখতে এবং বুঝতে পারবেন। 


------------ 



##  .dropna() 

### Drop Rows with Null Values

Null value সাধারণত data analysis বা prediction এর accuracy কমায়ে দেয়, তাই কোন column থেকে null value remove করতে হইলে আমরা বেশ কিছু উপায় follow করতে পারি।

খুব সহজে  <font color="green"> dataFrame.dropna() </font> ব্যবহার করে যে সব rows এর মান Nan বা null ঐ সব row বা index সম্পূর্ণ remove করা যায়। 

এ ছাড়া অনেক সময় data-set এ অনেক index বা row থাকে যে সব row বা index এর সব value ই null. data-set এর columns এর নাম এর পর বা total data-set এর last এ কিছু extra index থাকে যার সব value ই null থাকে । এই সব null value data-set এ noise বাড়ায়ে থাকে। 

 <font color="green"> dataFrame.dropna(how = "all") </font>  এর দ্বারা যে সব index এর সব columns ই null সেই সব index বাদ দিতে পারি। 


তা ছাড়া আমরা specific column থেকে null value থাকা index গুলো বাদ দিতে পারি। <font color="green"> dataFrame.dropna(subset = ["columnsName"]) </font>



<font color="green"> dataFrame.dropna(axis = 1) </font> দ্বারা যদি কোন column এ একটা ও null value থাকে তা হইলে পুরো column বাদ দাওয়া যায়।

আমরা জানি axis = 0 = row , আর axis = 1 = column

by default  dataset.dropna(axis = 0) থাকে । 




```python

salary = pd.read_csv("salary.csv")

print(salary.dropna()) # remove full rows if any null values happend

# remove those row whoes all value are null
print(salary.dropna(how = "all"))

# remove those row whoes all value are null and replace permanently
print(salary.dropna(how = "all", inplace = True))

#check specific column , if any null in specific column then drop thoes row care by specific column
print(salary.dropna(subset = ["Salary"]))

print(salary.dropna(axis = 1)) # remove full Column if any null values happend


```


<font color="blue"> output </font>

```

    নিজে try করতে পারেন। 

```


------------



##  .fillna() 


### Fill Null Values with the .fillna() method

<font color="green"> dataFrame.fillna(value) </font> আমরা null value গুলো replace করে যে কোন value দিয়ে fill করতে পারি। 

<font color="green"> dataFrame["column"].fillna(value = "value_as_string", inplace = True) </font> দ্বারা total dataFrame এ যে কোন column এর value গুলোতে কোন null value আছে কি না তা compare করে null value replace করে specific value দিয়ে fill করতে পারি। 





```python


salary = pd.read_csv("salary.csv")

# replace all Null value with specific value
print(salary.fillna(0))

# replace specific column's all Null value with specific value
print(salary["Salary"].fillna(value = "Here we found null value", inplace = False))



```



----------------



##  .astype() method 

আমরা যদি data-set এর কোন column এর data এর data-type পরিবর্তন করতে চাই তা হইলে <font color="green"> dataFrame["columnName"].astype("int") </font> দ্বারা data type পরিবর্তন করতে পারি। বি:দ্র: column টার data অবশ্যয় numerical data হইতে হবে। 



```python


salary = pd.read_csv("salary.csv")

salary["new"]= 0.00  # can't make null value so can't be drop
salary["new"] = salary["new"].astype("int")
print(salary["new"])


```



##   .numique() method 

<font color="green"> dataFrame["column"].nunique() </font>
দ্বারা কোন data-set এর specific column এ total কতরকম এর data আছে টা জানা যায়। 






```python


salary = pd.read_csv("salary.csv")

# use to find total different type of value
print(salary["Purchased"].nunique())


```


<font color="blue"> output </font>

```

    2

```


------------



##   reduse memory space by change .astype() 

আমরা .astype() এর সঙ্ঘে আগেই পরিচিত হইছি। .astype() ব্যবহার করে memory space কমানো যায়। .info() এর সঙ্ঘে আমরা অনেক আগে থেকে পরিচিত। এখন দেখব .astype() ব্যবহার করে data type পরিবর্তন করাতে .info() তে memory space অনেকটা কমেছে । 





```python


salary = pd.read_csv("salary.csv")

print(" before : " )
print( salary.info())

print( salary.dropna(inplace = True)) # remove full rows if any null values happend

salary["Salary"] = salary["Salary"].astype("int")

print(" after : " )
print(salary.info())



# another example to reduse memory size
print(salary["Country"].nunique())
print(salary["Country"].astype("category"))
print(salary.info())



```


<font color="blue"> output </font>

```

    before : 

    dtypes: float64(2), object(2)
    memory usage: 448.0+ bytes
    None


    after : 

    dtypes: float64(1), int64(2), object(2)
    memory usage: 384.0+ bytes
    None




```


------------



##  .sort_value()  method 

আমরা যদি কোন columns এর referance এ সম্পূর্ণ data-frame কে sort করতে চাই বা যদি নির্দিষ্ট কোন columns এর data sort করে use করতে চাই তা হলে <font color="green"> data-frame.sort_values("columnName") </font> ব্যবহার করা যায়। defaultly <font color="pink">ascending = True</font>থাকে। real data-frame এর কোন পরিবর্তন হয় না টাই এই method টাই inplace parameter ব্যবহার করতে হয়। 





```python


salary = pd.read_csv("salary.csv")
print(salary,'\n')
print(salary.sort_values("Country"))

print(salary.sort_values("Country", ascending = False, inplace = False))

# sort with Null value na_position = "last", seen null value top 

print(salary.sort_values("Country", na_position = "first"))  # or na_position = "last"




```

<font color="blue"> output </font>

```

    try by self... ;)


```


------------


##   .to_dateTime method: 

pandas library দ্বারা dataframe কে date-time অনুসারে formating করা যায়। আমরা চাইলে যে কোন columns এর data এর সঙ্গে date-time formate করতে পারি। code a comment দ্বারা script এর workflow দাওয়া হয়েছে। 
আমরা pandas এর default paramenter <font color="green"> parse_dates </font> ব্যবহার করে ও same কাজ করতে পারি। 


```python


import pandas as pd
emply = pd.read_csv("employees.csv")

print(pd.to_datetime(emply["Start Date"]))
print(pd.to_datetime(emply["Last Login Time"]))  # added date columns to Last Login Time

print(pd.to_datetime(emply["Salary"]))  # added date-time columns value to salary columns

# or
df = pd.read_csv("employees.csv", parse_dates= ["Start Date", "Last Login Time"])
print(df)




```

<font color="blue"> output </font>

```

    try by self... ;)


```


##  reduse memory using .astype() 

আমরা <font color="green"> .astype() </font> method ব্যবহার করে memory size কমায়তে পারি। আমরা data-frame/ series যে কোন columns এর memory size reduse করতে astype() ব্যবহার করতে পারি । আমরা column define করে <font color="green"> .astype(similar_pandas_dtype) </font> ব্যবহার করব। pandas নিজে থেকেই memory reduse করে দিবা।



| Pandas dtype | Python type  | NumPy type   | Usage |
|-----------|---------|------|------|
| object | str or mixed | string_, unicode_, mixed types | Text or mixed numeric and non-numeric values |
| int64 | int | int_, int8, int16, int32, int64, uint8, uint16, uint32, uint64 | Integer numbers | 
| float64 | float	 | loat_, float16, float32, float64 | Floating point numbers | 
| bool	 | bool | bool_	 | True/False values |  
| datetime64	 | NA | datetime64[ns]	 | Date and time values |
| timedelta[ns] | NA | NA | Differences between two datetimes |
| category | NA | NA | Finite list of text values |





```python


import pandas as pd

df = pd.read_csv("employees.csv", parse_dates = ["Start Date", "Last Login Time"]).drop(columns="Start Date")
print(df.info())    # see memory usage: 54.8+ KB


df['Senior Management'] = df['Senior Management'].astype("bool")
df['Gender'] = df['Gender'].astype("category")
print(df.head(3))
print(df.info())    # now memory usage: 41.2+ KB



```

<font color="blue"> output </font>

```

    try by self... ;)


```





##   filter A DataFrame Based On a Condition 

pandas এ dataframe['columns'] =condition= value  দ্বারা condition check করা যায়। 

আর pandas এ dataframe[dataframe['columns'] =condition= value ] দ্বারা specific condition যুক্ত data সম্পূর্ণ নতুন data-frame পাওয়া যায়।   

এই condition check করে আবার তা data-frame এ define করে dataframe কে filter করা যায়। 







```python


import pandas as pd

df = pd.read_csv("employees.csv", parse_dates = ["Start Date", "Last Login Time"]).drop(columns="Start Date")
df[df["Gender"] == "Male"]

# work as details
mask = df["Team"] != "Finance"
print(mask)
print(df[mask]) # print all without Finance in Team column

# or example same as
print(df[df["Salary"] > 110000])

print(df[df["Start Date"] <= "1985-01-01"])


mask1 = df["Senior Management"]
mask2 = df["Start Date"] <= "1985-01-01"

print(df[mask1 | mask2])

#or filter on more than one condition .... ;)
print(df[(df["Gender"] == "Male") & (df["Senior Management"])])






```

<font color="blue"> output </font>

```

    try by self... ;)


```





##   .isin()  Method: 

single condition এ multiple value compare এ <font color="green"> .isin() </font> method ব্যবহার করা হয়। যদি আমার একাধিক ভালু একটা same condition এ chack করতে বা check করে new data-frame বানাতে চাই তা হইলে <font color="green"> data-frame["columnName].isin("[value1", "value2", "value3"]) </font> দ্বারা data-frame এর specific-column এ [value] গুলো আছে কি না তা boolean type দ্বারা জানা যায় আর চাইলে new data-frame এ convert করা যায়। 




```python


import pandas as pd

df = pd.read_csv("employees.csv", parse_dates = ["Start Date", "Last Login Time"]).drop(columns="Start Date")

m1 = df["Team"] == "Legal"
m2= df["Team"] == "Sales"
m3 = df["Team"] == "Product"

print(df[m1 | m2 | m3])

# or using method
df["Team"].isin(["Legal", "Sales", "Product"])

df[df["Team"].isin(["Legal", "Sales", "Product"])]

#or make new data-frame with specific data

teamm = df["Team"].isin(["Legal", "Sales", "Product"])
print(df[teamm])



```

<font color="blue"> output </font>

```

    try by self... ;)


```




##   .isnull()  and   .notnull()  methods : 

isnull এবং notnull ব্যবহার করা হয় nullবা Nan value filter ও pre-process এর জন্য। 

<font color="green">dataFrame["column"].isnull()  </font> এর দ্বারা উল্লেখিত column এর boolen series পাওয়া যায় । dataFrame["column"] এ যদি কোন null value থাকে তা হইলে  null value এর row টা True না হইলে False value এর series পাওয়া যাবে। 

.isnull() ব্যবহার করে বিশেষ column এর null value বিশিষ্ট row এর data-frame পাওয়া যায়। 

এর .notnull() ব্যবহার করে বিশেষ column এর null value ছাড়া অন্য value বিশিষ্ট row এর data-frame পাওয়া যায়। 




```python


import pandas as pd

df = pd.read_csv("employees.csv", parse_dates = ["Start Date", "Last Login Time"]).drop(columns="Start Date")

# see boolen series of "Team" column, if null then True else False
is_null = df["Team"].isnull()
print(is_null)

# see "Team" column's null value rows with full data-frame
ndf = df[is_null] 
print(ndf)

# see boolen series of "Team" column, if null then True else False
not_null = df["Team"].notnull() 
print(not_null)

# see "Team" column's without null value rows with full data-frame
nndf = df[not_null]
print(nndf)

# we can call in single line as
not_null_dfram = df[df["Team"].notnull()]
print(not_null_dfram)




```

<font color="blue"> output </font>

```

    try by self... ;)


```




##   .between() method : 

আমরা যদি নির্দিষ্ট কোন column এর নিদিষ্ট range এর মধ্যকার data নিয়ে কোন data-frame বানাইতে চাই টা হইলে .between() method ব্যবহার করা যায়। .between() method এর ২ টা parameter আছে। start আর end .between function এ (start,end) value define করে দিতে হয়। <font color="green"> dataframe["columnName"].between(start,end) </font>





```python


import pandas as pd

df = pd.read_csv("employees.csv", parse_dates = ["Start Date", "Last Login Time"]).drop(columns="Start Date")

# make series with boolen value , if value in between range then True else False
betWeen = df["Salary"].between(60000, 70000)
print(betWeen)

# make a data-frame with specific column's True Values 
df_sal = df[betWeen]
print(df_sal) 



```

<font color="blue"> output </font>

```

    try by self... ;)


```




##   .sort_values() method : 

আমরা data-frame এর যে কোন column এর value ascending order বা descending order এ sort করতে পারি। 

আমরা আগে থেকেই জানি, যে সব method এ inplace parameter আছে তা inplace = True ব্যবহার করে পরিবর্তনকে data-frame এ update করা হয়। 






```python


import pandas as pd

df = pd.read_csv("employees.csv", parse_dates = ["Start Date", "Last Login Time"]).drop(columns="Start Date")

# sort data-frame as ascending order and update dataframe 
df.sort_values("First Name", inplace = True)
print(df.head(5))


```

<font color="blue"> output </font>

```

    try by self... ;)


```





##  .duplicated() method: 

data-set এ অনেক column এ diplicate value থাকে। যদি আমরা duplicate value নিয়ে কাজ করতে চাই বা unique value বাহির করতে চাই। তা হইলে .duplicated() method ব্যবহার করা যায়। 

.duplicated() method এ keep parameter টা unique value define করে। keep = "last" মানে duplicate value এর last value টা unique হিসেবে গণ্য হবে। 

keep = "first" মানে duplicate value এর first value টা unique হিসেবে গণ্য হবে। 

আর keep = False মানে data-frame বা series এ যতগুলো  duplicate value আছে শুধু ঐ সব value গণ্য হবে। 

আমরা ~ চিহ্ন ব্যবহার করে series এর সব boolen value গুলোর মান reverse করতে পারি। যা ব্যবহার করে unique মান গুলো বাহির করা যায়।   



```python


import pandas as pd

df = pd.read_csv("employees.csv", parse_dates = ["Start Date", "Last Login Time"]).drop(columns="Start Date")


# those are True which are duplicated value , unique value take False
unique_last = df["First Name"].duplicated(keep = "last")

# create dataframe with only duplicated value 
df[unique_last].head(5)

# or take first value as unique and make dataframe with all duplicate value
df[df["First Name"].duplicated(keep = "first")].head(5)


# false take all value which have any duplicate value 
dupli = df["First Name"].duplicated(keep = False)

# make True as False so we pick all unique value as True
uniq = ~df["First Name"].duplicated(keep = False)  # ~ make reverse boolen data on series

# just print unique values who has no duplicate value
df[~df["First Name"].duplicated(keep = False)]      # ~ make reverse boolen data 



```

<font color="blue"> output </font>

```

    try by self... ;)


```




##   .drop_duplicates() method : 

সাধারণত যদি একাধিক row এর সব value duplicate হয় তবে dataFrame.drop_duplicates() ব্যবহার করে Duplicate row টা বাদ দাওয়া যায়। 

এ ছাড়া <font color="green"> dataframe.drop_duplicates() </font>  method এর parameter `subset` ব্যবহার করে specific columns compare করা এবং ঐ সব columns এর duplicate value বাদ দাওয়া যায়। যদি আমরা একাধিক column `subset` parameter এ define করি তা হলে define করা সব column এ যে value duplicate হবে just সেই row বাদ যাবে। 





```python


import pandas as pd

df = pd.read_csv("employees.csv", parse_dates = ["Start Date", "Last Login Time"]).drop(columns="Start Date")

print(df.drop_duplicates()) # just drop if all column's are same on more than one rows

# keep first value from duplicate elements on "First Row" columns
df.drop_duplicates(subset = ["First Name"], keep = "first")  

# keep last value from duplicate elements on "First Row" columns
df.drop_duplicates(subset = ["First Name"], keep = "last")    



df.drop_duplicates(subset = ["First Name"], keep = False)  # print just unique value

# remove if duplicate happend on both of columns
print(df.drop_duplicates(subset = ["First Name", "Team"], inplace = True))  
print(df.head(5))



```

<font color="blue"> output </font>

```

    try by self... ;)


```





##  .unique() and nunique() method :

আমরা যদি data-frame এর কোন column এ কতগুলো unique value আছে তা জানতে চাই তা হইলে <font color="green"> dataframe["column"].unique() </font> ব্যবহার করে দেখতে পাই। 

dataframe এ যদি কোন Nan বা null value থাকে .unique() method তা হইলে null value কে ও unique value হিসেবে count করবে। 

.unique() আর .nunique() একই কাজ করে। কিন্তু .nunique() কোন null বা Nan value কে unique value হিসেবে count করে না। 






```python


import pandas as pd

df = pd.read_csv("employees.csv", parse_dates = ["Start Date", "Last Login Time"]).drop(columns="Start Date")

df["Team"].unique()  # total type of unique value
print(len(df["Team"].unique()))   # total number of unique items

df["Team"].nunique()  # defaultly count unique value without nan

#nunique drop nan value defaultly but if we want to count nan we need to pass false
df["Team"].nunique(dropna = False)


```

<font color="blue"> output </font>

```

    try by self... ;)


```




##    .set_index() and .reset_index() methods  


আমরা index_col= 'col_name' এর সঙ্ঘে আগে থেকেই পরিচিত। index_col parameter data-set read এর সময়ই ব্যবহার করা হয় এবং এই parameter দ্বারা আমরা data-set read এর সময় index-column select করে দিতে পারি। 

আমরা যদি চাই যে আমরা index reset করে main data-set এর index এ convert হয়ে যাব তা হইলে আমরা  .set_index() ব্যবহার করতে পারি। .set_index আর index_col এর কাজ same. 
`syntex` : <font color="green"> dataframe.set_index("columnName", inplace = True) </font>

.reset_index() method এর drop parameter দ্বারা define করা হয় .set_index() এর দ্বারা create করা index টা data-frame এর একটা column হিসেবে থাকবে না কি remove করা হবে। drop=True ব্যবহার করা হইলে current index টা data-frame থেকে remove হয়ে যাবে আর drop=False ব্যবহার করলে current index টা একটা column হিসেবে add হইবে। 
`syntex` : <font color="green"> dataframe.reset_index(drop = True, inplace = True) </font>  bydefaultly: drop=False. তাই আমরা drop না ডিফাইন করলে তা False থাকে। মানে current index টা একটা column এ convert হয়ে থাকে। 


তাই index change করতে হইলে আগে reset index(drop=False) use করতে হবে না হইলে current index data-frame থেকে remove হয়ে যাবে।  




```python


import pandas as pd

bond = pd.read_csv("jamesbond.csv")

bond.set_index("Film", inplace = True)   # create index but other column are empty
print(bond.head(3))

bond.reset_index(drop = False)
print(bond.head(3))


bond.reset_index(drop = True)
print(bond.head(3))

bond.reset_index(drop = False, inplace= True)
print(bond.head(3))

"""
first need to reset_index then make set_index unless set_index remove current index and replace by new
"""

bond.reset_index(inplace= True)
bond.set_index("Year", inplace = True)
print(bond.head(3))


```

<font color="blue"> output </font>

```

    try by self... ;)


```






## .loc[] &  .iloc[] methods: 

*.loc[] function label নিয়ে কাজ করে এবং .iloc[] কাজ করে index নিয়ে ।  এছাড়া ২ function একই কাজ করে।*

pandas এ Data-Frame sort করা উচিত। কারণ pandas যদি unstructured data পায় তা হইলে একটার পর একটা data check করে কিন্তু sorted বা structured data এর ক্ষেত্রে pandas data check এর ক্ষেত্রে jump করে specific data খোঁজে। তাই time & execution complexity কমে। 

.loc[] & .iloc[] method এ () এর পরিবর্তে [] ব্যবহার করা হয়। Pandas এ extraction process এর জন্য [] ব্যবহার করা হয়। আমরা data-frame থেকে specific data বা columns extract এর জন্য [] করে থাকি। আমার মনে হয় pandas সেই একই process row extraction এ ও ব্যবহার করছে।  

আমরা .loc["index_value"] ব্যবহার করে data-frame এ যদি index_value বলে কিছু থাকে তা হইলে ঐ value টার Series পাব। 

আমরা [] এর মধ্যে range define করতে পারি  :  ব্যবহার করে। 
অথবা multiple value ডিফাইন করতে পারি। <font color="green"> dataframe.loc["value_1" : "value_9"] </font>
.loc[] alphabetically data check এবং execute করে। তাই range(:) এর condition এ বাপার তা লক্ষ রাখতে হবে। 


<font color="green"> dataframe.loc["value_1", "value_3","value_9"] </font> এখন যে সব index এর মান value_1 বা value_3 বা value_9 টার সবকয়টা value নিয়ে একটা new data-frame পাওয়া যাবে। যদি কোন define করা value data-frame এ না থাকে তা হইলে new data-frame এ ঐ ভালু index এবং বাকি সব value Nan সহ একটা new row পাওয়া যাবে।  



.loc[] দ্বারা index এবং .iloc[] সাধারণত index location কে represent করে থাকে।

.loc[] এর ক্ষেত্রে আমাদের index_value Declare করতে হয়। কিন্তু .iloc[] এ index যদি string ও হয় তা হইলে ও আমরা index এর position declare করতে পারি বা String index এর ক্ষেত্রেও index position integer এ range define করতে পারি। যা .loc[] এ possible na।





```python


import pandas as pd

bond = pd.read_csv("jamesbond.csv")
bond.sort_index(inplace = True) # sort index alphabetically

# .loc[]  work with label and .iloc[] work with index . otherwise both are same
print(bond.loc[14])
print(bond.iloc[14])

# if index is string then use .iloc[] as numeric range if necessary 
bond = pd.read_csv("jamesbond.csv", index_col ="Film")
bond.sort_index(inplace = True) # sort index alphabetically


print(bond.loc["Casino Royale"])
print(bond.loc["Casino Royale" : "Dr. No"])
print(bond.loc["Dr. No" : "Casino Royale"]) # always check condition alphabetically



print(bond.iloc[1:3])   # can be use on String index
print(bond.iloc[[0,3]])



```

<font color="blue"> output </font>

```

    run every print function one by one 
    try by self... ;)


```








##  .ix[] Method

*.ix[] মূলত .loc[] & .iloc[] এর combination এ তৈরি।*

আমরা .loc[] বা ,iloc[] এর যে কোন method এর বদল এ কোন রকম syntex পরিবর্তন না করেই .ix[] ব্যবহার করতে পারি। 

অমি personally .ix[] method টা prefer করি। আপনে যদি .loc[] এ lebel এবং .iloc[] এ index এই সব ব্যবহার নিয়ে ঝামেলা মনে করেন টা হইলে .ix[] ব্যবহার করে .loc[] বা .iloc[] ২ structure এই data-frame থেকে value নিতে পারেন। 


*NOTE: 'ix' pandas 1.0.0 থেকে remove করে দেওয়া হয়েছে , পূর্বের version গুলোতে কাজ করে। install previous version যদি .ix[] use করতে হয়। conda install pandas=0.25.1*





```python



import pandas as pd 

bond = pd.read_csv("jamesbond.csv", index_col ="Film")
bond.sort_index(inplace = True) # sort index alphabetically

# .ix[] work same as .loc[] or .iloc[]
bond.ix["GoldenEye"]
bond.ix["A View to a Kill" : "The World Is Not Enough"]
bond.ix[10:16]

#if give single unknown value then face error
#bond.ix["Sacred Bond"]  # cause Sacred Bond  not exist on data-frame
bond.ix[["Sacred Bond", "Spectre" ]]   # make Nan row with index Sacred Bond


# return boolen value, if exist then Yes else No
"Spectre" in bond.index
"Sacred Bond" in bond.index



```

<font color="blue"> output </font>

```

    try by self... ;)


```




## Second Argument to .loc[], .iloc[], and .ix[] Methods

যদি উপরের .loc[] এবং .iloc[] এবং .ix[] method বুঝে থাকেন টা হইলে example দেখেই বুজতে পারবেন । আমরা উপরের single কাজ গুলো একত্রে করেছি । 





```python


import pandas as pd 

bond = pd.read_csv("jamesbond.csv", index_col ="Film")
bond.sort_index(inplace = True) # sort index alphabetically


# .loc[row,column]
print(bond.loc["Moonraker"])
bond.loc["Moonraker", "Actor"]
bond.loc["Moonraker", "Actor" : "Budget"]
bond.loc["Moonraker", ["Actor" ,"Budget"]]


bond.iloc[1]
print(bond.iloc[1, 1])
bond.iloc[1, 1:6]
bond.iloc[1, [1 ,6]]


```


<font color="blue"> output </font>

```
    use print method to see every execution 

    please run one by one

    try by self... ;)


```



## Set New Values for a Specific Cell or Row

আমরা যদি Data-Frame এর specific কোন কোন data change করতে চাই, তা হইলে just python list এর basic consept আর pandas এর .loc[] বা .iloc[] কিংবা .ix[] ব্যবহার করলে ই হবে। 

আমরা .loc[] বা .iloc[] কিংবা .ix[] ব্যবহার করে specific data pick করব  যে data টা change করার দরকার। then just assign operator(=) ব্যবহার করে new data add করব। 


<font color="green"> define dataframe.loc[series, index] = new_Value </font>



```python


import pandas as pd 
bond = pd.read_csv("jamesbond.csv", index_col ="Film")
bond.sort_index(inplace = True)
print(bond.head(3))

# using .ix[] function
print(bond.ix["Dr. No"])
bond.ix["Dr. No", "Actor"] = "Sir Sean Connery"

# using .loc[] function 
print(bond.loc["Dr. No"])

bond.loc["Dr. No", "Actor"] = "Sir Sean Connery"
print(bond.loc["Dr. No"])


bond.loc["Dr. No", ["Box Office", "Budget", "Bond Actor Salary"]] = [448800000, 7000000, 600000]
print(bond.loc["Dr. No"])



```


<font color="blue"> output </font>

```

    please run one by one

    try by self... ;)


```




## Set Multiple Values in DataFrame

আমরা data-frame থেকে multiple ভালু এর Series বা new_dataframe pick করে তাতে specific value change করতে পারি। এর ফলে একটা change এর দ্বারা অনেক row তে change আনা যায়। 

<font color="green"> define dataframe.loc[new_dataframe_with_specific_value, index] = new_Value </font>



```python


import pandas as pd 
bond = pd.read_csv("jamesbond.csv", index_col ="Film")  # make "Film" as index
bond.sort_index(inplace = True)   # sort alphabetically 
print(bond.head(3))

mask = bond["Actor"] == "Sean Connery"  # make a nwe_dataframe with actor as "Sean Connery"
df2 = bond[mask]   
print(df2)

df2["Actor"] = "Sir Sean Connery"
print(df2)

# or  
bond.loc[mask,"Actor"] = "Sir Sean Connery"
print(bond)

bond[bond["Actor"] == "Roger Moore"]


```


<font color="blue"> output </font>

```

    please run one by one

    try by self... ;)


```





## Rename Index Labels or Columns in a DataFrame

আমরা <font color="green">  data-frame.rename(columns= {"old_name" : "new_name "}) </font> ব্যবহার করে column অথবা <font color="green">  data-frame.rename(index= {"old_name" : "new_name "}) </font> ব্যবহার করে dataframe এর যে কোন row বা index এর নাম change করতে পারি। 

আমরা dictionary আকারে value inseart করে data update করতে পারি। 

*.rename() এ inplace paramiter আছে ।*



```python



import pandas as pd 
bond = pd.read_csv("jamesbond.csv", index_col ="Film")
bond.sort_index(inplace = True)
print(bond.head(3))

# rename column
bond.rename(columns = {"Year": "Release Date", "Box Office": "Revenue"}, inplace = True)
print(bond.head(1))

# rename index
bond.rename(index = {"Dr. No": "Doctor No", 
                     "GoldenEye": "Golden Eye",
                     "The World Is Not Enough": "Best Bond Movie"}, inplace = True)

print(bond.head(10))
bond.ix["Best Bond Movie"]

# or we can change columns name by
bond.columns = ["Year", "Hero", "Director", "Gross", "cost", "salary"]
print(bond.head(3))



```


<font color="blue"> output </font>

```

    please run one by one

    try by self... ;)


```



## Delete Rows or Columns in a DataFrame 

আমরা <font color="green"> data-frame.drop(index = "Row_name",inplace = True) </font> ব্যবহার করে row এবং <font color="green">  data-frame.drop(labels = "column_name",inplace = True) </font> ব্যবহার করে column কে Data-frame থেকে remove করতে পারি। 

আমরা যদি কোন column এর Data cut করে new কোন Data inseart করতে চাই তা হইলে <font color="green"> data-frame.pop("name") </font> ব্যবহার করে specific column name এর Series পাইতে পারি। 

তা ছাড়া আমরা <font color="green"> del dataframe["column_name"] </font>  ব্যবহার করে data-frame থেকে column remove করতে পারি।   





```python


import pandas as pd
bond = pd.read_csv("jamesbond.csv", index_col ="Film")
bond.sort_index(inplace = True)
print(bond.head(3))

# drop rows
bond.drop(index = "Casino Royale",inplace = True)
print(bond.head(3))

# drop columns
d2 = bond.drop(labels = ["Year", "Director"], axis= "columns",inplace = True)
print(d2)
print(bond.head(3))


# cut columns and insert to another variable
hero = bond.pop("Actor")
print(hero)

# delete column permanentlly by del keyword
del bond["Director"]
print(bond.head(3))


```


<font color="blue"> output </font>

```

    please run one by one

    try by self... ;)


```





## Create Random Sample

বেশির ভাগ সময় data-set এ বিপুল পরিমাণ sample data থাকে বা প্রয়োজন এর অতিরিক্ত label থাকে । 

আমরা <font color="green"> data-frame.sample() </font> ব্যবহার করে সমস্ত data-frame এর নির্দিষ্ট কিছু data sample নিয়ে train বা test করতে পারি। আমরা .sample(n) এ n = (যে কোন numerical value) ব্যবহার করে সমস্ত data-frame থেকে randomly n সংখ্যক index এর data নিতে পারি। 

এ ছাড়া .sample(frac ) এ আমরা specific % data এর floating value define করে দিতে পারি। যার ফলে সমস্ত data থেকে ঐ নির্দিষ্ট শতাংশ data নিয়ে test বা train করতে পারি। 

আমরা .sample(n , axis = "columns") ব্যবহার করে column থেকে sampling করতে পারি। 







```python


import pandas as pd
bond = pd.read_csv("jamesbond.csv", index_col ="Film")
bond.sort_index(inplace = True)
print(bond)

bond.sample(n = 6)  # give 6 random rows from bond

bond.sample(frac = .25) # give 25% of number from bond 

bond.sample(n = 3, axis = "columns") # give 3 random columns from bond



```


<font color="blue"> output </font>

```

    please run one by one

    try by self... ;)
    
    or comment for discussion .......


```





## The .nsmallest() and .nlargest() methods

আমরা data-frame থেকে index অনুযায়ী যে কোন পরিমাণ এর সবথেকে বড় data  <font color="green"> data-frame.nlargest() </font>  এবং সবথেকে ছোট data <font color="green"> data-frame.nsmallest() </font> function ব্যবহার করে নিতে পারি। 




```python



import pandas as pd
bond = pd.read_csv("jamesbond.csv", index_col ="Film")
bond.sort_index(inplace = True)
print(bond)

# we can sort by
bond.sort_values("Year", ascending = False).head(3)
# or using .nlargest()
bond.nlargest(n=3, columns = "Year")


# we can sort by
bond.sort_values("Year", ascending = True).head(3)
# or using .nlargest()
bond.nsmallest(n=3, columns = "Year")
#or
bond["Year"].nsmallest(2)



```


<font color="blue"> output </font>

```

    please run one by one

    try by self... ;)
    
    or comment for discussion .......


```






## Filtering with the where Method

data-frame থেকে data filter এর জন্য যদি নির্দিষ্ট কোন condition অনুযায়ী data pick করতে হইলে <font color="green"> data-frame.where(data-frame["column-name"] ~condition~ n ) </font> ব্যবহার করা যায়। 





```python



import pandas as pd
bond = pd.read_csv("jamesbond.csv", index_col ="Film")
bond.sort_index(inplace = True)
print(bond.head(3))

mask = bond["Actor"] == "Sean Connery"
bond[mask]

b = bond.where(mask)

# same as
b2 = bond.where(bond["Box Office"] > 800)

b3 = bond.where(bond["Year"] > 2000)




```


<font color="blue"> output </font>

```

    please run one by one

    try by self... ;)
    
    or comment for discussion .......


```






## The .query() method 


* .query() method only string argument এর জন্য কাজ করে। 
* data-frame এর column এর নাম এ যদি কোন spece না থাকে তা হইলে .query() method কাজ করে।


আমরা .query() method এ single বা multiple condition ব্যবহার করতে পারি। 

.query() অনেকটা search operation এর মত কিন্তু সাধারণ operation এর থেকে প্রায় ১০ গুন বেশি faster. 






```python


import pandas as pd
bond = pd.read_csv("jamesbond.csv", index_col ="Film")
bond.sort_index(inplace = True)
print(bond.head(3))

# using list comprehention to replace data for reduse spaces 
bond.columns = [column_name.replace(" ", "_") for column_name in bond.columns]
bond.head(1)

# using .query()
bond.query("Actor == 'Sean Connery'")

ad = bond.query("Actor == 'Sean Connery' or Director == 'John Glen'")

add = bond.query("Actor not in ['Sean Connery', 'Roger Moore']")
print(add)





```


<font color="blue"> output </font>

```

    please run one by one

    try by self... ;)
    
    or comment for discussion .......


```






## .apply() Method on Single Columns


data-frame এর কোন single column নিয়ে কাজ করা মানে data-frame থেকে একটা Series নিয়ে কাজ করা। 

.apply() method ব্যবহার করা হয় condition বা operation এর পর, যার দ্বারা change টা সমস্ত data তে execute হয়। 






```python



import pandas as pd
bond = pd.read_csv("jamesbond.csv", index_col ="Film")
bond.sort_index(inplace = True)
print(bond.head(3))

def convert_to_String_and_add_millions(number):
    return str(number) + "MILLIONS"

bond["Box Office"] = bond["Box Office"].apply(convert_to_String_and_add_millions)
print(bond["Box Office"])

# convert multiple rows with specific value by
columns = ["Budget","Bond Actor Salary"]
for col in columns:
    bond[col] = bond[col].apply(convert_to_String_and_add_millions)

print(bond[col])





```


<font color="blue"> output </font>

```

    please run one by one

    try by self... ;)
    
    or comment for discussion .......


```






## .apply() Method with Row Values


আমরা যদি data-frame থেকে classification বাহির করতে চাই। বা specific row দ্বারা আলাদা data-frame বাহির করতে চাই, তা হইলে ও <font color="green"> data-frame.apply(operation, axis) </font> ব্যবহার করা হয়। 

আমরা একটি example এ actor আর budget এর উপর ভিত্তি করে movies category বানাব। 






```python


import pandas as pd 
bond = pd.read_csv("jamesbond.csv", index_col ="Film")
bond.sort_index(inplace = True)
print(bond.head(3))

def good_movie(row):
    
    actor = row[1]
    budget = row[4]
    
    if actor == "Pierce Brosnan":
        return "The Best"
    elif actor == "Roger Moore" and budget > 40:
        return "Enjoyable"
    else:
        return "I have no clue"

bond.apply(good_movie, axis = "columns")



```


<font color="blue"> output </font>

```


    try by self... ;)
    
    or comment for discussion .......


```





## .copy() Method 

আমরা data-frame নিয়ে অনেক operation করে থাকি। আবার data-frame এ ও অনেক পরিবর্তন করে থাকি। যদি কখনও আমরা data-frame এর কোন পরিবর্তন আনি কিন্তু তা যেন main data-frame এ কোন পরিবর্তন না করে এমন কিছু করতে চাই, তা হইলে আমরা <font color="green"> .copy()  </font> method ব্যবহার করে data-frame এর যে কোন part অন্য variable এ copy করে নিয়ে তা ব্যবহার করতে পারি। 






```python

import pandas as pd 
bond = pd.read_csv("jamesbond.csv", index_col ="Film")
bond.sort_index(inplace = True)
print(bond.head(3))

directors = bond["Director"].copy()
directors.head(3)



```


<font color="blue"> output </font>

```


    try by self... ;)
    
    or comment for discussion .......


```














