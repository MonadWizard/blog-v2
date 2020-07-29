---
title: Pandas GroupBy
keywords: Pandas Bangla Tutorials, bangla Pandas, Bangla Python, Data Preprocessing Bangla, Monad wizard
last_updated: July 20, 2020
tags: [getting_started]
summary: "python bangla blog post এর দ্বারা Pandas Library এর GroupBy related method গুলো আলোচিত হয়েছে ।"
sidebar: mydoc_sidebar
permalink: pandas_GroupBy.html
folder: mydoc
---


[প্রয়োজনীয় data-set যা এই post এ ব্যবহার করা হয়েছে DOWNLOAD ](https://github.com/dust-nk-org/pandasDataSet/archive/master.zip)

এবং [Official Doc](https://pandas.pydata.org/)

Pandas এর groupby function টি পাইথনের একটি শক্তিশালী এবং বহুমুখী function. এটি আপনাকে আরও ভাল বিশ্লেষণের জন্য, গণনা সম্পাদনের জন্য, পৃথক গ্রুপে আপনার ডেটা বিভক্ত করতে দেয়।

common value গুলোকে আলাদা column এ পৃথক করতে বা data-set কে বেশকিছু segment এ ভাগ করতে groupby function অনেক কাজে লাগে। 

fortune নাম এর ১০০০ company এর information সহ একটা data-set থেকে fortune নাম এর একটা data-frame তৈরি করা হয়েছে। এখন ঐ data-frame থেকে sector column টাকে আলাদা একটা group বানানো হয়েছে।  

<font color="blue"> Example: </font>


```python
#please run one script line than another

import pandas as pd

fortune = pd.read_csv("fortune1000.csv", index_col = "Rank")
sectors = fortune.groupby("Sector")
fortune.head(3)

# data-frame and groupby's data type are not same
print("dataframe type: ", type(fortune), "\n\n\n")
print("groupby object type: ", type(sectors), "\n\n\n")

len(sectors)  # gropeBy create 21 unique group
print("total unique object : ",fortune["Sector"].nunique(), "\n\n\n")  # we see total unique object

# we can see our total unique object with there value by .size()
sectors.size() # there are 21 sector , we see

# we can also see our unique object with its value by .value_count() but value_count make sorted as
fortune["Sector"].value_counts()  # there are 21 sector , we see

```



<font color="blue"> Output: </font>



    dataframe type:  <class 'pandas.core.frame.DataFrame'> 
    
    
    
    groupby object type:  <class 'pandas.core.groupby.generic.DataFrameGroupBy'> 
    
    
    
    total unique object :  21 
    
    
    





    Financials                      139
    Energy                          122
    Technology                      102
    Retailing                        80
    Health Care                      75
    Business Services                51
    Industrials                      46
    Food, Beverages & Tobacco        43
    Materials                        43
    Wholesalers                      40
    Transportation                   36
    Chemicals                        30
    Household Products               28
    Engineering & Construction       26
    Media                            25
    Hotels, Resturants & Leisure     25
    Motor Vehicles & Parts           24
    Aerospace & Defense              20
    Telecommunications               15
    Apparel                          15
    Food and Drug Stores             15
    Name: Sector, dtype: int64



### Basic group object

data-set এর যে সব label এ repeated value থাকে সেই সব labels নিয়ে groupby object বানানো হয়। তাই একটা group value সম্পূর্ণ data-frame এ অনেক বার repeated থাকে। 

আমরা <font color="green"> groupbyDataFrame.first() </font> ব্যবহার করে প্রতিটি group value এর under এ যে row টি প্রথমে আছে তা pick করতে পারি।

আমরা <font color="green"> groupbyDataFrame.last() </font> ব্যবহার করে প্রতিটি group value এর under এ যে row টি শেষ এ আছে তা pick করতে পারি।

আমরা <font color="green"> groupbyDataFrame.groups </font> ব্যবহার করে একটি python dictionary পেয়ে থাকি, যার key=each_group_value আর value=index_position_which_are_in_this_group_value.

আমরা .groups ব্যবহার করে index_number নিতে পারি। যা dataFrame.loc[index_number] এ ব্যবহার করে ঐ index এর সব data পাইতে পারি। 

<font color="blue"> Example: </font>


```python
#please run one script line than another

import pandas as pd

fortune = pd.read_csv("fortune1000.csv", index_col = "Rank")
sectors = fortune.groupby("Sector")
print(fortune.head(3),"\n\n\n")

# from 1000 companies total 21 sector's each values 
print(fortune["Sector"].value_counts(), "\n\n\n")

# we can extract very first row on group by .first()
first=sectors.first()

# we can extract last row on group by .first()
sectors.last()

# we can represent every group as a python dictionary. each group object represent as key and values are index label as
sectors.groups

# now we see our first keys 1st value what represent by .loc[]
fortune.loc[24] # here sector which is group object, that match with 1st key

```


<font color="blue"> Output: </font>



              Company      Sector                     Industry         Location  \
    Rank                                                                          
    1         Walmart   Retailing        General Merchandisers  Bentonville, AR   
    2     Exxon Mobil      Energy           Petroleum Refining       Irving, TX   
    3           Apple  Technology  Computers, Office Equipment    Cupertino, CA   
    
          Revenue  Profits  Employees  
    Rank                               
    1      482130    14694    2300000  
    2      246204    16150      75600  
    3      233715    53394     110000   
    
    
    
    Financials                      139
    Energy                          122
    Technology                      102
    Retailing                        80
    Health Care                      75
    Business Services                51
    Industrials                      46
    Food, Beverages & Tobacco        43
    Materials                        43
    Wholesalers                      40
    Transportation                   36
    Chemicals                        30
    Household Products               28
    Engineering & Construction       26
    Media                            25
    Hotels, Resturants & Leisure     25
    Motor Vehicles & Parts           24
    Aerospace & Defense              20
    Telecommunications               15
    Apparel                          15
    Food and Drug Stores             15
    Name: Sector, dtype: int64 
    
    
    





    Company                     Boeing
    Sector         Aerospace & Defense
    Industry     Aerospace and Defense
    Location               Chicago, IL
    Revenue                      96114
    Profits                       5176
    Employees                   161400
    Name: 24, dtype: object



### .get_group() Method

<font color="green"> datafeame.get_group("target_value") </font> ব্যবহার করে আমরা DataFrame থেকে যে কোন value define করতে পারি এবং যে সব row তে ঐ value আছে শুধু সেই সব row বিশিষ্ট একটা নতুন dataFrame পেতে পারি। 



<font color="blue"> Example: </font>


```python
import pandas as pd

fortune = pd.read_csv("fortune1000.csv", index_col = "Rank")
sectors = fortune.groupby("Sector")
fortune.head(3)

# now try to create sub-set of all group values separetly by
fortune[fortune["Sector"] == "Apparel"]  # thats create one dataframe similar as .get_group()method

# or
# now we extract any group object's total value as a sub set by .get_group("groupObj")
energy = sectors.get_group("Energy")
# same as
tec = sectors.get_group("Technology")
tec.head(5)

```




<font color="blue"> Output: </font>




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
      <th>Company</th>
      <th>Sector</th>
      <th>Industry</th>
      <th>Location</th>
      <th>Revenue</th>
      <th>Profits</th>
      <th>Employees</th>
    </tr>
    <tr>
      <th>Rank</th>
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
      <th>3</th>
      <td>Apple</td>
      <td>Technology</td>
      <td>Computers, Office Equipment</td>
      <td>Cupertino, CA</td>
      <td>233715</td>
      <td>53394</td>
      <td>110000</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Amazon.com</td>
      <td>Technology</td>
      <td>Internet Services and Retailing</td>
      <td>Seattle, WA</td>
      <td>107006</td>
      <td>596</td>
      <td>230800</td>
    </tr>
    <tr>
      <th>20</th>
      <td>HP</td>
      <td>Technology</td>
      <td>Computers, Office Equipment</td>
      <td>Palo Alto, CA</td>
      <td>103355</td>
      <td>4554</td>
      <td>287000</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Microsoft</td>
      <td>Technology</td>
      <td>Computer Software</td>
      <td>Redmond, WA</td>
      <td>93580</td>
      <td>12193</td>
      <td>118000</td>
    </tr>
    <tr>
      <th>31</th>
      <td>IBM</td>
      <td>Technology</td>
      <td>Information Technology Services</td>
      <td>Armonk, NY</td>
      <td>82461</td>
      <td>13190</td>
      <td>411798</td>
    </tr>
  </tbody>
</table>
</div>



### Methods on GroupBy

groupby দ্বারা specific label আলাদা করে নিয়ে আমরা সকল groupby object থেকে বেশকিছু operation করতে পারি। যা আমাদের analysis কে অনেক efficient করে। 

আমরা আমাদের প্রতিটি group এর under এ যে valueটি maximum বা minimum কিংবা প্রতিটি group এর numerical value নিয়ে arithmatic operation করতে পারি। 

<font color="blue"> Example: </font>


```python
import pandas as pd

fortune = pd.read_csv("fortune1000.csv", index_col = "Rank")
sectors = fortune.groupby("Sector")
fortune.head(3)

# now if we use .max() its display last alphabetcaly or max value of each group object's very first columns defaultly
sectors.max()
# same for .min() method
sectors.min()

# but for numeric operation it's just take those columns which have numeric value as
sectors.sum()
sectors.mean()

# we can also work same for specific group object by
sectors.get_group("Apparel")["Revenue"].sum()

# we can also work same for specific colums  all value on group boject by
sectors["Revenue"].sum()
sectors["Employees"].sum()
sectors["Profits"].max()
sectors[["Employees", "Profits"]].sum()
```




<font color="blue"> Output: </font>




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
      <th>Employees</th>
      <th>Profits</th>
    </tr>
    <tr>
      <th>Sector</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aerospace &amp; Defense</th>
      <td>968057</td>
      <td>28742</td>
    </tr>
    <tr>
      <th>Apparel</th>
      <td>346397</td>
      <td>8236</td>
    </tr>
    <tr>
      <th>Business Services</th>
      <td>1361050</td>
      <td>28227</td>
    </tr>
    <tr>
      <th>Chemicals</th>
      <td>463651</td>
      <td>22628</td>
    </tr>
    <tr>
      <th>Energy</th>
      <td>1188927</td>
      <td>-73447</td>
    </tr>
    <tr>
      <th>Engineering &amp; Construction</th>
      <td>406708</td>
      <td>5304</td>
    </tr>
    <tr>
      <th>Financials</th>
      <td>3359948</td>
      <td>260209</td>
    </tr>
    <tr>
      <th>Food and Drug Stores</th>
      <td>1395398</td>
      <td>16759</td>
    </tr>
    <tr>
      <th>Food, Beverages &amp; Tobacco</th>
      <td>1211632</td>
      <td>51417</td>
    </tr>
    <tr>
      <th>Health Care</th>
      <td>2678289</td>
      <td>106114</td>
    </tr>
    <tr>
      <th>Hotels, Resturants &amp; Leisure</th>
      <td>2484245</td>
      <td>20697</td>
    </tr>
    <tr>
      <th>Household Products</th>
      <td>646038</td>
      <td>14428</td>
    </tr>
    <tr>
      <th>Industrials</th>
      <td>1545229</td>
      <td>20764</td>
    </tr>
    <tr>
      <th>Materials</th>
      <td>638123</td>
      <td>4428</td>
    </tr>
    <tr>
      <th>Media</th>
      <td>550314</td>
      <td>24347</td>
    </tr>
    <tr>
      <th>Motor Vehicles &amp; Parts</th>
      <td>1082560</td>
      <td>25898</td>
    </tr>
    <tr>
      <th>Retailing</th>
      <td>6227629</td>
      <td>47830</td>
    </tr>
    <tr>
      <th>Technology</th>
      <td>3578949</td>
      <td>180473</td>
    </tr>
    <tr>
      <th>Telecommunications</th>
      <td>832468</td>
      <td>48637</td>
    </tr>
    <tr>
      <th>Transportation</th>
      <td>1536793</td>
      <td>44169</td>
    </tr>
    <tr>
      <th>Wholesalers</th>
      <td>525597</td>
      <td>8233</td>
    </tr>
  </tbody>
</table>
</div>



### Grouping By Multiple Columns


আমরা groupby দ্বারা সাধারণত series তৈরি করে থাকি যা প্রদত্ত data-frame এর সঙ্ঘে বিভিন্ন operation করে থাকে। কিন্তু multi-columns এ groupby ব্যবহার করা মানে multi-index series তৈরি করা। আমরা multi-index নিয়ে আগের post এ জেনেছি । আমরা groupby এ list আকারে multiple index define করতে পারি। যা একটি multi-index series.

আমরা groupby এর যে কোন method ব্যবহার করলে তা প্রথমে outer index টার পর same way তে inner index এ execute হবে।  



<font color="blue"> Example: </font>




```python
import pandas as pd

fortune = pd.read_csv("fortune1000.csv", index_col = "Rank")
sectors = fortune.groupby(["Sector", "Industry"])
fortune.head(3)

# here we can see our created multi indexing
sectors.size()

# now try to work with multiIndex group object
sectors["Revenue"].sum()

```





<font color="blue"> Output: </font>



    Sector               Industry                                     
    Aerospace & Defense  Aerospace and Defense                            357940
    Apparel              Apparel                                           95968
    Business Services    Advertising, marketing                            22748
                         Diversified Outsourcing Services                  64829
                         Education                                          7485
                                                                           ...  
    Transportation       Trucking, Truck Leasing                           35950
    Wholesalers          Miscellaneous                                      8982
                         Wholesalers: Diversified                         176138
                         Wholesalers: Electronics and Office Equipment    147906
                         Wholesalers: Food and Grocery                    111774
    Name: Revenue, Length: 79, dtype: int64



### .agg() Method (Aggragation)

* .agg() method ব্যবহার করে আমরা অনেকগুলো label এ বিভিন্ন type এর operation  একই সঙ্ঘে করতে পারি। 

        groupBy_Object.agg({"labelName1" : ["operation1", "operation2"],
                                                  "labelName2" : "operation3",
                                                  "labelName3" : "operation4"})
                                          
* আবার সকল label এর জন্য বিভিন্ন operation এক সঙ্ঘে define করতে পারি। 

        groupBy_Object.agg(["operation1","operation2","operation3"])







<font color="blue"> Example: </font>


```python
import pandas as pd

fortune = pd.read_csv("fortune1000.csv", index_col = "Rank")
sectors = fortune.groupby("Sector")
fortune.head(3)

# now we can aggragation specific unique column by
sectors.agg({"Revenue" : ["sum","mean"],
             "Profits" : "sum",
             "Employees" : "mean"})

# or we can do same by
a = sectors.agg(["size","sum","mean"])
a
```




<font color="blue"> Output: </font>




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

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="3" halign="left">Revenue</th>
      <th colspan="3" halign="left">Profits</th>
      <th colspan="3" halign="left">Employees</th>
    </tr>
    <tr>
      <th></th>
      <th>size</th>
      <th>sum</th>
      <th>mean</th>
      <th>size</th>
      <th>sum</th>
      <th>mean</th>
      <th>size</th>
      <th>sum</th>
      <th>mean</th>
    </tr>
    <tr>
      <th>Sector</th>
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
      <th>Aerospace &amp; Defense</th>
      <td>20</td>
      <td>357940</td>
      <td>17897.000000</td>
      <td>20</td>
      <td>28742</td>
      <td>1437.100000</td>
      <td>20</td>
      <td>968057</td>
      <td>48402.850000</td>
    </tr>
    <tr>
      <th>Apparel</th>
      <td>15</td>
      <td>95968</td>
      <td>6397.866667</td>
      <td>15</td>
      <td>8236</td>
      <td>549.066667</td>
      <td>15</td>
      <td>346397</td>
      <td>23093.133333</td>
    </tr>
    <tr>
      <th>Business Services</th>
      <td>51</td>
      <td>272195</td>
      <td>5337.156863</td>
      <td>51</td>
      <td>28227</td>
      <td>553.470588</td>
      <td>51</td>
      <td>1361050</td>
      <td>26687.254902</td>
    </tr>
    <tr>
      <th>Chemicals</th>
      <td>30</td>
      <td>243897</td>
      <td>8129.900000</td>
      <td>30</td>
      <td>22628</td>
      <td>754.266667</td>
      <td>30</td>
      <td>463651</td>
      <td>15455.033333</td>
    </tr>
    <tr>
      <th>Energy</th>
      <td>122</td>
      <td>1517809</td>
      <td>12441.057377</td>
      <td>122</td>
      <td>-73447</td>
      <td>-602.024590</td>
      <td>122</td>
      <td>1188927</td>
      <td>9745.303279</td>
    </tr>
    <tr>
      <th>Engineering &amp; Construction</th>
      <td>26</td>
      <td>153983</td>
      <td>5922.423077</td>
      <td>26</td>
      <td>5304</td>
      <td>204.000000</td>
      <td>26</td>
      <td>406708</td>
      <td>15642.615385</td>
    </tr>
    <tr>
      <th>Financials</th>
      <td>139</td>
      <td>2217159</td>
      <td>15950.784173</td>
      <td>139</td>
      <td>260209</td>
      <td>1872.007194</td>
      <td>139</td>
      <td>3359948</td>
      <td>24172.287770</td>
    </tr>
    <tr>
      <th>Food and Drug Stores</th>
      <td>15</td>
      <td>483769</td>
      <td>32251.266667</td>
      <td>15</td>
      <td>16759</td>
      <td>1117.266667</td>
      <td>15</td>
      <td>1395398</td>
      <td>93026.533333</td>
    </tr>
    <tr>
      <th>Food, Beverages &amp; Tobacco</th>
      <td>43</td>
      <td>555967</td>
      <td>12929.465116</td>
      <td>43</td>
      <td>51417</td>
      <td>1195.744186</td>
      <td>43</td>
      <td>1211632</td>
      <td>28177.488372</td>
    </tr>
    <tr>
      <th>Health Care</th>
      <td>75</td>
      <td>1614707</td>
      <td>21529.426667</td>
      <td>75</td>
      <td>106114</td>
      <td>1414.853333</td>
      <td>75</td>
      <td>2678289</td>
      <td>35710.520000</td>
    </tr>
    <tr>
      <th>Hotels, Resturants &amp; Leisure</th>
      <td>25</td>
      <td>169546</td>
      <td>6781.840000</td>
      <td>25</td>
      <td>20697</td>
      <td>827.880000</td>
      <td>25</td>
      <td>2484245</td>
      <td>99369.800000</td>
    </tr>
    <tr>
      <th>Household Products</th>
      <td>28</td>
      <td>234737</td>
      <td>8383.464286</td>
      <td>28</td>
      <td>14428</td>
      <td>515.285714</td>
      <td>28</td>
      <td>646038</td>
      <td>23072.785714</td>
    </tr>
    <tr>
      <th>Industrials</th>
      <td>46</td>
      <td>497581</td>
      <td>10816.978261</td>
      <td>46</td>
      <td>20764</td>
      <td>451.391304</td>
      <td>46</td>
      <td>1545229</td>
      <td>33591.934783</td>
    </tr>
    <tr>
      <th>Materials</th>
      <td>43</td>
      <td>259145</td>
      <td>6026.627907</td>
      <td>43</td>
      <td>4428</td>
      <td>102.976744</td>
      <td>43</td>
      <td>638123</td>
      <td>14840.069767</td>
    </tr>
    <tr>
      <th>Media</th>
      <td>25</td>
      <td>220764</td>
      <td>8830.560000</td>
      <td>25</td>
      <td>24347</td>
      <td>973.880000</td>
      <td>25</td>
      <td>550314</td>
      <td>22012.560000</td>
    </tr>
    <tr>
      <th>Motor Vehicles &amp; Parts</th>
      <td>24</td>
      <td>482540</td>
      <td>20105.833333</td>
      <td>24</td>
      <td>25898</td>
      <td>1079.083333</td>
      <td>24</td>
      <td>1082560</td>
      <td>45106.666667</td>
    </tr>
    <tr>
      <th>Retailing</th>
      <td>80</td>
      <td>1465076</td>
      <td>18313.450000</td>
      <td>80</td>
      <td>47830</td>
      <td>597.875000</td>
      <td>80</td>
      <td>6227629</td>
      <td>77845.362500</td>
    </tr>
    <tr>
      <th>Technology</th>
      <td>102</td>
      <td>1377600</td>
      <td>13505.882353</td>
      <td>102</td>
      <td>180473</td>
      <td>1769.343137</td>
      <td>102</td>
      <td>3578949</td>
      <td>35087.735294</td>
    </tr>
    <tr>
      <th>Telecommunications</th>
      <td>15</td>
      <td>461834</td>
      <td>30788.933333</td>
      <td>15</td>
      <td>48637</td>
      <td>3242.466667</td>
      <td>15</td>
      <td>832468</td>
      <td>55497.866667</td>
    </tr>
    <tr>
      <th>Transportation</th>
      <td>36</td>
      <td>408508</td>
      <td>11347.444444</td>
      <td>36</td>
      <td>44169</td>
      <td>1226.916667</td>
      <td>36</td>
      <td>1536793</td>
      <td>42688.694444</td>
    </tr>
    <tr>
      <th>Wholesalers</th>
      <td>40</td>
      <td>444800</td>
      <td>11120.000000</td>
      <td>40</td>
      <td>8233</td>
      <td>205.825000</td>
      <td>40</td>
      <td>525597</td>
      <td>13139.925000</td>
    </tr>
  </tbody>
</table>
</div>



### Iterating through Groups

আমাদের data-set এ যে ১০০০ company এর data আছে টার মধ্যে প্রতিটি sector এ highest revenue যে company এর তা বাহির করার try করে দেখি। 


<font color="blue"> Example: </font>


```python
import pandas as pd

fortune = pd.read_csv("fortune1000.csv", index_col = "Rank")
sectors = fortune.groupby("Sector")
fortune.head(3)


# we can extract every value from a group object with specific operation by

df = pd.DataFrame(columns = fortune.columns) # seen empty value with all columns

for sector, data in sectors:
    highest_revenue_company_in_group = data.nlargest(1, "Revenue")
    df = df.append(highest_revenue_company_in_group)



# or we can do same by
cities = fortune.groupby("Location")
df2 = pd.DataFrame(columns = fortune.columns)
df2  # seen empty value with all columns

for city, data in cities:
    highest_revenue_in_city = data.nlargest(1, "Revenue")
    df2 = df2.append(highest_revenue_in_city)   

df2
```



<font color="blue"> Output: </font>



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
      <th>Company</th>
      <th>Sector</th>
      <th>Industry</th>
      <th>Location</th>
      <th>Revenue</th>
      <th>Profits</th>
      <th>Employees</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>138</th>
      <td>Abbott Laboratories</td>
      <td>Health Care</td>
      <td>Medical Products and Equipment</td>
      <td>Abbott Park, IL</td>
      <td>20661</td>
      <td>4423</td>
      <td>74000</td>
    </tr>
    <tr>
      <th>169</th>
      <td>Goodyear Tire &amp; Rubber</td>
      <td>Motor Vehicles &amp; Parts</td>
      <td>Motor Vehicles and Parts</td>
      <td>Akron, OH</td>
      <td>16443</td>
      <td>307</td>
      <td>66000</td>
    </tr>
    <tr>
      <th>288</th>
      <td>Air Products &amp; Chemicals</td>
      <td>Chemicals</td>
      <td>Chemicals</td>
      <td>Allentown, PA</td>
      <td>9895</td>
      <td>1278</td>
      <td>19550</td>
    </tr>
    <tr>
      <th>830</th>
      <td>Benchmark Electronics</td>
      <td>Technology</td>
      <td>Semiconductors and Other Electronic Components</td>
      <td>Angleton, TX</td>
      <td>2541</td>
      <td>95</td>
      <td>10500</td>
    </tr>
    <tr>
      <th>374</th>
      <td>Casey’s General Stores</td>
      <td>Retailing</td>
      <td>Specialty Retailers: Other</td>
      <td>Ankeny, IA</td>
      <td>7052</td>
      <td>181</td>
      <td>22408</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>CVS Health</td>
      <td>Food and Drug Stores</td>
      <td>Food and Drug Stores</td>
      <td>Woonsocket, RI</td>
      <td>153290</td>
      <td>5237</td>
      <td>199000</td>
    </tr>
    <tr>
      <th>506</th>
      <td>Hanover Insurance Group</td>
      <td>Financials</td>
      <td>Insurance: Property and Casualty (Stock)</td>
      <td>Worcester, MA</td>
      <td>5034</td>
      <td>332</td>
      <td>4800</td>
    </tr>
    <tr>
      <th>764</th>
      <td>Penn National Gaming</td>
      <td>Hotels, Resturants &amp; Leisure</td>
      <td>Hotels, Casinos, Resorts</td>
      <td>Wyomissing, PA</td>
      <td>2838</td>
      <td>1</td>
      <td>18204</td>
    </tr>
    <tr>
      <th>773</th>
      <td>Bon-Ton Stores</td>
      <td>Retailing</td>
      <td>General Merchandisers</td>
      <td>York, PA</td>
      <td>2790</td>
      <td>-57</td>
      <td>24100</td>
    </tr>
    <tr>
      <th>932</th>
      <td>Herman Miller</td>
      <td>Household Products</td>
      <td>Home Equipment, Furnishings</td>
      <td>Zeeland, MI</td>
      <td>2142</td>
      <td>98</td>
      <td>7510</td>
    </tr>
  </tbody>
</table>
<p>416 rows × 7 columns</p>
</div>






