---
title: Pandas merging Joining Concatenating
keywords: Pandas Bangla Tutorials, bangla Pandas, Bangla Python, Data Preprocessing Bangla, Monad wizard
last_updated: July 20, 2020
tags: [getting_started]
summary: "python bangla blog post এর দ্বারা Pandas Library এর concatination, join, merge related method গুলো আলোচিত হয়েছে । "
sidebar: mydoc_sidebar
permalink: pandas_mergingJoiningConcatenating.html
folder: mydoc
---

# pandas pandas_mergingJoiningConcatenating comming soon


[প্রয়োজনীয় data-set যা এই post এ ব্যবহার করা হয়েছে DOWNLOAD ](https://github.com/dust-nk-org/pandasDataSet/archive/master.zip)

এবং [Official Doc](https://pandas.pydata.org/)

### .concat() method

.concat() method ব্যবহার করে আমরা same length এর একাধিক data-frame কে একটি data-frame এ রূপান্তর করতে পারি বা একাধিক data কে এক সঙ্ঘে concatination করতে পারি। 

সাধারণত obj signature নিয়ে কাজ করা যায়।
কিন্তু প্রয়োজন এর তাগিদে আমাদের আর ও কিছু signature ব্যবহার করতে হতে পারে। যেমন 
<font color="pink"> ignore_index </font> ব্যবহার করলে একটি continous indexing পাওয়া যায়। তা না হইলে আমাদের 1st data-frame এর index 2nd data-frame এর index মিলে problem হতে পারে। 
<font color="pink"> keys </font> ব্যবহার করে আমরা external Index তৈরি করতে পারি। 
<font color="pink"> names </font> ব্যবহার করে আমরা multi-Index গুলোর specific নাম দিতে পারি।  

<font color="green"> pandas.concat(objs, keys, names, ignore_index) </font>

<font color="Salmon"> Example: </font>


```python
import pandas as pd

week1 = pd.read_csv("Restaurant - Week 1 Sales.csv")
week2 = pd.read_csv("Restaurant - Week 2 Sales.csv")

len(week1)    # same length
len(week2)

wek1and2_index = pd.concat([week1, week2])
wek1and2_index.tail()

#  create continous numaric index
wek1and2 = pd.concat([week1, week2], ignore_index = True)

# create external index with key1 for obj1 and key2 for obj2
sales = pd.concat(objs= [week1, week2], keys= ["week1", "week2"])

# extract only week1 external row
sales.loc["week1"]

# extract whoes CustomerID 240 and external index week2
sales.loc[("week2", 240)]

# extract thoes all other datas whoes CustomerID 240 and external index week2
sales.loc[("week2", 240), "Customer ID"]

# we can change index label name 
sales = pd.concat(objs=[week1, week2], keys=["week1", "week2"], names=['data frames', 'indexs'])

sales.head()

```


<font color="Salmon"> OUTPUT: </font>




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Customer ID</th>
      <th>Food ID</th>
    </tr>
    <tr>
      <th>data frames</th>
      <th>indexs</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">week1</th>
      <th>0</th>
      <td>537</td>
      <td>9</td>
    </tr>
    <tr>
      <th>1</th>
      <td>97</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>658</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>202</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>155</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>



### .append() method

.append() method অনেকটাই .concat() method এর মত। .concat() সরাসরি pandas কে call করে, আর .append() দ্বারা specific data-frame কে call করতে হয়। 

<font color="green"> dataFrame1.append(dataFrame2, ignore_index=True) </font>

<font color="Salmon"> Example: </font>


```python

import pandas as pd

week1 = pd.read_csv("Restaurant - Week 1 Sales.csv")
week2 = pd.read_csv("Restaurant - Week 2 Sales.csv")

week1_2 = week2.append(week1, ignore_index = True)  # work same as concat method
week1_2.head()

```




<font color="Salmon"> OUTPUT: </font>





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Customer ID</th>
      <th>Food ID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>688</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>813</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>495</td>
      <td>10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>189</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>267</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



## .merge() Method

### left_on and right_on parameters

২টি data-set কে একত্রে আনার প্রক্রিয়াই marging.

<font color="green"> pandas.merge(leftDataFrame, rightDataFrame, how, left_on, right_on) </font>

pandas কে merge method দ্বারা call করে signuture গুলোতে সঠিক data পাঠিয়ে marge করতে পারি। how parameter এ define করতে হবে merge টাই left dataFrame এ নাকি right dataFrame প্রথমে থাকবে । left_on এ left dataFrame এর specific label এবং right_on এ right dataFrame এর specific label থাকবে। 

same type এর যে কোন label দ্বারা index define করে merge data কে compare করা যায়। 


<font color="Salmon"> Example: </font>


```python
import pandas as pd

week1 = pd.read_csv("Restaurant - Week 1 Sales.csv")
customers = pd.read_csv("Restaurant - Customers.csv", index_col = "ID")  # define index column cause data frame have extra number column serial

mergeData= pd.merge(week1, customers, how = "left", left_on = "Customer ID", right_on = "ID")
mergeData.head()
```





<font color="Salmon"> OUTPUT: </font>





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Customer ID</th>
      <th>Food ID</th>
      <th>First Name</th>
      <th>Last Name</th>
      <th>Gender</th>
      <th>Company</th>
      <th>Occupation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>537</td>
      <td>9</td>
      <td>Cheryl</td>
      <td>Carroll</td>
      <td>Female</td>
      <td>Zoombeat</td>
      <td>Registered Nurse</td>
    </tr>
    <tr>
      <th>1</th>
      <td>97</td>
      <td>4</td>
      <td>Amanda</td>
      <td>Watkins</td>
      <td>Female</td>
      <td>Ozu</td>
      <td>Account Coordinator</td>
    </tr>
    <tr>
      <th>2</th>
      <td>658</td>
      <td>1</td>
      <td>Patrick</td>
      <td>Webb</td>
      <td>Male</td>
      <td>Browsebug</td>
      <td>Community Outreach Specialist</td>
    </tr>
    <tr>
      <th>3</th>
      <td>202</td>
      <td>2</td>
      <td>Louis</td>
      <td>Campbell</td>
      <td>Male</td>
      <td>Rhynoodle</td>
      <td>Account Representative III</td>
    </tr>
    <tr>
      <th>4</th>
      <td>155</td>
      <td>9</td>
      <td>Carolyn</td>
      <td>Diaz</td>
      <td>Female</td>
      <td>Gigazoom</td>
      <td>Database Administrator III</td>
    </tr>
  </tbody>
</table>
</div>



### Merging by Indexes ( left_index & right_index) Parameters

by-Default left_index এবং right_index এর মান False থাকে, merge করার সময় left Data-Frame বা right Data-Frame এর index কে main index হিসেবে ব্যবহার করার জন্য specific index এর মান True দিতে হবে। 

<font color="green"> leftDataFrame.merge(rightDataFrame, how, left_on, right_on, left_index, right_index, suffixes=["lastNameForLeft", "LastNameForRight"]) </font>

* how তে left merge না কি right merge টা দিতে হবে,
* left DataFrame এর index হিসেবে যদি label ব্যবহার করা হয় তবে টা left_on এ দিতে হবে। unless দিতে হবে না।  
* right DataFrame এর index হিসেবে যদি label ব্যবহার করা হয় তবে টা right_on এ দিতে হবে।  unless দিতে হবে না।
* left DataFrame এর index হিসেবে যদি left DataFrame এর index ব্যবহার করা হয় তবে left_index = True দিতে হবে। unless দিতে হবে না।  
* right DataFrame এর index হিসেবে যদি right DataFrame এর index ব্যবহার করা হয় তবে right_index = True দিতে হবে।  unless দিতে হবে না।
*  merge data চেনার জন্য যদি specific data-frame এর সকল label এর সঙ্ঘে specific কোন word add করতে চাই তা হইলে suffixes parameter ব্যবহার করতে হবে। 

<font color="Salmon"> Example: </font>


```python
import pandas as pd

week1 = pd.read_csv("Restaurant - Week 1 Sales.csv")
week2 = pd.read_csv("Restaurant - Week 2 Sales.csv")
customers = pd.read_csv("Restaurant - Customers.csv", index_col = "ID")  # define index column cause data frame have extra number column serial
food = pd.read_csv("Restaurant - Foods.csv",  index_col = "Food ID")
food.head()

""" 
use for marge with index value or marge with index and column
"""
sales = week1.merge(customers, how = "left", left_on = "Customer ID", right_index = True)

# now marge with foods data set to add food details with sales 

sales.merge(food, how = "left", left_on = "Food ID", right_index = True)
sales.head()


# merge by Index In both datasets and include suffixes name on label
week1.merge(week2, how = "left", left_index = True, right_index = True, suffixes = ["-week1", "-week2"])


```





<font color="Salmon"> OUTPUT: </font>





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Customer ID-week1</th>
      <th>Food ID-week1</th>
      <th>Customer ID-week2</th>
      <th>Food ID-week2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>537</td>
      <td>9</td>
      <td>688</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>97</td>
      <td>4</td>
      <td>813</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>658</td>
      <td>1</td>
      <td>495</td>
      <td>10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>202</td>
      <td>2</td>
      <td>189</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>155</td>
      <td>9</td>
      <td>267</td>
      <td>3</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>245</th>
      <td>413</td>
      <td>9</td>
      <td>783</td>
      <td>10</td>
    </tr>
    <tr>
      <th>246</th>
      <td>926</td>
      <td>6</td>
      <td>556</td>
      <td>10</td>
    </tr>
    <tr>
      <th>247</th>
      <td>134</td>
      <td>3</td>
      <td>547</td>
      <td>9</td>
    </tr>
    <tr>
      <th>248</th>
      <td>396</td>
      <td>6</td>
      <td>252</td>
      <td>9</td>
    </tr>
    <tr>
      <th>249</th>
      <td>535</td>
      <td>10</td>
      <td>249</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
<p>250 rows × 4 columns</p>
</div>



### .join() Method

.merge() method এর মত .join() method ব্যবহার করে আমরা ২টি data-frame কে একটি data-frame এ রূপান্তর করতে পারি। 
সাধারণত <font color="Salmon"> leftDataFrame.join(rightDataFrame) </font> ব্যবহার করে পাশাপাশি 2 টি DataFrame কে join করা যায়। 

<font color="Salmon"> Example: </font>


```python
import pandas as pd

week1 = pd.read_csv("Restaurant - Week 1 Sales.csv")
satisfaction = pd.read_csv("Restaurant - Week 1 Satisfaction.csv")

# use for join 2 dataSet with out extra parameter
week1.join(satisfaction).head()


```




<font color="Salmon"> OUTPUT: </font>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Customer ID</th>
      <th>Food ID</th>
      <th>Satisfaction Rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>537</td>
      <td>9</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>97</td>
      <td>4</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>658</td>
      <td>1</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>202</td>
      <td>2</td>
      <td>7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>155</td>
      <td>9</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>



![image](https://drive.google.com/uc?export=view&id=1TIhNLVA2FFsz_FsaNoLnuT_xwgWumUlk)

### inner Joins (inner marge)

২ টা data-frame এর মদ্ধে common value গুলো মিলে new data-frame তৈরি করলে inner-join করা হয়। 
join করার সময় notice করতে হবে যেন ২ টা data-frame এ same Name এবং same size এর common label থাকে, যে label টার উপর deppend করে আমাদের inner join complete হবে। 

<mark>সকল প্রকার join করতে .marge() method এর how parameter এর পরিবর্তন ঘটাতে হয়। </mark>  

<font color="green"> leftDataFrame.merge(rightDataFrame, how="inner", left_on, right_on, left_index, right_index, suffixes=["lastNameForLeft", "LastNameForRight"]) </font>


<font color="Salmon"> Example: </font>


```python
import pandas as pd

week1 = pd.read_csv("Restaurant - Week 1 Sales.csv")
week2 = pd.read_csv("Restaurant - Week 2 Sales.csv")

""" try to find which customer are came on week1 and week2 both """

# both dataset have same name of column "Customer ID" so it defaultly create "Customer ID_x""Customer ID_y" for reduse duplicate column name
week1.merge(week2, how = "inner", on = "Customer ID").head(4)

# now give some specific name to "Customer ID"
week1.merge(week2, how = "inner", on = "Customer ID",suffixes = [" - week 1"," - week 2"]).head(4)

""" try to find which customer are came on both week1 and week2 both and ordered exjact same product to both week1 & week2"""
week1.merge(week2, how = "inner", on = ["Customer ID", "Food ID"]).head(4)




```






<font color="Salmon"> OUTPUT: </font>





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Customer ID</th>
      <th>Food ID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>304</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>540</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>937</td>
      <td>10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>233</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



### outer Joins (outer marge)

উপরের picture এ সকল join এ কি ঘটে তা দাওয়া হয়েছে। আপনারা যদি উপরের topic গুলো ভাল মত বুঝতে পারেন এবং SQL এর join topic জেনে থাকেন তা হইলে code এর flow অনুসরণ করুন এবং line by line code run করুন। আশা করি বুঝতে পারবেন। 

inner join এর similar. just how="outer"

<font color="green"> leftDataFrame.merge(rightDataFrame, how="outer", left_on, right_on, left_index, right_index, suffixes=["lastNameForLeft", "LastNameForRight"]) </font>


<font color="Salmon"> Example: </font>


```python

import pandas as pd

week1 = pd.read_csv("Restaurant - Week 1 Sales.csv")
week2 = pd.read_csv("Restaurant - Week 2 Sales.csv")
customers = pd.read_csv("Restaurant - Customers.csv")
food = pd.read_csv("Restaurant - Foods.csv")

""" try to find which customer are not came on week1 and week2 both """

# both dataset have same name of column "Customer ID" so it defaultly create "Customer ID_x""Customer ID_y" for reduse duplicate column name
week1.merge(week2, how = "outer", on = "Customer ID").head(4)

# NaN found when those costomer is not found in column
# now give some specific name to "Customer ID".  indicator parameter define where the value is
marged = week1.merge(week2, how = "outer", on = "Customer ID",
                     suffixes = [" - week 1"," - week 2"], indicator = True)

len(marged)  # 454 rows have not similar value 


""" try to find which customer are not came on both week1 and week2 both and ordered exjact same product to both week1 & week2"""
week1.merge(week2, how = "outer", on = ["Customer ID", "Food ID"]).head(4)


# total discription
marged["_merge"].value_counts()


```




<font color="Salmon"> OUTPUT: </font>





    right_only    197
    left_only     195
    both           62
    Name: _merge, dtype: int64



### left Joins (left marge)

.merge() method এ যে example দেখেছেন তা left join এর উদাহরণ। 

how = "left" ব্যবহার করে বাকি সব same. 

just আপনাদের join বাপার টার visual flow মনে রাখতে হবে এবং কেন কোন merge ব্যবহার করবেন টা নিশ্চিত করতে হবে।  

<font color="Salmon"> Example: </font>


```python

import pandas as pd

week1 = pd.read_csv("Restaurant - Week 1 Sales.csv")
week2 = pd.read_csv("Restaurant - Week 2 Sales.csv")
customers = pd.read_csv("Restaurant - Customers.csv")
food = pd.read_csv("Restaurant - Foods.csv")


""" try to find which food item buy customer on week1 """ # so food ID is our matching column
buy = week1.merge(food, how = "left", on = "Food ID", sort = True) # it's sort with matching column
buy.head()


```




<font color="Salmon"> OUTPUT: </font>





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Customer ID</th>
      <th>Food ID</th>
      <th>Food Item</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>658</td>
      <td>1</td>
      <td>Sushi</td>
      <td>3.99</td>
    </tr>
    <tr>
      <th>1</th>
      <td>600</td>
      <td>1</td>
      <td>Sushi</td>
      <td>3.99</td>
    </tr>
    <tr>
      <th>2</th>
      <td>155</td>
      <td>1</td>
      <td>Sushi</td>
      <td>3.99</td>
    </tr>
    <tr>
      <th>3</th>
      <td>341</td>
      <td>1</td>
      <td>Sushi</td>
      <td>3.99</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20</td>
      <td>1</td>
      <td>Sushi</td>
      <td>3.99</td>
    </tr>
  </tbody>
</table>
</div>



### right Joins (right marge)


how = "right" ব্যবহার করে বাকি সব same. 

just আপনাদের join বাপার টার visual flow মনে রাখতে হবে এবং কেন কোন merge ব্যবহার করবেন টা নিশ্চিত করতে হবে।  

<font color="Salmon"> Example: </font>


```python

import pandas as pd

week1 = pd.read_csv("Restaurant - Week 1 Sales.csv")
week2 = pd.read_csv("Restaurant - Week 2 Sales.csv")
customers = pd.read_csv("Restaurant - Customers.csv")
food = pd.read_csv("Restaurant - Foods.csv")


""" try to find which food item buy customer on week1 """ # so food ID is our matching column
buy = food.merge(week1, how = "right", on = "Food ID", sort = True) # it's sort with matching column
buy.head()


```






<font color="Salmon"> OUTPUT: </font>







<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Food ID</th>
      <th>Food Item</th>
      <th>Price</th>
      <th>Customer ID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Sushi</td>
      <td>3.99</td>
      <td>658</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Sushi</td>
      <td>3.99</td>
      <td>600</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>Sushi</td>
      <td>3.99</td>
      <td>155</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>Sushi</td>
      <td>3.99</td>
      <td>341</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>Sushi</td>
      <td>3.99</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>



### Drop label

যদি merged data-frame এ অপ্রয়োজনীয় label এবং data থাকে তা হইলে .drop() method ব্যবহার করব। 

<font color="Salmon"> Example: </font>

<mark> 
When marged column have not same name then we cann't work with previous marge or join system.
matching or comparing columns always need same name. If that's not happend then we need extra 2 parameter left_on & right_on


</mark>



```python

import pandas as pd

week1 = pd.read_csv("Restaurant - Week 1 Sales.csv")
week2 = pd.read_csv("Restaurant - Week 2 Sales.csv")
customers = pd.read_csv("Restaurant - Customers.csv")
food = pd.read_csv("Restaurant - Foods.csv")

week2.merge(customers, how = "left", left_on = "Customer ID", right_on = "ID") # "Customer ID" & "ID" same so we don't need duplicate column
 
week2CustomerDemo = week2.merge(customers, how = "left", left_on = "Customer ID", 
                                right_on = "ID", sort = True).drop("ID", axis= "columns")  # now ID column is drop
week2CustomerDemo.head()


```




<font color="Salmon"> OUTPUT: </font>





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Customer ID</th>
      <th>Food ID</th>
      <th>First Name</th>
      <th>Last Name</th>
      <th>Gender</th>
      <th>Company</th>
      <th>Occupation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>8</td>
      <td>6</td>
      <td>Frances</td>
      <td>Adams</td>
      <td>Female</td>
      <td>Dabshots</td>
      <td>Developer III</td>
    </tr>
    <tr>
      <th>1</th>
      <td>13</td>
      <td>2</td>
      <td>Ruth</td>
      <td>Alvarez</td>
      <td>Female</td>
      <td>Twitterlist</td>
      <td>Mechanical Systems Engineer</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21</td>
      <td>4</td>
      <td>Albert</td>
      <td>Burns</td>
      <td>Male</td>
      <td>Rhynoodle</td>
      <td>Junior Executive</td>
    </tr>
    <tr>
      <th>3</th>
      <td>24</td>
      <td>8</td>
      <td>Donna</td>
      <td>Thomas</td>
      <td>Female</td>
      <td>Jaxbean</td>
      <td>Chief Design Engineer</td>
    </tr>
    <tr>
      <th>4</th>
      <td>27</td>
      <td>4</td>
      <td>Jessica</td>
      <td>Bennett</td>
      <td>Female</td>
      <td>Twitternation</td>
      <td>Account Executive</td>
    </tr>
  </tbody>
</table>
</div>











