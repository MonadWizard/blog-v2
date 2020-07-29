---
title: Pandas multi Index
keywords: Pandas Bangla Tutorials, bangla Pandas, Bangla Python, Data Preprocessing Bangla, Monad wizard
last_updated: July 20, 2020
tags: [getting_started]
summary: "python bangla blog post এর দ্বারা Pandas Library এর MultiIndex related method গুলো আলোচিত হয়েছে ।"
sidebar: mydoc_sidebar
permalink: pandas_multiIndex.html
folder: mydoc
---

## .set_index() Method

[প্রয়োজনীয় data-set যা এই post এ ব্যবহার করা হয়েছে DOWNLOAD ](https://github.com/dust-nk-org/pandasDataSet/archive/master.zip)

এবং [Official Doc](https://pandas.pydata.org/)

আমরা পূর্বেই দেখেছি যে, set_index() method ব্যবহার করে আমরা যে কোন column কে Index বানিয়ে ব্যবহার করতে পারি। কিন্তু যদি আমাদের nested index এর প্রয়োজন হয় তা হইলে আমরা আমাদের একাধিক index এর নাম .set_index() এর মাদ্ধমে defain করতে পারি। .set_index() এর parameter <font color="green"> key </font> তে আমরা column নাম Index হিসেবে define করি। 

উদাহরণ হিসেবে আমরা নির্দিষ্ট data এ কোন country তে macBook এর price কত ছিল অথবা নির্দিষ্ট country তে কোন date এ MacBook এর price কত ছিল তা জানার জন্য আমাদের multiple index এর প্রয়োজন হয়।


আমরা multi-index এ <font color="green"> dataFrame.sort_index() </font> ব্যবহার করে আমরা Multiple Index কে একটার পর একটা Sort করতে পারি।  

আমরা <font color="green"> dataFrame.index.names </font> ব্যবহার করে Index গুলোর নাম দেখতে পারি। 
এবং <font color="green"> type(dataFrame.index) </font> ব্যবহার করে Data Type দেখতে পাই MultiIndex। 


<font color="blue"> Example: </font>


```python

import pandas as pd

bigmac = pd.read_csv("bigmac.csv", parse_dates = ["Date"])
bigmac.head(3)

bigmac.set_index(keys = ["Date","Country"], inplace = True)  # work with respected Index data as mach as a layer keys=[Index1,Index2]
bigmac.head(3)

bigmac.sort_index() # sort data in alpha numaric. here Now Date Is 1st index, country is 2nd index


# see name of Index by
bigmac.index.names
bigmac.index.names[0]


# we can see its type as multindex by
type(bigmac.index)


```


<font color="blue"> OUTPUT: </font>



    pandas.core.indexes.multi.MultiIndex



## .get_level_values() Method

আমরা data-frame define করার সময়ই <font color="green"> index_col=["column1", "column2"] </font> define করার মাদ্ধমে multi-index ডিফাইন করতে পারি। set_index() method এর বদলে index_col ব্যবহার করা যায়। কিন্তু good practice হিসেবে আমি set_index() method কে prefer করি।  

multi index এর ক্ষেত্রে যদি আমাদের specific index এর data নিয়ে কাজ করতে হয় তা হইলে <font color="green">dataFrame.index </font> এর দ্বারা প্রয়োজনীয় index diclar করা যায়। আমরা index এর নাম অথবা index এর possition define করে index এর সব data pick করতে পারি। 

অথবা specific index এর value data-frame হিসেবে পেতে হইলে  <font color="green">.get_level_values() </font> ব্যবহার করতে হবে।

<font color="green"> dataFrame.index.get_level_values() </font> তে আমরা index এর নাম অথবা index এর possition define করে index এর সব data এর একটি data-frame পেতে পারি। 



<font color="blue"> Example </font>


```python

import pandas as pd

bigmac = pd.read_csv("bigmac.csv", parse_dates = ["Date"], index_col = ["Date", "Country"])
bigmac.sort_index(inplace = True)
bigmac.head(3)

# we can see all index by
bigmac.index
bigmac.index[0]

# we can see the value of our index by
bigmac.index.get_level_values(1)
bigmac.index.get_level_values("Date")


```

<font color="blue"> OUTPUT: </font>



    DatetimeIndex(['2010-01-01', '2010-01-01', '2010-01-01', '2010-01-01',
                   '2010-01-01', '2010-01-01', '2010-01-01', '2010-01-01',
                   '2010-01-01', '2010-01-01',
                   ...
                   '2016-01-01', '2016-01-01', '2016-01-01', '2016-01-01',
                   '2016-01-01', '2016-01-01', '2016-01-01', '2016-01-01',
                   '2016-01-01', '2016-01-01'],
                  dtype='datetime64[ns]', name='Date', length=652, freq=None)



## .set_names() Method

অনেক সময় data-frame এর column's name বা label's name পরিবর্তন করার প্রয়োজন হয় এই ক্ষেত্রে <font color="green"> dataframe.index.set_names(["1st Label New Name","2ne Label New Name"]) </font> ব্যবহার করতে পারি।

যদি আমরা কোন label's name পরিবর্তন করতে না চাই তা হইলে আমরা label টার যে নাম আছে তাই New Name এ ব্যবহার করব।


<font color="blue"> Example </font>


```python
import pandas as pd

bigmac = pd.read_csv("bigmac.csv", parse_dates = ["Date"], index_col = ["Date", "Country"])
bigmac.sort_index(inplace = True)
bigmac.head(3)


# We can change our Index Name By set new index name as
bigmac.index.set_names(["Day", "Location"], inplace = True)
bigmac.head(3)

```

<font color="blue"> OUTPUT: </font>



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
      <th>Price in US Dollars</th>
    </tr>
    <tr>
      <th>Day</th>
      <th>Location</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">2010-01-01</th>
      <th>Argentina</th>
      <td>1.84</td>
    </tr>
    <tr>
      <th>Australia</th>
      <td>3.98</td>
    </tr>
    <tr>
      <th>Brazil</th>
      <td>4.76</td>
    </tr>
  </tbody>
</table>
</div>



## .sort_index() Method

আমরা জানি .sort_index() এর দ্বারা data-frame এর index এর value গুলো sort করা যায়। 

multi index এ label value গুলো যদি random order বা custom order এ sort করতে চাই তা হইলে আমাদের ascinding = True বা ascinding = False(decending) define করতে হবে। একটা list এর দ্বারা সকল index এর sort type define boolen formate এ define করা যায়। <font color="green"> dataFrame.sort_index(ascending = [boolen, boolen]) </font> দ্বারা define করা হয়। 

<font color="blue"> Example </font>


```python
import pandas as pd

bigmac = pd.read_csv("bigmac.csv", parse_dates = ["Date"], index_col = ["Date", "Country"])
bigmac.sort_index(inplace = True)
bigmac.head(3)


# we can sort all as ascending/discending or can be sort specific order in maltiIndex as
bigmac.sort_index(ascending = [True, False], inplace = True) # we sort Date ascending and Country Descending
bigmac.head()


```


<font color="blue"> OUTPUT: </font>



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
      <th>Price in US Dollars</th>
    </tr>
    <tr>
      <th>Date</th>
      <th>Country</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">2010-01-01</th>
      <th>Uruguay</th>
      <td>3.32</td>
    </tr>
    <tr>
      <th>United States</th>
      <td>3.58</td>
    </tr>
    <tr>
      <th>Ukraine</th>
      <td>1.83</td>
    </tr>
    <tr>
      <th>UAE</th>
      <td>2.99</td>
    </tr>
    <tr>
      <th>Turkey</th>
      <td>3.83</td>
    </tr>
  </tbody>
</table>
</div>



## .loc()   Extract Rows from  MultiIndex

আমরা data-frame থেকে specific label value এর অন্তর্গত সব value এর একটি নতুন data-frame পাওয়ার জন্য <font color="green"> dataframe.loc[("outer_index_value_name", "inner_index_value_name"), "label_name" ] </font> এই syntex ব্যবহার করতে পারি।  
উদাহরণ স্বরূপ আপনি specific কোন outer index data এর অন্তর্গত সকল value পেতে পারি । বা specific কোন outer index data এর অন্তর্গত specific কোন inner index data এর সকল value পেতে পারি। বা বা specific কোন outer index data এর অন্তর্গত specific কোন inner index data এর সকল value নির্দিষ্ট কিছু label এর জন্য পেতে পারি। 


*NOTE: 'ix' pandas 1.0.0 থেকে remove করে দেওয়া হয়েছে , পূর্বের version গুলোতে কাজ করে। install previous version যদি .ix[] use করতে হয়। conda install pandas=0.25.1*

<font color="blue"> Example </font>


```python
import pandas as pd

bigmac = pd.read_csv("bigmac.csv", parse_dates = ["Date"], index_col = ["Date", "Country"])
bigmac.sort_index(inplace = True)
bigmac.head(3)

'''
# same  using .ix()                # .ix() need pandas 0.25 version
bigmac.ix[("2010-01-01","China")] 
bigmac.ix[("2010-01-01","China"), 0] # if we have more column we can be define after index tuple
'''

# loc accept index level
bigmac.loc[("2010-01-01")]  # all data inside "2010-01-01" outer-index name
bigmac.loc[("2010-01-01","China")]    # all data inside "2010-01-01" outer-index and inside "China" inner index name

# if we have more column we can be define after index tuple
bigmac.loc[("2010-01-01","China"), "Price in US Dollars"] # all data inside "2010-01-01" outer-index 
                                                            # and inside "China"  name, 
                                                            #  only for "Price in US Dollars" label


```


<font color="blue"> OUTPUT: </font>




    Date        Country
    2010-01-01  China      1.83
    Name: Price in US Dollars, dtype: float64



### .transpose() Method

আমরা যদি row এবং column এর axis পরিবর্তন করতে চাই বা data-frame টাকে vertical axis থেকে horizontal axis বানাইতে চাই তা হইলে <font color="green"> dataframe.transpose() </font> ব্যবহার করে তা করতে পারি। 

<font color="blue"> Example </font>


```python
import pandas as pd

bigmac = pd.read_csv("bigmac.csv", parse_dates = ["Date"], index_col = ["Date", "Country"])
bigmac.sort_index(inplace = True)
bigmac.head(3)

# replace rows to columns and columns to row
bigmac = bigmac.transpose()
bigmac.head(3)

#bigmac.loc["Price in US Dollars", ("2016-01-01", "Denmark")]  #filter data

```



<font color="blue"> OUTPUT: </font>




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>Date</th>
      <th colspan="10" halign="left">2010-01-01</th>
      <th>...</th>
      <th colspan="10" halign="left">2016-01-01</th>
    </tr>
    <tr>
      <th>Country</th>
      <th>Argentina</th>
      <th>Australia</th>
      <th>Brazil</th>
      <th>Britain</th>
      <th>Canada</th>
      <th>Chile</th>
      <th>China</th>
      <th>Colombia</th>
      <th>Costa Rica</th>
      <th>Czech Republic</th>
      <th>...</th>
      <th>Switzerland</th>
      <th>Taiwan</th>
      <th>Thailand</th>
      <th>Turkey</th>
      <th>UAE</th>
      <th>Ukraine</th>
      <th>United States</th>
      <th>Uruguay</th>
      <th>Venezuela</th>
      <th>Vietnam</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Price in US Dollars</th>
      <td>1.84</td>
      <td>3.98</td>
      <td>4.76</td>
      <td>3.67</td>
      <td>3.97</td>
      <td>3.18</td>
      <td>1.83</td>
      <td>3.91</td>
      <td>3.52</td>
      <td>3.71</td>
      <td>...</td>
      <td>6.44</td>
      <td>2.08</td>
      <td>3.09</td>
      <td>3.41</td>
      <td>3.54</td>
      <td>1.54</td>
      <td>4.93</td>
      <td>3.74</td>
      <td>0.66</td>
      <td>2.67</td>
    </tr>
  </tbody>
</table>
<p>1 rows × 652 columns</p>
</div>



### .swaplevel() Method

প্রয়োজনে multi Index এ inner label আর outer label column গুলো exchange করতে পারি। <font color="blue"> dataFrame.swaplevel() </font> ব্যবহার করে inner label কে outer label আর outer label কে inner label এ পরিণত করা যায়। 

<font color="blue"> Example </font>


```python
import pandas as pd

bigmac = pd.read_csv("bigmac.csv", parse_dates = ["Date"], index_col = ["Date", "Country"])
bigmac.sort_index(inplace = True)
bigmac.head(3)

# if your index have more than 2 level then need to swap by
bigmac = bigmac.swaplevel() # no inplace parameter, need to declar as bigmac = bigmac.swaplevel()
bigmac.head(3)

```



<font color="blue"> OUTPUT: </font>




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
      <th>Price in US Dollars</th>
    </tr>
    <tr>
      <th>Country</th>
      <th>Date</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Argentina</th>
      <th>2010-01-01</th>
      <td>1.84</td>
    </tr>
    <tr>
      <th>Australia</th>
      <th>2010-01-01</th>
      <td>3.98</td>
    </tr>
    <tr>
      <th>Brazil</th>
      <th>2010-01-01</th>
      <td>4.76</td>
    </tr>
  </tbody>
</table>
</div>



### .stack() Method

data-frame এর প্রতিটা index label value এর জন্য অন্য সব label ভালুএ এর মান কি তা দেখার জন্য <font color="green"> dataFrame.stack() </font> ব্যবহার করা হয়। 
আমরা একটি index value এর জন্য অন্য সব label value এর মান তারপর next index value এর জন্য অন্য সব label value এর মান এইভাবে পর্যায়ক্রমে data সাজিয়া data-frame বানানর জন্য .stack() method ব্যবহার করতে পারি। 


<font color="blue"> Example </font>


```python
import pandas as pd

world = pd.read_csv("worldstats.csv",index_col = ["country","year"])
world.head(3)

# display total value for a specific multiIndex by 
a = world.stack()
type(world.stack()) # its a series 

# we can convert series to dataFrame by .to_frame()
a.to_frame()


```



<font color="blue"> OUTPUT: </font>




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
      <th></th>
      <th>0</th>
    </tr>
    <tr>
      <th>country</th>
      <th>year</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Arab World</th>
      <th rowspan="2" valign="top">2015</th>
      <th>Population</th>
      <td>3.920223e+08</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>2.530102e+12</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2014</th>
      <th>Population</th>
      <td>3.842226e+08</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>2.873600e+12</td>
    </tr>
    <tr>
      <th>2013</th>
      <th>Population</th>
      <td>3.765043e+08</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">Zimbabwe</th>
      <th>1962</th>
      <th>GDP</th>
      <td>1.117602e+09</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">1961</th>
      <th>Population</th>
      <td>3.876638e+06</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>1.096647e+09</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">1960</th>
      <th>Population</th>
      <td>3.752390e+06</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>1.052990e+09</td>
    </tr>
  </tbody>
</table>
<p>22422 rows × 1 columns</p>
</div>



### .unstack() Method

আমরা যে কোন stack customize data কে unstack করে segmentation করার জন্য <font color="green"> dataFrame.unstack()</font>  ব্যবহার করা হয়।

<font color="blue"> Example </font>


```python
import pandas as pd

world = pd.read_csv("worldstats.csv",index_col = ["country","year"])
world.head(3)

# display total value for a specific multiIndex by 
a = world.stack()

# unstack besically reverse of stack method
a.unstack() # its unstack our created stack


b = a.unstack().unstack() # its change our multi layer's inner Index as column 


c = a.unstack().unstack().unstack()  # its make data frame to series





import pandas as pd

world = pd.read_csv("worldstats.csv",index_col = ["country","year"])
world.head(3)

a = world.stack()
a
a.unstack(2)  # unstack 3 number column (Population,GDP)
a.unstack(0)  # unstack 1 number column (country )
a.unstack(-1)  # unstack last number column 

a.unstack("country")  # unstack 1 number column (country )

# we can unstack column as new levels 
a.unstack(level = ["country", "year"])

s1 = a.unstack("year")

# we can fill NaN value with 0 or specific value by
s = a.unstack("year", fill_value = 0)

print(s)


```



<font color="blue"> OUTPUT: </font>




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
      <th>year</th>
      <th>1960</th>
      <th>1961</th>
      <th>1962</th>
      <th>1963</th>
      <th>1964</th>
      <th>1965</th>
      <th>1966</th>
      <th>1967</th>
      <th>1968</th>
      <th>1969</th>
      <th>...</th>
      <th>2006</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
    </tr>
    <tr>
      <th>country</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">Afghanistan</th>
      <th>Population</th>
      <td>8.994793e+06</td>
      <td>9.164945e+06</td>
      <td>9.343772e+06</td>
      <td>9.531555e+06</td>
      <td>9.728645e+06</td>
      <td>9.935358e+06</td>
      <td>1.014884e+07</td>
      <td>1.036860e+07</td>
      <td>1.059979e+07</td>
      <td>1.084951e+07</td>
      <td>...</td>
      <td>2.518362e+07</td>
      <td>2.587754e+07</td>
      <td>2.652874e+07</td>
      <td>2.720729e+07</td>
      <td>2.796221e+07</td>
      <td>2.880917e+07</td>
      <td>2.972680e+07</td>
      <td>3.068250e+07</td>
      <td>3.162751e+07</td>
      <td>3.252656e+07</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>5.377778e+08</td>
      <td>5.488889e+08</td>
      <td>5.466667e+08</td>
      <td>7.511112e+08</td>
      <td>8.000000e+08</td>
      <td>1.006667e+09</td>
      <td>1.400000e+09</td>
      <td>1.673333e+09</td>
      <td>1.373333e+09</td>
      <td>1.408889e+09</td>
      <td>...</td>
      <td>7.057598e+09</td>
      <td>9.843842e+09</td>
      <td>1.019053e+10</td>
      <td>1.248694e+10</td>
      <td>1.593680e+10</td>
      <td>1.793024e+10</td>
      <td>2.053654e+10</td>
      <td>2.004633e+10</td>
      <td>2.005019e+10</td>
      <td>1.919944e+10</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Albania</th>
      <th>Population</th>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>...</td>
      <td>2.992547e+06</td>
      <td>2.970017e+06</td>
      <td>2.947314e+06</td>
      <td>2.927519e+06</td>
      <td>2.913021e+06</td>
      <td>2.904780e+06</td>
      <td>2.900247e+06</td>
      <td>2.896652e+06</td>
      <td>2.893654e+06</td>
      <td>2.889167e+06</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>...</td>
      <td>8.992642e+09</td>
      <td>1.070101e+10</td>
      <td>1.288135e+10</td>
      <td>1.204421e+10</td>
      <td>1.192695e+10</td>
      <td>1.289087e+10</td>
      <td>1.231978e+10</td>
      <td>1.278103e+10</td>
      <td>1.327796e+10</td>
      <td>1.145560e+10</td>
    </tr>
    <tr>
      <th>Algeria</th>
      <th>Population</th>
      <td>1.112489e+07</td>
      <td>1.140486e+07</td>
      <td>1.169015e+07</td>
      <td>1.198513e+07</td>
      <td>1.229597e+07</td>
      <td>1.262695e+07</td>
      <td>1.298027e+07</td>
      <td>1.335420e+07</td>
      <td>1.374438e+07</td>
      <td>1.414444e+07</td>
      <td>...</td>
      <td>3.374933e+07</td>
      <td>3.426197e+07</td>
      <td>3.481106e+07</td>
      <td>3.540179e+07</td>
      <td>3.603616e+07</td>
      <td>3.671713e+07</td>
      <td>3.743943e+07</td>
      <td>3.818614e+07</td>
      <td>3.893433e+07</td>
      <td>3.966652e+07</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Yemen, Rep.</th>
      <th>GDP</th>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>...</td>
      <td>1.908173e+10</td>
      <td>2.563367e+10</td>
      <td>3.039720e+10</td>
      <td>2.845950e+10</td>
      <td>3.090675e+10</td>
      <td>3.107886e+10</td>
      <td>3.207477e+10</td>
      <td>3.595450e+10</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Zambia</th>
      <th>Population</th>
      <td>3.049586e+06</td>
      <td>3.142848e+06</td>
      <td>3.240664e+06</td>
      <td>3.342894e+06</td>
      <td>3.449266e+06</td>
      <td>3.559687e+06</td>
      <td>3.674088e+06</td>
      <td>3.792864e+06</td>
      <td>3.916928e+06</td>
      <td>4.047479e+06</td>
      <td>...</td>
      <td>1.238151e+07</td>
      <td>1.273868e+07</td>
      <td>1.311458e+07</td>
      <td>1.350785e+07</td>
      <td>1.391744e+07</td>
      <td>1.434353e+07</td>
      <td>1.478658e+07</td>
      <td>1.524609e+07</td>
      <td>1.572134e+07</td>
      <td>1.621177e+07</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>6.987397e+08</td>
      <td>6.823597e+08</td>
      <td>6.792797e+08</td>
      <td>7.043397e+08</td>
      <td>8.226397e+08</td>
      <td>1.061200e+09</td>
      <td>1.239000e+09</td>
      <td>1.340639e+09</td>
      <td>1.573739e+09</td>
      <td>1.926399e+09</td>
      <td>...</td>
      <td>1.275686e+10</td>
      <td>1.405696e+10</td>
      <td>1.791086e+10</td>
      <td>1.532834e+10</td>
      <td>2.026555e+10</td>
      <td>2.345952e+10</td>
      <td>2.550306e+10</td>
      <td>2.804552e+10</td>
      <td>2.713464e+10</td>
      <td>2.120156e+10</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Zimbabwe</th>
      <th>Population</th>
      <td>3.752390e+06</td>
      <td>3.876638e+06</td>
      <td>4.006262e+06</td>
      <td>4.140804e+06</td>
      <td>4.279561e+06</td>
      <td>4.422132e+06</td>
      <td>4.568320e+06</td>
      <td>4.718612e+06</td>
      <td>4.874113e+06</td>
      <td>5.036321e+06</td>
      <td>...</td>
      <td>1.312794e+07</td>
      <td>1.329780e+07</td>
      <td>1.349546e+07</td>
      <td>1.372100e+07</td>
      <td>1.397390e+07</td>
      <td>1.425559e+07</td>
      <td>1.456548e+07</td>
      <td>1.489809e+07</td>
      <td>1.524586e+07</td>
      <td>1.560275e+07</td>
    </tr>
    <tr>
      <th>GDP</th>
      <td>1.052990e+09</td>
      <td>1.096647e+09</td>
      <td>1.117602e+09</td>
      <td>1.159512e+09</td>
      <td>1.217138e+09</td>
      <td>1.311436e+09</td>
      <td>1.281750e+09</td>
      <td>1.397002e+09</td>
      <td>1.479600e+09</td>
      <td>1.747999e+09</td>
      <td>...</td>
      <td>5.443896e+09</td>
      <td>5.291950e+09</td>
      <td>4.415703e+09</td>
      <td>8.157077e+09</td>
      <td>9.422161e+09</td>
      <td>1.095623e+10</td>
      <td>1.239272e+10</td>
      <td>1.349023e+10</td>
      <td>1.419691e+10</td>
      <td>1.389294e+10</td>
    </tr>
  </tbody>
</table>
<p>504 rows × 56 columns</p>
</div>



### .pivot() Method

যদি কোন label এ same value repeatedly থাকে তা হইলে আমরা <font color="green"> dataFrame.pivot() </font> ব্যবহার করে repeated value গুলোেকে label এবং অন্য label এ ঐ value গুলো এর যে মান আছে তা value হিসেবে define করতে পারি। 

 <font color="green"> dataFrame.pivot(index, columns, values) </font> 
 * index এ আমরা যে label কে index বানাইতে চাই তা দিব। 
 * columns এ যে label এ repeated value আছে বা যে label এর মানগুলোকে new label বানাইতে চাই তা দিব। 
 * আর values এ আমরা new columns গুলো এর মান যে label থেকে হবে তা define করব।  

<font color="blue"> Example </font>


```python
import pandas as pd

sales = pd.read_csv("salesmen.csv",parse_dates = ["Date"])
sales["Salesman"] = sales["Salesman"].astype("category")
sales.head(3)

# we can specifi all levels data to needed catagory by .pivot()
sales.pivot(index = "Date", columns = "Salesman", values = "Revenue")

```



<font color="blue"> OUTPUT: </font>




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
      <th>Salesman</th>
      <th>Bob</th>
      <th>Dave</th>
      <th>Jeb</th>
      <th>Oscar</th>
      <th>Ronald</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2016-01-01</th>
      <td>7172</td>
      <td>1864</td>
      <td>4430</td>
      <td>5250</td>
      <td>2639</td>
    </tr>
    <tr>
      <th>2016-01-02</th>
      <td>6362</td>
      <td>8278</td>
      <td>8026</td>
      <td>8661</td>
      <td>4951</td>
    </tr>
    <tr>
      <th>2016-01-03</th>
      <td>5982</td>
      <td>4226</td>
      <td>5188</td>
      <td>7075</td>
      <td>2703</td>
    </tr>
    <tr>
      <th>2016-01-04</th>
      <td>7917</td>
      <td>3868</td>
      <td>3144</td>
      <td>2524</td>
      <td>4258</td>
    </tr>
    <tr>
      <th>2016-01-05</th>
      <td>7837</td>
      <td>2287</td>
      <td>938</td>
      <td>2793</td>
      <td>7771</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2016-12-27</th>
      <td>2045</td>
      <td>2843</td>
      <td>6666</td>
      <td>835</td>
      <td>2981</td>
    </tr>
    <tr>
      <th>2016-12-28</th>
      <td>100</td>
      <td>8888</td>
      <td>1243</td>
      <td>3073</td>
      <td>6129</td>
    </tr>
    <tr>
      <th>2016-12-29</th>
      <td>4115</td>
      <td>9490</td>
      <td>3498</td>
      <td>6424</td>
      <td>7662</td>
    </tr>
    <tr>
      <th>2016-12-30</th>
      <td>2577</td>
      <td>3594</td>
      <td>8858</td>
      <td>7088</td>
      <td>2570</td>
    </tr>
    <tr>
      <th>2016-12-31</th>
      <td>3845</td>
      <td>6830</td>
      <td>9717</td>
      <td>8408</td>
      <td>2619</td>
    </tr>
  </tbody>
</table>
<p>366 rows × 5 columns</p>
</div>



### .pivot_table() Method

.pivot_table() method টা অনেকটা .pivot() method এর মত। .pivot_table() method এ অতিরিক্ত parameter হিসেবে aggfunc আছে, যা একটা label এর সমস্ত data গুলোকে নিয়ে, Arithmetic Operators করে থাকে। 
values label এর aggfunc হয়ে থাকে। 

<font color="blue"> Example </font>


```python
import pandas as pd

foods = pd.read_csv("foods.csv")
foods.head(3)

# work like microsoft xl by .pivot_table
foods.pivot_table(values = "Spend", index = "Gender", aggfunc = "min")

# work with multiIndex
foods.pivot_table(values = "Spend", index = ["Gender","Item"], aggfunc = "max")

# for specific colums 
foods.pivot_table(values = "Spend", index = ["Gender","Item"],columns = "City", aggfunc = "sum")

```



<font color="blue"> OUTPUT: </font>




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
      <th>City</th>
      <th>New York</th>
      <th>Philadelphia</th>
      <th>Stamford</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th>Item</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="6" valign="top">Female</th>
      <th>Burger</th>
      <td>1239.04</td>
      <td>1639.24</td>
      <td>1216.02</td>
    </tr>
    <tr>
      <th>Burrito</th>
      <td>978.95</td>
      <td>1458.76</td>
      <td>1820.11</td>
    </tr>
    <tr>
      <th>Chalupa</th>
      <td>876.58</td>
      <td>1673.33</td>
      <td>1602.35</td>
    </tr>
    <tr>
      <th>Donut</th>
      <td>1446.78</td>
      <td>1639.26</td>
      <td>1656.96</td>
    </tr>
    <tr>
      <th>Ice Cream</th>
      <td>1521.62</td>
      <td>1479.22</td>
      <td>1032.03</td>
    </tr>
    <tr>
      <th>Sushi</th>
      <td>1480.29</td>
      <td>1742.88</td>
      <td>1459.91</td>
    </tr>
    <tr>
      <th rowspan="6" valign="top">Male</th>
      <th>Burger</th>
      <td>1294.09</td>
      <td>938.18</td>
      <td>1439.16</td>
    </tr>
    <tr>
      <th>Burrito</th>
      <td>1399.40</td>
      <td>1312.93</td>
      <td>1300.29</td>
    </tr>
    <tr>
      <th>Chalupa</th>
      <td>1227.77</td>
      <td>1114.23</td>
      <td>1150.26</td>
    </tr>
    <tr>
      <th>Donut</th>
      <td>1345.27</td>
      <td>1249.36</td>
      <td>1421.13</td>
    </tr>
    <tr>
      <th>Ice Cream</th>
      <td>1603.63</td>
      <td>2191.27</td>
      <td>1059.22</td>
    </tr>
    <tr>
      <th>Sushi</th>
      <td>1396.15</td>
      <td>1395.88</td>
      <td>1267.82</td>
    </tr>
  </tbody>
</table>
</div>



### pd.melt() Method

.melt() method অনেক টা .pivot() method এর মত আবার অনেক টা বিপরীত। আমরা অনেকগুলো label থেকে specific label বানানর জন্য .melt() method use করে থাকি।

<font color="green"> pandas.melt(dataframe, id_vars, var_name, value_name) </font>
* dataFrame এ আমরা dataFrame এর নাম define করব।
* id_vars এ label define করব, যে label আমাদের index এর মত হবে।
* var_name এ একটা নাম দিব যা একটা new label এর নাম হবে এবং var_name এর value গুলো অন্য সব label name compress হয়ে তৈরি হবে। 
* value_name এ একটা নাম দিব যা একটা new label এর নাম হবে এবং এর মান গুলো var_name এর মান হবে। 


<font color="blue"> Example </font>


```python
import pandas as pd

sales = pd.read_csv("quarters.csv")
sales  

pd.melt(sales, id_vars = "Salesman")

# give variable_name and value_name
pd.melt(sales, id_vars = "Salesman", var_name = "Quarter", value_name = "Revenue")

```




<font color="blue"> OUTPUT: </font>




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
      <th>Salesman</th>
      <th>Quarter</th>
      <th>Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Boris</td>
      <td>Q1</td>
      <td>602908</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bob</td>
      <td>Q1</td>
      <td>43790</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Tommy</td>
      <td>Q1</td>
      <td>392668</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Travis</td>
      <td>Q1</td>
      <td>834663</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Donald</td>
      <td>Q1</td>
      <td>580935</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Ted</td>
      <td>Q1</td>
      <td>656644</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Jeb</td>
      <td>Q1</td>
      <td>486141</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Stacy</td>
      <td>Q1</td>
      <td>479662</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Morgan</td>
      <td>Q1</td>
      <td>992673</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Boris</td>
      <td>Q2</td>
      <td>233879</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Bob</td>
      <td>Q2</td>
      <td>514863</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Tommy</td>
      <td>Q2</td>
      <td>113579</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Travis</td>
      <td>Q2</td>
      <td>266785</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Donald</td>
      <td>Q2</td>
      <td>411379</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Ted</td>
      <td>Q2</td>
      <td>70803</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Jeb</td>
      <td>Q2</td>
      <td>600753</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Stacy</td>
      <td>Q2</td>
      <td>742806</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Morgan</td>
      <td>Q2</td>
      <td>879183</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Boris</td>
      <td>Q3</td>
      <td>354479</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Bob</td>
      <td>Q3</td>
      <td>297151</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Tommy</td>
      <td>Q3</td>
      <td>430882</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Travis</td>
      <td>Q3</td>
      <td>749238</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Donald</td>
      <td>Q3</td>
      <td>110390</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Ted</td>
      <td>Q3</td>
      <td>375948</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Jeb</td>
      <td>Q3</td>
      <td>742716</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Stacy</td>
      <td>Q3</td>
      <td>770712</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Morgan</td>
      <td>Q3</td>
      <td>37945</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Boris</td>
      <td>Q4</td>
      <td>32704</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Bob</td>
      <td>Q4</td>
      <td>544493</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Tommy</td>
      <td>Q4</td>
      <td>247231</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Travis</td>
      <td>Q4</td>
      <td>570524</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Donald</td>
      <td>Q4</td>
      <td>651572</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Ted</td>
      <td>Q4</td>
      <td>321388</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Jeb</td>
      <td>Q4</td>
      <td>404995</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Stacy</td>
      <td>Q4</td>
      <td>2501</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Morgan</td>
      <td>Q4</td>
      <td>293710</td>
    </tr>
  </tbody>
</table>
</div>















