---
title: Pandas Series
keywords: Pandas Bangla Tutorials, bangla Pandas, Bangla Python, Data Preprocessing Bangla, Monad wizard
last_updated: July 20, 2020
# tags: [getting_started]
summary: "python bangla blog post এর দ্বারা Pandas Library এর Series related method গুলো আলোচিত হয়েছে ।"
sidebar: mydoc_sidebar
permalink: pandas_series.html
folder: mydoc
---


### Pandas


[প্রয়োজনীয় data-set যা এই post এ ব্যবহার করা হয়েছে DOWNLOAD ](https://github.com/dust-nk-org/pandasDataSet/archive/master.zip)


Pandas একটি পাইথন প্যাকেজ যা "রিলেশনাল" বা "লেবেলযুক্ত" ডেটা সহজ এবং স্বজ্ঞামূলকতার সঙ্গে কাজ করার জন্য fast, flexible, এবং expressive ডাটা স্ট্রাকচার প্রদান করে। python প্রোগ্রামিং  এ real-world ডাটা analysis এর জন্য high-level building block বা structured data তৈরিতে pandas খুবই গুরুত্বপূর্ণ। pandas একটি open-source পাইথন package.

পান্ডাস বিভিন্ন ধরণের ডেটার জন্য বেশ উপযোগী:
* SQL table বা Excel spreadsheet এ Tabular data এর সঙ্গে heterogeneously-typed columns এ।
* Ordered এবং unordered (fixed-frequency প্রয়োজন নাই) time series data এ। 
* Arbitrary matrix data (homogeneously বা heterogeneous ধরনের ডাটা) এর সঙ্গে row এবং column labels এর। 
* যে কোন ধরনের observational / statistical data sets এ।তাছাড়া pandas ডেটা স্ট্রাকচারে রাখার জন্য ডেটা লেবেল লাগে না। 

pandas নিম্নলিখিত তিনটি ডেটা স্ট্রাকচার নিয়ে কাজ করে -
* Series
* DataFrame
* Panel

| ডেটা স্ট্রাকচার | Dimension(মাত্রা)  | Description  |
| ------------------------ | ------ | ---------- |
| [Series](#Series) | 1 | 1D labeled homogeneous array, sizeimmutable. |
| [DataFrames](#DataFrames) | 2 | General 2D labeled, size-mutable tabular structure with potentially heterogeneously typed columns. |
| [Panels](#Panels) | 3 | General 3D labeled, size-mutable array. |

pandas লাইব্রেরিতে [Numpy](https://numpy.org/)এর বেশিরভাগ কার্যকারিতা ব্যবহার করা হয়। pandas DataFrame এবং Panel ndarray ব্যবহার করে।  


Pandas এর ব্যবহার হয় :

* Fast এবং efficient DataFrame object এর সঙ্গে default and customized indexing তৈরিতে।
* বিভিন্ন file formate থেকে memory তে data load করতে ।
* missing data এর জন্য data alignment এবং integrated করতে।  
* data sets কে Reshaping এবং pivoting করতে।
* large data set কে Label-based slicing, indexing এবং subsetting করতে। 
* একটি data structure এর columns বা rows কে delete বা insert করতে। 
* Group by data এর জন্য aggregation and transformations করতে। 
* High performance এ merging এবং joining করতে।
* Time Series functionality তে।




### Installation

Pandas installation এর সবথেকে সহজ উপাই Anaconda distribution। একটি cross platform distribution যা  data analysis এবং scientific computing এর জন্য ব্যবহার করা হয়।

আমরা anaconda install করে pipline ব্যবহার করে pandas install করব। 
আমি মনে করতেছি আপনারা anaconda install করেছেন এবং anaconda-prompt ব্যবহার করে 
<font color="green"> pip install pandas </font> দ্বারা pandas install সম্পূর্ণ করেছেন। 

online এর help নিয়ে খুব তাড়াতাড়ি installation শেষ করুন তার পর আবার blog এ ফিরে আসুন ।





### Series

আমরা আগেই জেনেছি যে Series একটি আক-মাত্রা বিশিষ্ট labeled array যা যেকোনো data type এর  ডেটা store করতে পারে। আমরা labeled array বলছি , কারন Series এ সকল 1-dimensional data থাকে, এর প্রতিটি data এর axis label গুলোকে index বলা হয়। 

pandas.Series এর syntax <font color="pink"> pandas.Series( data, index, dtype, copy) </font>


| parameter number | Parameter name  | Description  |
| -------------------- | ------ | ---------- |
| 1 | data | data takes various forms like ndarray, list, constants. |
| 2 | index | Index values must be unique and hashable, same length as data. Default np.arrange(n) if no index is passed. |
| 3 | dtype | dtype is for data type. If None, data type will be inferred. |
| 4 | copy | Copy data. Default False |



### without importing Dataset

আমরা List এবং Dictionary ব্যবহার করে series তৈরি করব তারপর data set ব্যবহার করে series তৈরি করব। আমার এর পোস্টটি implementation এ main focus দিয়ে তৈরী । 

pandas নিয়ে যে কোন কাজ করার জন্য padas কে import করে নেয়। pandas নামটি include করে কোন execution করার জন্য একটা sort name define kori syntax <font color="green"> as pd </font>। Series() class কে call করার মাধমে series তৈরী করা হয়। প্রথমে আমরা একটা blank Series তৈরি করবো। 

```python

import pandas as pd

pd.Series() # empty series

```


python এর list তৈরী করে তা একটা series এ রুপান্তর করি। 
আপনারা অন্য একটি list তৈরী করে try করুন।


```python

# List
ice_cream= ["chocolate", "vanila", "strawbarry", "Run Raisin"]

import pandas as pd

s = pd.Series(ice_cream)
print(s)

```


 <font color="blue"> OUTPUT: </font> 


|   |    |
|-------|------|
| 0 |  chocolate |
| 1 |      vanila|
| 2 |  strawbarry|
| 3 |  Run Raisin|

dtype: object 



--------



এইবার numpy এর দ্বারা array তৈরী করে তা একটি series এ রুপান্তর করি।
এর জন্য numpy কে import করতে হবে, সুবিধার জন্য  <font color="green"> as np</font> define করি। numpy এর <font color="green">arange</font> function, python এর <font color="green">range</font> function এর মত । arange function array তৈরি করে।  np.arange(start, end, difference)




```python

import numpy as np
arr = np.arange(1,5)
arr2 = np.arange(1,9,2)

import pandas as pd
ser = pd.Series(data=arr)
ser2 = pd.Series(data=arr, index=arr2)

print("series1", ser)
print("series2", ser2)

```



 <font color="blue"> OUTPUT: </font> 

series1 

|   |    |
| ---------- | ------ |
| 0 | 1 |
|1  |  2|
|2  |  3|
|3  |  4|

dtype: int32 


series2 

|   |    |
| ---------- | --------- |
| 1 | 1 |
|3  |  2|
|5  |  3|
|7  |  4|

dtype: int32 



---------




boolean value ব্যবহার করে ও আমরা series তৈরি করতে পারি।  



```python

registration= [True, False, True, False]

import pandas as pd
s2 = pd.Series(registration)
print(s2)

```


 <font color="blue"> OUTPUT: </font> 

 
|   |    |
|--------- | ------ |
| 0 | True |
|1  | False|
|2  | True|
|3  | False|

dtype: bool 



---------




এখন python এর Dictionary তৈরী করে তা একটা series এ রুপান্তর করি।
dictionary এর key কে index এবং value কে data হিসেবে ব্যবহার করবো। 
 আপনারা অন্য একটি Dictionaryতৈরী করে try করুন।


```python

data = {"Aardvark" : "An animal", "Cyan" : "A color", "Nothing" : "None"}

import pandas as pd
s3 = pd.Series(data)

print(s3)


```



 <font color="blue"> OUTPUT: </font> 


|   |    |
| ---------- | ------ |
| Aardvark | An animal |
|Cyan | A color|
|Nothing | None|

dtype: bool 



----------





এখন আমরা pandas.Series এর কিছু attribute দেখে নেয়। যেমন series এর সব value বা সব index বা series এর datatype.



```python


data = {"Aardvark" : "An animal", "Cyan" : "A color", "Nothing" : "None"}

import pandas as pd
s3 = pd.Series(data)

print(s3.values)
print(s3.index)
print(s3.dtype)


```


 <font color="blue"> OUTPUT: </font> 

 
    ['An animal' 'A color' 'None']

    Index(['Aardvark', 'Cyan', 'Nothing'], dtype='object')

    object


---------





pandas excel এর মত total calculation করতে পারে।defaultly সব calculation value নিয়ে ঘটে। আমরা বিশেষ কিছু method দেখব। 

sum() function দ্বারা total যোগফল বাহির করা যায়। 

product() function দ্বারা একটি কে অপরটি দ্বারা গুন করা  গুনফল বাহির করা যায়।

mean() function দ্বারা গড় মান  বাহির করা যায়।

min() function দ্বারা সব থেকে ছোট  মান বাহির করা যায়।

max() function দ্বারা সব থেকে বড় মান বাহির করা যায়।


```python

import pandas as pd
ser = pd.Series([1,2,3,4],index = ['USA', 'Germany','USSR', 'Japan'])   

print(ser.sum())
print(ser.product())  # multiply eatch other
print(ser.mean())
print(ser.min())
print(ser.max())

```


 <font color="blue"> OUTPUT: </font> 
 

    10
    24
    2.5
    1
    4




---------




এখন আমরা একটা series কে অন্য series এর সঙ্গে concatination করবো আর আমাদের প্রয়োজনীয় series তৈরী করবো। ঠাণ্ডা মাথায় চিন্তা করুন আমার বিশ্বাস আপনারা নিজেরাই পুরটা বঝতে পারবেন। 


```python

import numpy as np
import pandas as pd

ice_cream= ["chocolate", "vanila", "strawbarry", "Run Raisin"]
s = pd.Series(ice_cream)

lottery= [4,115,23,42]
s1 = pd.Series(lottery)

registration= [True, False, True, False]
s2 = pd.Series(registration)

webster = {"Aardvark" : "An animal", "Banana" : "A delicious fruit", "Cyan" : "A color", "Nothing" : "None"}
s3 = pd.Series(webster)

s4 = pd.Series(ice_cream,lottery)
s5 = pd.Series(data= lottery, index = registration)
s6 = pd.Series(index = webster, data = registration) 

print(s4,"\n")
print(s5,"\n")
print(s6,"\n")

```


 <font color="blue"> OUTPUT: </font> 
 

|   |    |
| ------------- | ------ |
| 4 | chocolate |
|115 | vanila |
|23 | strawbarry|
|42 | Run Raisin|

dtype: object  


---


|   |    |
| ---------- | ------ |
| True | 4 |
|False | 115 |
|True | 23 |
|False | 42 |

dtype: int64  

---

|   |    |
| ------------ | ------ |
| Aardvark | True |
| Banana | False |
|Cyan | True |
|Nothing | False |

dtype: bool 





-----------




### with importing Dataset

pandas.Series এর এই অংশতে আমরা .csv file include করে তা থেকে series তৈরি করবো।
pandas library তে pandas.read_csv দ্বারা csv ফাইল directory থেকে read করা হয়। 

১৮ টির বেশি file type pandas read করতে পারে। এই post এ আমরা comma-separated values file নিয়ে কাজ করবো। 
read_csv এর প্রায় ৪৯ টির মত parameter আছে। এর মধ্যে filepath_or_buffer তা major.অন্য parameter গুল প্রয়োজন হইলে ব্যবহার করতে হয়। 

dataset টি source code এর একই path এ থাকলে just dataset টির নাম উল্লেখ করলেই pandas read করতে পারবে। এর যদি dataset টি অন্য path এ থাকে বা net থেকে read করতে হয় তবে একটু বেশি কষ্ট করতে হবে। 


আমরা Beton এবং Salary ২ টি demo dataset ব্যবহার করবো। আপনারা অবশ্যয় dataset ২ টি download করে নিজারা try করবেন।

[প্রয়োজনীয় data-set যা এই post এ ব্যবহার করা হয়েছে DOWNLOAD ](https://github.com/dust-nk-org/pandasDataSet/archive/master.zip)

যদি code এ কোন update করতে না ইত্তছে করে তা হইলে যে directory তে .py file create করেছেন .csv ফাইল download করে same directory তে রাখুন। 

## .read_csv()

সবার প্রথম pandas import করে নেয়। এখন read_csv এর দ্বারা dataset ফাইল থেকে variable এ store করি। 
for a basic purpose আমরা read_csv ar ২ টা parameter ব্যবহার করবো। file path এবং use colunms.
এখন টা হইলে আমরা dataset থেকে data read করি।



```python

import pandas as pd

#[["salary","Age"]] restructured dataset's columns
salary = pd.read_csv("salary.csv", usecols = ["Age","Salary"])[["Salary","Age"]] 

#squeeze convert from dataframe to series
beton = pd.read_csv("Beton.csv", usecols = ["Salary"], squeeze = True) 

beton2 = pd.read_csv("Beton.csv")

print("salary: ", type(salary))
print("beton: ", type(beton))
print("beton2: "type(beton2))


```


 <font color="blue"> OUTPUT: </font> 

    salary: <class 'pandas.core.frame.DataFrame'>
    beton: <class 'pandas.core.series.Series'>
    beton2: <class 'pandas.core.frame.DataFrame'> 




আমরা <font color="green">usecols</font> parameter এ dataset এর যে সব columns use করবো সেই সব columns এর নাম উল্লেখ করবো। data set এর heading এ যে নাম আসে same নাম দিতে হবে।pandas এ csv file কে mainly DataFrame এ  নিয়ে কাজ করা হয়। 


আমরা চাইলে columns গুলোকে আগে বা পিছে নিতে পারি। মানে columns এর position change করতে পারি। <font color="green">pd.read_csv("path", usecols=["col1","col2"])</font> এই তার দ্বারা আমাদের dataset read complete.এখন আমাদের value তে col1 এর পর col2 এই structured এ ডাটা store হয়েছে। শেষ এ restructered define করতে পারি। [["col2","col1"]] এখন<font color="green">pd.read_csv("path", usecols=["col1","col2"])[["col2","col1"]]</font> দ্বারা col2 এর পর col1 এই structured এ ডাটা store হবে। 


## .head()


.head() এর দ্বারা defaultly প্রথম ৫ টা row এর ডাটা দেখতে পারা যায়। বিশাল dataset এর overview নিতে চাইলেও যদি সম্পূর্ণ dataset print করা হয় তা হইলে ব্যাপারটা যেমন সময় সাপেক্ষ তেমনই তার জন্য memory আর execution এ problem হয়। dataset এর sort overview নিতে তাই .head() ব্যবহার করা হয়। .head() এ যত number define করা হয় সেই কয়টা row print হয়। 



```python

import pandas as pd

beton2 = pd.read_csv("Beton.csv")
print(beton2.head(),"\n\n")
print(beton2.head(3))

```


 <font color="blue"> OUTPUT: </font> 

 
| |YearsExperience   |   Salary |
| --------- | ----------- | ------ |
| 0 | 1.1 | 39343.0 |
|1 | 1.3 | 46205.0 |
|2 | 1.5| 37731.0 |
|3 | 2.0 | 43525.0 |
|4 | 2.2 | 39891.0  |


-------


| |YearsExperience   |   Salary |
| --------- | ----------- | ------ |
| 0 | 1.1 | 39343.0 |
|1 | 1.3 | 46205.0 |
|2 | 1.5 | 37731.0 |



## .tail()


.head() যেমন প্রথম data গুলো দেখায় .tail() তেমনই শেষ data গুলো দেখায়। 

output নিজেরাই try করে দেখুন। 



```python

import pandas as pd

beton2 = pd.read_csv("Beton.csv")
print(beton2.tail(),"\n\n")
print(beton2.tail(10))

```


## python এর কিছু built-in Function এর ব্যবহার :

আমি মনে করি আপনারা python language এর ধারনা রাখেন। তাই এই topic নিয়ে কিছু আলোচনা করলাম না। আসা করি আপনাদের বুঝতে problem হবে না। 

এই topic টি আপনারা নিজেরাই বুঝে run করবেন। 



```python


import pandas as pd

beton2 = pd.read_csv("Beton.csv")

print(len(beton2))   # len(series) give total number of row
print(type(beton2))
print(dir(beton2))  # see all method can be use with this data frame

print(sorted(beton2))  #sort(dataFrame) sorted data assiending orderd and create a list
print(type(sorted(beton2)))


print(list(beton2))          # create a list of data frame


print(dict(beton2))       # create a dictionary of data frame

print(max(beton2))        # maximum number
print(min(beton2))        # minimum number


```



## .is_unique

dataset এ duplicate value আসে কি না। বা dataset এ একই কোন value  এক এর অধিক  আসছে কি না তা check করতে <font color="green">.is_unique</font> ব্যবহার করা হয়।

.is_unique এর output booolen type হয়ে থাকে। যদি True হয় তবে কোন duplicate value নেই। আর যদি output টা False হয় তা হইলে duplicate value আছে । 



```python

import pandas as pd
beton = pd.read_csv("Beton.csv", usecols = ["Salary"], squeeze = True)  #squeeze convert from dataframe to series

print(beton.is_unique) # boolen compare unique value

```


 <font color="blue"> OUTPUT: </font> 

    True


.is_unique function টি series এ কাজ করে। dataFrame এ কাজ করে না। তাই নিচের code টায় error আসবে। 


```python

import pandas as pd
beton2 = pd.read_csv("Beton.csv") 

print(beton2.is_unique) # boolen compare unique value

```


 <font color="blue"> OUTPUT: </font> 


    AttributeError: 'DataFrame' object has no attribute 'is_unique'



## .ndim

আমরা জানি series 1-Dimention আর DataFrame 2-Dimention. আমরা <font color="green">.ndim</font> এর দ্বারা dataset টা Series না কি DataFrame তা বঝতে পারা যায়। যদি output 1 হয় তবে 1-Dimention বা Series. আর যদি output 2 হয় তবে 2-Dimention বা DataFrame.


```python

import pandas as pd

#squeeze convert from dataframe to series
beton = pd.read_csv("Beton.csv", usecols = ["Salary"], squeeze = True) 
beton2 = pd.read_csv("Beton.csv")

print(beton.ndim)
print(beton2.ndim)

```


 <font color="blue"> OUTPUT: </font> 


    1 
    2 


-------



## .shape

dataset এ কত গুলো rows আর columns আছে তা <font color="green">.shape</font> এর দ্বারা বাহির করা যায়। output এ <font color="gray">(rows, columns)</font> এই রুপে দেখা যায়। 


```python

import pandas as pd

#squeeze convert from dataframe to series
beton = pd.read_csv("Beton.csv", usecols = ["Salary"], squeeze = True) 
beton2 = pd.read_csv("Beton.csv")

print(beton.shape)   # represent (row,column)
print(beton2.shape)

```

 <font color="blue"> OUTPUT: </font> 

    (30,)
    (30, 2)



--------



## .size

dataset এ null সহ total কতগুল value আছে  তা <font color="green">.size</font> এর দ্বারা দেখা যায়। output এ সব row এবং column এর total value count এর মান  numeric এ দেখা যায়। 



```python

import pandas as pd

#squeeze convert from dataframe to series
beton = pd.read_csv("Beton.csv", usecols = ["Salary"], squeeze = True) 
beton2 = pd.read_csv("Beton.csv")

print(beton.size)   # # total value include null
print(beton2.size)

```



 <font color="blue"> OUTPUT: </font> 

    30
    60 


--------


## .sort_values()

যদি কখনো dataset এর value sort করে দেখতে হয় মানে ascending order বা descending order এ নিতে হয় তবে <font color="green">.sort_values()</font> ব্যবহার করে তা করা যায়। defaultly ascending parameter টা True থাকে। 

```python

import pandas as pd

#squeeze convert from dataframe to series
beton = pd.read_csv("Beton.csv", usecols = ["Salary"], squeeze = True) 
beton2 = pd.read_csv("Beton.csv")


print(beton2.sort_values("Salary").head(4),'\n')   # ascending ordered
print(beton.sort_values().head(4),'\n')   # ascending ordered
print(beton.sort_values(ascending = False).tail(3))     # descending ordered

```


 <font color="blue"> OUTPUT: </font> 
 
| |YearsExperience   |   Salary |
| --------- | ----------- | ------ |
|2 | 1.5 | 37731.0 |
|0 | 1.1 | 39343.0 |
|4 | 2.2| 39891.0 |
|3 | 2.0 | 43525.0 |


------


|   |   |
| ----------- | ------ |
| 2 | 37731.0 |
| 0 | 39343.0 |
| 4 | 39891.0 |
| 3 | 43525.0 |

Name: Salary, dtype: float64



------


|   |   |
| ----------- | ------ |
| 4 | 39891.0 |
| 0 | 39343.0 |
| 2 | 37731.0 |

Name: Salary, dtype: float64


-----


## inplace Parameter

আমরা সবাই জানি যে যদি variable এ কোন operation ঘটে তাহলে আমাদের main data-set এ কোন change ঘটবে না। কিন্তু inplace Parameter ব্যবহার করে আমরা instandly variable এর change বা execution এর change টা কে data-set এর real-value তেও change ঘটাতে পারি। by-Defaultly <font color="green"> inplace = False </font> থাকে।


```python

import pandas as pd

salary2 = pd.read_csv("salary.csv", usecols = ["Salary"], squeeze = True)
print(salary2)

print(salary2.sort_values(ascending = False, inplace = True))
print(salary2)

```


 <font color="blue"> OUTPUT: </font> 
 

| |   |
| --------- | ----------- |
|0 | 72000.0 |
|1 | 48000.0 |
|2 | 54000.0|
|3 | 61000.0 |
|4 | NaN |
|5 | 58000.0 |
|6 | 52000.0|
|7 | 79000.0 |
|8 | 83000.0 |
|9 | 67000.0 |

Name: Salary, dtype: float64
None


------


| |   |
| --------- | ----------- |
|8 | 83000.0 |
|7 | 79000.0 |
|0 | 72000.0 |
|9 | 67000.0 |
|3 | 61000.0 |
|5 | 58000.0 |
|2 | 54000.0|
|6 | 52000.0|
|1 | 48000.0 |
|4 | NaN |

Name: Salary, dtype: float64


------


## .sort_index()


sort_index() টা অনেকটা sort_values() এর মত। sort_index() দ্বারা data-set এর index কে ascending বা deascending order এ sort করা যায়।  



```python

import pandas as pd

salary2 = pd.read_csv("salary.csv", usecols = ["Salary"], squeeze = True)
print(salary2)

print(salary2.sort_index(ascending = False, inplace = True))
print(salary2)

```


 <font color="blue"> OUTPUT: </font> 

 
| |   |
| --------- | ----------- |
|0 | 72000.0 |
|1 | 48000.0 |
|2 | 54000.0|
|3 | 61000.0 |
|4 | NaN |
|5 | 58000.0 |
|6 | 52000.0|
|7 | 79000.0 |
|8 | 83000.0 |
|9 | 67000.0 |

Name: Salary, dtype: float64
None

--------

| |   |
| --------- | ----------- |
|9 | 67000.0 |
|8 | 83000.0 |
|7 | 79000.0 |
|6 | 52000.0|
|5 | 58000.0 |
|4 | NaN |
|3 | 61000.0 |
|2 | 54000.0|
|1 | 48000.0 |
|0 | 72000.0 |

Name: Salary, dtype: float64


------


## in

data-set এ কাঙ্ক্ষিত data আছে কি নাই টা  <font color="green"> in </font> ব্যবহার করে check করে নিতে পারেন। যদি data টি data-set এ থেকে থাকে তা হইলে output <font color="pink"> True </font> এর যদি না থাকে তা হইলে output <font color="pink"> False </font>আসবে।  


```python

import pandas as pd

salary2 = pd.read_csv("salary.csv", usecols = ["Salary"], squeeze = True)
print(salary2)

print(67000.0 in salary2)
print(67000.0 in salary2.values)
print(2 in salary2)

```


 <font color="blue"> OUTPUT: </font> 
 

| |   |
| --------- | ----------- |
|0 | 72000.0 |
|1 | 48000.0 |
|2 | 54000.0|
|3 | 61000.0 |
|4 | NaN |
|5 | 58000.0 |
|6 | 52000.0|
|7 | 79000.0 |
|8 | 83000.0 |
|9 | 67000.0 |


Name: Salary, dtype: float64


||
| --- |
|False|
|True|
|True|



------



## index_col parameter

এতক্ষণ আমরা default index নিয়ে কাজ করছি but এখন আমরা দেখব কেমন করে data-set এর একটি column কে index এ রূপান্তর করা যায়। এর জন্য pd.read_csv তে একটা extra parmeter ব্যবহার করতে হবে output <font color="green"> index_col = "column এর নাম" </font>

```python

import pandas as pd
salaryy = pd.read_csv("salary.csv", index_col = "Salary", usecols = ["Age","Salary"] , squeeze = True)
print(salaryy)

```


 <font color="blue"> OUTPUT: </font> 


 Salary

| |   |
| --------- | ----------- |
 | 72000.0|44.0 |
 | 48000.0|27.0 |
 | 54000.0|30.0 |
 | 61000.0|38.0 |
 | NaN |40.0|
 | 58000.0|35.0 |
 | 52000.0 |NaN|
 | 79000.0|48.0 |
 | 83000.0|50.0 |
 | 67000.0|37.0 |

Name: Age, dtype: float64


------



## .get()

<font color="green"> .get() </font> ব্যবহার করে আমরা data-set এর index define করে উক্ত index এর value পেতে পারি। but যদি আমরা এমন কোন index define করি যা data-set এ নাই, তা হইলে আমরা error face করব। তাই .get() এ default parameter ব্যবহার করব।<font color="green"> .get() </font> এ ২টা parameter: key, default. <font color="green"> key= "columns name" </font> আর <font color="green"> default="data না পাইলে যে কোন কিছু comment" </font> দিতে পারেন, যা error এর পরিবর্তে যদি data না থাকে তবে দেখতে পাবেন। 

```python

import pandas as pd
salaryy = pd.read_csv("salary.csv", index_col = "Salary", usecols = ["Age","Salary"] , squeeze = True)
print(salaryy,"\n")

print(salaryy.get(key = [61000.0, 52000.0], default = "This is not a salary"),"\n")

print(salaryy.get(key = 200 , default = "This is not a salary"),"\n")


```


 <font color="blue"> OUTPUT: </font> 


 Salary

| |   |
| --------- | ----------- |
 | 72000.0|44.0 |
 | 48000.0|27.0 |
 | 54000.0|30.0 |
 | 61000.0|38.0 |
 | NaN |40.0|
 | 58000.0|35.0 |
 | 52000.0 |NaN|
 | 79000.0|48.0 |
 | 83000.0|50.0 |
 | 67000.0|37.0 |

Name: Age, dtype: float64


------


 Salary

| |   |
| --------- | ----------- |
 | 61000.0|38.0 |
 | 52000.0|NaN |

 
Name: Age, dtype: float64 

This is not a salary 



------



## Math Methods 

<font color="green"> dataseries.count() </font>: total কতগুলো data বা row আছে তা .count() এর দ্বারা দেখতে পারা যায়। NaN বা blank data .count() এ count করে না।

```python

import pandas as pd
salaryy = pd.read_csv("salary.csv", index_col = "Salary", usecols = ["Age","Salary"] , squeeze = True)
print(salaryy.count())

```


 <font color="blue"> OUTPUT: </font> 

    9


-------


<font color="green"> len(dataseries) </font>: len(series) method টা অনেকটা .count() এর similar,কিন্তু len() NaN বা blank data সহ সমস্ত data এর length count করে। 

```python

import pandas as pd
salaryy = pd.read_csv("salary.csv", index_col = "Salary", usecols = ["Age","Salary"] , squeeze = True)
print(len(salaryy))

```



 <font color="blue"> OUTPUT: </font> 

    10


------
  


<font color="green"> dataseries.sum()</font> :  dataseries এর data যদি numeric হয় তা হইলে আমরা .sum() ব্যবহার করে total যোগফল বাহির করতে পারি। 

```python

import pandas as pd
salaryy = pd.read_csv("salary.csv", index_col = "Salary", usecols = ["Age","Salary"] , squeeze = True)
print(salaryy.sum())

```


 <font color="blue"> OUTPUT: </font> 

    349.0


------


<font color="green"> dataseries.mean() </font>: dataseries এর data যদি numeric হয় তা হইলে আমরা .mean() ব্যবহার করে total data এর গড় বাহির করতে পারি।

```python

import pandas as pd

salaryy = pd.read_csv("salary.csv", index_col = "Salary", usecols = ["Age","Salary"] , squeeze = True)
print(salaryy.mean())

```



 <font color="blue"> OUTPUT: </font> 

    38.77777777777778



------



<font color="green"> dataseries.std() </font> : dataseries এর data যদি numeric হয় তা হইলে আমরা .std() ব্যবহার করে total data এর standard deviation বাহির করতে পারি।

```python

import pandas as pd

salaryy = pd.read_csv("salary.csv", index_col = "Salary", usecols = ["Age","Salary"] , squeeze = True)
print(salaryy.std())

```


 <font color="blue"> OUTPUT: </font> 

    7.693792591722527


-------



<font color="green"> dataseries.min() </font> : dataseries এর data যদি numeric হয় তা হইলে আমরা .min() ব্যবহার করে total data এর সব থেকে minimum vaule বাহির করতে পারি।

```python

import pandas as pd

salaryy = pd.read_csv("salary.csv", index_col = "Salary", usecols = ["Age","Salary"] , squeeze = True)
print(salaryy.min())

```



 <font color="blue"> OUTPUT: </font> 

    27.0


-------




<font color="green"> dataseries.max() </font> : dataseries এর data যদি numeric হয় তা হইলে আমরা .max() ব্যবহার করে total data এর সব থেকে maximum vaule বাহির করতে পারি।

```python

import pandas as pd

salaryy = pd.read_csv("salary.csv", index_col = "Salary", usecols = ["Age","Salary"] , squeeze = True)
print(salaryy.max())

```


 <font color="blue"> OUTPUT: </font> 

    50.0



-------





<font color="green"> dataseries.median() </font> : dataseries এর data যদি numeric হয় তা হইলে আমরা .median() ব্যবহার করে total data এর mid point vaule বাহির করতে পারি।



```python

import pandas as pd

salaryy = pd.read_csv("salary.csv", index_col = "Salary", usecols = ["Age","Salary"] , squeeze = True)
print(salaryy.median()) # give mid point value 

```



 <font color="blue"> OUTPUT: </font> 

    38.0




-------




<font color="green"> dataseries.mode() </font> : dataseries এর data যদি numeric হয় তা হইলে আমরা .mode() ব্যবহার করে total data এর most frequently data বাহির করতে পারি।



```python

import pandas as pd

salaryy = pd.read_csv("salary.csv", index_col = "Salary", usecols = ["Age","Salary"] , squeeze = True)
print(salaryy.mode())

```



 <font color="blue"> OUTPUT: </font> 

| |   |
| --------- | ----------- |
|0 | 27.0 |
|1 | 30.0 |
|2 | 35.0|
|3 | 37.0 |
|4 | 38.0 |
|5 | 40.0 |
|6 | 44.0|
|7 | 48.0 |
|8 | 50.0 |

dtype: float64



-------




<font color="green"> dataseries.describe() </font> : আমরা data-set এর overview পাইতে চাইলে .describe() ব্যবহার করে <font color="gray"> count </font> row তে NaN ছাড়া total কতটা row আছে তা দেখতে পাই। <font color="gray"> mean </font> row তে total row এর গড় দেখতে পাই। <font color="gray"> std </font> row তে dataseries এর standerd devision এর মান দেখতে পাই।<font color="gray"> min </font> row তে NaN ছাড়া minimum value দেখতে পাই।এ ছাড়া <font color="gray"> 25%,50%,75% </font> row তে total value এর 25% এর বা 50%এর বা 75%এর value কত হইতে পারে তা দেখতে পাই।



```python

import pandas as pd

salaryy = pd.read_csv("salary.csv", index_col = "Salary", usecols = ["Age","Salary"] , squeeze = True)
print(salaryy.describe())

```



 <font color="blue"> OUTPUT: </font> 

| |   |
| --------- | ----------- |
|count | 9.000000|
|mean | 38.777778|
|std | 7.693793|
|min | 27.000000|
|25% | 35.000000|
|50% | 38.000000|
|75% | 44.000000|
|max | 50.000000|

Name: Age, dtype: float64




--------




## .idxmax() AND .idxmin() :

আমরা তো maximum বা minimum value বাহির করতে পারি। এখন দেখব কেমনে আমরা max বা min এর index বাহির করতে পারি। .idxmax() দ্বারা আমরা maximum value এর index এবং .idxmin() দ্বারা minimum value এর index পাইতে পারি।



```python

import pandas as pd
salaryy = pd.read_csv("salary.csv", index_col = "Salary", usecols = ["Age","Salary"] , squeeze = True)

print(salaryy.max())
print(salaryy.idxmax())  #1

print(salaryy[83000.0])  #2

print(salaryy[salaryy.idxmin()])  # together 2[1]

```



 <font color="blue"> OUTPUT: </font> 

    50.0
    83000.0
    50.0
    27.0



---------



## .value_counts() :

আমরা চাইলে কোন value কতবার আছে তা <font color="green"> .value_counts() </font> এর দ্বারা দেখতে পারি। 


```python

import pandas as pd
salaryy = pd.read_csv("salary.csv", index_col = "Salary", usecols = ["Age","Salary"] , squeeze = True)


print(salaryy.value_counts())  # count repeted value +1

print(salaryy.value_counts().sum()) 
print(salaryy.count())  # same as sum of value_counts()

```


 <font color="blue"> OUTPUT: </font> 

| |   |
| --------- | ----------- |
|37.0 | 1 |
|50.0 | 1 |
|48.0 | 1|
|35.0 | 1 |
|40.0 | 1 |
|38.0 | 1 |
|30.0 | 1|
|27.0 | 1 |
|44.0 | 1 |

Name: Age, dtype: int64

    9
    9


-------




## .apply() :

আমরা data-preprocessing এর জন্য .apply() function use করতে পারি। আমাদের data-set এর কোন column এর সকল ভালু যদি একটা flow তে change করতে চাই তা হইলে <font color="green"> .apply() </font> ব্যবহার করে তা আমরা করতে পারি। .apply() এর জন্য একটি function প্রয়োজন হয়। আমরা annonimus function ব্যবহার করতে পারি। যেমন lambda function. আমরা একটি উদাহারন এ age column এর সব মান ১০০ গুন বাড়ায়ে দেখব।



```python

import pandas as pd
salaryy = pd.read_csv("salary.csv", index_col = "Salary", usecols = ["Age","Salary"] , squeeze = True)

salaryy.apply(lambda age : age * 100)

```

 <font color="blue"> OUTPUT: </font> 


 Salary

| |   |
| --------- | ----------- |
 | 72000.0|4400.0 |
 | 48000.0|2700.0 |
 | 54000.0|3000.0 |
 | 61000.0|3800.0 |
 | NaN |4000.0|
 | 58000.0|3500.0 |
 | 52000.0 |NaN|
 | 79000.0|4800.0 |
 | 83000.0|5000.0 |
 | 67000.0|3700.0 |

Name: Age, dtype: float64



-------



## .map()


আমরা যদি একাধিক dataset কে একটি dataset এ রূপান্তর করতে চাই তা হইলে আমরা <font color="green"> .map() </font>  ব্যবহার করতে পারি। series_value.map(compare_argoment_series). series_value এর column-data এর সঙ্ঘে compare_argoment_series এর index compare হয়। আর নতুন যে series তৈরি হবে, তার index হবে series_value এর column আর compare_argoment_series এর columns গুলো নতুন series এর columns হবে। 


```python

import pandas as pd

salary = pd.read_csv("salary.csv", index_col = "Salary", usecols = ["Age","Salary"] , squeeze = True)

age = pd.read_csv("salary.csv", index_col = "Age", usecols = ["Age","Salary"] , squeeze = True)

print(age.map(salary))

```


 <font color="blue"> OUTPUT: </font> 


Age

| |   |
| --------- | ----------- |
 | 44.0|44.0 |
 | 27.0 |27.0 |
 | 30.0 |30.0 |
 | 38.0|38.0 |
 | 40.0 |40.0|
 | 35.0|35.0 |
 | NaN |NaN|
 | 48.0|48.0 |
 | 50.0|50.0 |
 | 37.0|37.0 |

Name: Salary, dtype: float64




-----

-------

















