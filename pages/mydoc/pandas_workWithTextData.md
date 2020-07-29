---
title: Pandas Text Data
keywords: Pandas Bangla Tutorials, bangla Pandas, Bangla Python, Data Preprocessing Bangla, Monad wizard
last_updated: July 20, 2020
tags: [getting_started]
summary: "python bangla blog post এর দ্বারা Pandas Library এর TextData related method গুলো আলোচিত হয়েছে ।"
sidebar: mydoc_sidebar
permalink: pandas_workWithTextData.html
folder: mydoc
---

[প্রয়োজনীয় data-set যা এই post এ ব্যবহার করা হয়েছে DOWNLOAD ](https://github.com/dust-nk-org/pandasDataSet/archive/master.zip)

এবং [Official Doc](https://pandas.pydata.org/)

Text-Data নিয়ে কাজ করতে হইলে pandas এর str function ব্যবহার করতে হয়। কারণ pandas এর text-data related কাজ গুলো .str function এর sub-function গুলো করে থাকে । আমরা নিচে function গুলো এর example দেখব। 

# .str.lower(), .str.upper(), .str.title(), .str.len()

যদি data-frame এর সব data string type হয়, তবে আমরা .str function ব্যবহার করতে পারি। 


<font color="green"> .str.title() </font> ব্যবহার করে data-frame এর specific column  বা Row এর সকল data এর capitalize করা যায়। 
মানে সকল word এর প্রথম letter Capital হবে। বাকি letter গুলো smaller থাকবে।  

<font color="green"> .str.lower() </font> ব্যবহার করে data-frame এর specific column বা Row এর সকল data এর সব word গুলো lower case করা যায়। 
মানে সকল word এর সকল letter lower case হবে।

<font color="green"> .str.upper() </font> ব্যবহার করে data-frame এর specific column বা Row এর সকল word গুলো Upper case করা যায়। 
মানে সকল word এর সকল letter Upper case হবে।

<font color="green"> .str.len() </font> ব্যবহার করে data-frame এর specific column বা Row এর সকল data এর মধ্যে total কতগুলো character আছে তা count করা যায়। 
মানে সকল word এর total character এর পরিমাণ জানা যায় । 

<font color="green"> Example </font>


```python
import pandas as pd#
chicago = pd.read_csv("chicago.csv").dropna(how = "all")
# reduse memory size
chicago["Department"] = chicago["Department"].astype("category")
chicago["Position Title"] = chicago["Position Title"].astype("category")
chicago["Employee Annual Salary"] = chicago["Employee Annual Salary"].astype("category")

# info
chicago.info()


```


<font color="blue"> Output </font>



    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 32062 entries, 0 to 32061
    Data columns (total 4 columns):
     #   Column                  Non-Null Count  Dtype   
    ---  ------                  --------------  -----   
     0   Name                    32062 non-null  object  
     1   Position Title          32062 non-null  category
     2   Department              32062 non-null  category
     3   Employee Annual Salary  32062 non-null  category
    dtypes: category(3), object(1)
    memory usage: 756.6+ KB



```python

# Capitalize Name column's Data
chicago["Name"] = chicago["Name"].str.title()
chicago["Name"]
```


<font color="blue"> Output </font>




    0            Aaron,  Elvia J
    1          Aaron,  Jeffery M
    2             Aaron,  Karina
    3        Aaron,  Kimberlei R
    4        Abad Jr,  Vicente M
                    ...         
    32057    Zygadlo,  Michael J
    32058     Zygowicz,  Peter J
    32059      Zymantas,  Mark E
    32060    Zyrkowski,  Carlo E
    32061    Zyskowski,  Dariusz
    Name: Name, Length: 32062, dtype: object




```python
# lower all Department column's Data
chicago["Department"] = chicago["Department"].str.lower()
chicago["Department"]
```


<font color="blue"> Output </font>




    0             water mgmnt
    1                  police
    2                  police
    3        general services
    4             water mgmnt
                   ...       
    32057    general services
    32058              police
    32059              police
    32060              police
    32061                doit
    Name: Department, Length: 32062, dtype: object




```python
# Upper all Position Title column's Data
chicago["Position Title"] = chicago["Position Title"].str.upper()
chicago["Position Title"]
```


<font color="blue"> Output </font>




    0                      WATER RATE TAKER
    1                        POLICE OFFICER
    2                        POLICE OFFICER
    3              CHIEF CONTRACT EXPEDITER
    4                     CIVIL ENGINEER IV
                          ...              
    32057    FRM OF MACHINISTS - AUTOMOTIVE
    32058                    POLICE OFFICER
    32059                    POLICE OFFICER
    32060                    POLICE OFFICER
    32061           CHIEF DATA BASE ANALYST
    Name: Position Title, Length: 32062, dtype: object




```python
# count total character par row by 
chicago["Position Title"].str.len()


```

<font color="blue"> Output </font>




    0        16
    1        14
    2        14
    3        24
    4        17
             ..
    32057    30
    32058    14
    32059    14
    32060    14
    32061    23
    Name: Position Title, Length: 32062, dtype: int64




```python
#count total String
print(len(chicago["Position Title"]))


```

<font color="blue"> Output </font>


    32062


### .str.replace()

আমরা data-frame এর specific column এর যে কোন data কে change করতে পারি। আমরা <font color="green"> .str.replace("target","output")</font> এ target=যে value change করতে চাই এবং output=update value হিসেবে যে value চাই।
তা ব্যবহার করে আমরা Data-frame বা Series এর যে কোন data যত জায়গায় আছে সব জায়গা থেকে update করতে পারি define করার মাধ্যমে। 

<font color="green"> Example </font>


```python
import pandas as pd#
chicago = pd.read_csv("chicago.csv").dropna(how = "all")
# reduse memory size
chicago["Department"] = chicago["Department"].astype("category")
chicago["Position Title"] = chicago["Position Title"].astype("category")
chicago["Employee Annual Salary"] = chicago["Employee Annual Salary"].astype("category")

# # info
# chicago.info()

print("before : \n \n",chicago["Department"])  # before change

chicago["Department"] = chicago["Department"].str.replace("MGMNT","MANAGEMENT")  # replace("terget", "output")
chicago["Employee Annual Salary"] = chicago["Employee Annual Salary"].str.replace("$","").astype(float) # astype() for reduce memory
print("\n after : \n \n ",chicago["Department"])  # after change
```


<font color="blue"> Output </font>



    before : 
     
     0             WATER MGMNT
    1                  POLICE
    2                  POLICE
    3        GENERAL SERVICES
    4             WATER MGMNT
                   ...       
    32057    GENERAL SERVICES
    32058              POLICE
    32059              POLICE
    32060              POLICE
    32061                DoIT
    Name: Department, Length: 32062, dtype: category
    Categories (35, object): [ADMIN HEARNG, ANIMAL CONTRL, AVIATION, BOARD OF ELECTION, ..., STREETS & SAN, TRANSPORTN, TREASURER, WATER MGMNT]
    
     after : 
     
      0        WATER MANAGEMENT
    1                  POLICE
    2                  POLICE
    3        GENERAL SERVICES
    4        WATER MANAGEMENT
                   ...       
    32057    GENERAL SERVICES
    32058              POLICE
    32059              POLICE
    32060              POLICE
    32061                DoIT
    Name: Department, Length: 32062, dtype: object


### Filtering with String Method

Data-frame বা Series এর data গুলো আমরা specific data অনুসারে filter করতে পারি। 

filter এর জন্য সকল data কে upper বা lower case এ convert করার প্রয়োজন হইতে পারে। আমরা একটা script এ বেশকিছু condition apply করতে পারি। 

<font color="green"> .str.contains() </font> ব্যবহার করে যদি আমরা filter-data define করি তা হইলে initial data-frame বা series এর যে সব data এর মধ্যে filter-data থাকবে , আমরা শুধু ঐ সব data পাব। 

<font color="green"> .str.startswith() </font> ব্যবহার করে যদি আমরা filter-data define করি তা হইলে initial data-frame বা series এর যে সব data এর শুরুতে filter-data থাকবে , আমরা শুধু ঐ সব data পাব। 

<font color="green"> .str.endswith() </font> ব্যবহার করে যদি আমরা filter-data define করি তা হইলে initial data-frame বা series এর যে সব data এর শেষ এ filter-data থাকবে , আমরা শুধু ঐ সব data পাব। 

<font color="green"> Example </font>


```python
import pandas as pd
chicago = pd.read_csv("chicago.csv").dropna(how = "all")
# reduse memory size
chicago["Department"] = chicago["Department"].astype("category")
chicago["Position Title"] = chicago["Position Title"].astype("category")
chicago["Employee Annual Salary"] = chicago["Employee Annual Salary"].astype("category")


# if found water in any whhere in Position Title
mask = chicago["Position Title"].str.lower().str.contains("water")
print("found water in any whhere in Position Title \n \n \n", chicago[mask])

# if found water in first in  Position Title
print("\n \n if found water in first in  Position Title: \n \n \n" , chicago[chicago["Position Title"].str.lower().str.startswith("water")])

# if found ist in last in  Position Title
print("\n \n if found ist in last in  Position Title: \n \n \n" , chicago[chicago["Position Title"].str.lower().str.endswith("ist")])


```


<font color="blue"> Output </font>




    found water in any whhere in Position Title 
     
     
                            Name                                 Position Title  \
    0           AARON,  ELVIA J                               WATER RATE TAKER   
    554      ALUISE,  VINCENT G             FOREMAN OF WATER PIPE CONSTRUCTION   
    671         ANDER,  PERRY A                               WATER CHEMIST II   
    685     ANDERSON,  ANDREW J  DISTRICT SUPERINTENDENT OF WATER DISTRIBUTION   
    702       ANDERSON,  DONALD             FOREMAN OF WATER PIPE CONSTRUCTION   
    ...                     ...                                            ...   
    29669        VERMA,  ANUPAM           MANAGING ENGINEER - WATER MANAGEMENT   
    30239   WASHINGTON,  JOSEPH                              WATER CHEMIST III   
    30544       WEST,  THOMAS R                   GEN SUPT OF WATER MANAGEMENT   
    30991    WILLIAMS,  MATTHEW             FOREMAN OF WATER PIPE CONSTRUCTION   
    31405  WOODRIDGE,  ROBERT L             FOREMAN OF WATER PIPE CONSTRUCTION   
    
            Department Employee Annual Salary  
    0      WATER MGMNT              $90744.00  
    554    WATER MGMNT             $102440.00  
    671    WATER MGMNT              $82044.00  
    685    WATER MGMNT             $109272.00  
    702    WATER MGMNT             $102440.00  
    ...            ...                    ...  
    29669  WATER MGMNT             $111192.00  
    30239  WATER MGMNT              $89676.00  
    30544  WATER MGMNT             $115704.00  
    30991  WATER MGMNT             $102440.00  
    31405  WATER MGMNT             $102440.00  
    
    [111 rows x 4 columns]
    
     
     if found water in first in  Position Title: 
     
     
                              Name           Position Title   Department  \
    0             AARON,  ELVIA J         WATER RATE TAKER  WATER MGMNT   
    671           ANDER,  PERRY A         WATER CHEMIST II  WATER MGMNT   
    1054         ASHLEY,  KARMA T         WATER CHEMIST II  WATER MGMNT   
    1079        ATKINS,  JOANNA M         WATER CHEMIST II  WATER MGMNT   
    1181       AZEEM,  MOHAMMED A         WATER CHEMIST II  WATER MGMNT   
    ...                       ...                      ...          ...   
    28574      THREATT,  DENISE R  WATER QUALITY INSPECTOR  WATER MGMNT   
    28602       TIGNOR,  DARRYL B         WATER RATE TAKER  WATER MGMNT   
    28955  TRAVIS COOK,  LESLIE R         WATER RATE TAKER  WATER MGMNT   
    29584        VELAZQUEZ,  JOHN         WATER RATE TAKER  WATER MGMNT   
    30239     WASHINGTON,  JOSEPH        WATER CHEMIST III  WATER MGMNT   
    
          Employee Annual Salary  
    0                  $90744.00  
    671                $82044.00  
    1054               $82044.00  
    1079               $82044.00  
    1181               $53172.00  
    ...                      ...  
    28574              $62004.00  
    28602              $78948.00  
    28955              $78948.00  
    29584              $78948.00  
    30239              $89676.00  
    
    [75 rows x 4 columns]
    
     
     if found ist in last in  Position Title: 
     
     
                               Name                        Position Title  \
    184             AFROZ,  NAYYAR                          PSYCHIATRIST   
    308           ALARCON,  LUIS J            LOAN PROCESSING SPECIALIST   
    422           ALLAIN,  CAROLYN  SENIOR TELECOMMUNICATIONS SPECIALIST   
    472             ALLEN,  ROBERT                             MACHINIST   
    705        ANDERSON,  EDWARD M             SR PROCUREMENT SPECIALIST   
    ...                        ...                                   ...   
    31667         YODER,  TERESA G                   ARCHIVAL SPECIALIST   
    31688  YOUNGBLOOM,  LAURENCE G        CRIMES SURVEILLANCE SPECIALIST   
    31717       YOUNG,  KIMBERLY M             SR PROCUREMENT SPECIALIST   
    31837            ZAPATA,  HUGO             SR PROCUREMENT SPECIALIST   
    31918        ZEMKE,  RICHARD P                             MACHINIST   
    
                      Department Employee Annual Salary  
    184                   HEALTH              $99840.00  
    308    COMMUNITY DEVELOPMENT              $81948.00  
    422                     DoIT              $89880.00  
    472              WATER MGMNT              $94328.00  
    705              PROCUREMENT              $91476.00  
    ...                      ...                    ...  
    31667         PUBLIC LIBRARY              $74304.00  
    31688                   OEMC              $19676.80  
    31717            PROCUREMENT              $68556.00  
    31837            PROCUREMENT              $87324.00  
    31918               AVIATION              $94328.00  
    
    [172 rows x 4 columns]


### .strip(), .lstrip(), .rstrip() for remove freeSpace

data-set এর data গুলো তে অনেক সময় অপ্রয়োজনীয় space থেকে যায়। আমরা <font color="green"> .str.strip()</font> বা <font color="green"> .str.lstrip()</font> বা <font color="green"> .str.rstrip()</font> ব্যবহার করে space remove করতে পারি। 


<font color="green"> .str.rstrip()</font> দ্বারা right-side এর space remove করা যায়। 
<font color="green"> .str.lstrip()</font> দ্বারা left-side এর space remove করা যায়। 

<font color="green"> .str.strip()</font> দ্বারা left-side এবং right-side (উভয় পাশ) এর space একই সঙ্ঘে remove করা যায়। 




<font color="green"> Example </font>


```python
import pandas as pd
chicago = pd.read_csv("chicago.csv").dropna(how = "all")
# reduse memory size
chicago["Department"] = chicago["Department"].astype("category")
chicago["Position Title"] = chicago["Position Title"].astype("category")
chicago["Employee Annual Salary"] = chicago["Employee Annual Salary"].astype("category")

print(chicago.head())

# remove white space only from left and from right 
chicago["Name"] = chicago["Name"].str.rstrip().str.lstrip()

print("use rstrip() and lstrip : \n \n \n",chicago["Name"])

chicago["Position Title"] = chicago["Position Title"].str.strip()
print("\n \n \n use strip() : \n \n \n", chicago["Position Title"])


```


<font color="blue"> Output </font>



                      Name            Position Title        Department  \
    0      AARON,  ELVIA J          WATER RATE TAKER       WATER MGMNT   
    1    AARON,  JEFFERY M            POLICE OFFICER            POLICE   
    2       AARON,  KARINA            POLICE OFFICER            POLICE   
    3  AARON,  KIMBERLEI R  CHIEF CONTRACT EXPEDITER  GENERAL SERVICES   
    4  ABAD JR,  VICENTE M         CIVIL ENGINEER IV       WATER MGMNT   
    
      Employee Annual Salary  
    0              $90744.00  
    1              $84450.00  
    2              $84450.00  
    3              $89880.00  
    4             $106836.00  
    use rstrip() and lstrip : 
     
     
     0            AARON,  ELVIA J
    1          AARON,  JEFFERY M
    2             AARON,  KARINA
    3        AARON,  KIMBERLEI R
    4        ABAD JR,  VICENTE M
                    ...         
    32057    ZYGADLO,  MICHAEL J
    32058     ZYGOWICZ,  PETER J
    32059      ZYMANTAS,  MARK E
    32060    ZYRKOWSKI,  CARLO E
    32061    ZYSKOWSKI,  DARIUSZ
    Name: Name, Length: 32062, dtype: object
    
     
     
     use strip() : 
     
     
     0                      WATER RATE TAKER
    1                        POLICE OFFICER
    2                        POLICE OFFICER
    3              CHIEF CONTRACT EXPEDITER
    4                     CIVIL ENGINEER IV
                          ...              
    32057    FRM OF MACHINISTS - AUTOMOTIVE
    32058                    POLICE OFFICER
    32059                    POLICE OFFICER
    32060                    POLICE OFFICER
    32061           CHIEF DATA BASE ANALYST
    Name: Position Title, Length: 32062, dtype: object


### .str.split() method for Spliting Strings

.str.split() method data-frame এ কাজ করে, series এ single data থাকে তাই series এ কিছুই split করার নাই। 
কোন series এ split() ব্যবহার করলে error face করে।  

<font color="green"> Example </font>


```python
import pandas as pd
chicago = pd.read_csv("chicago.csv").dropna(how = "all")
# reduse memory size
chicago["Department"] = chicago["Department"].astype("category")
chicago["Position Title"] = chicago["Position Title"].astype("category")
chicago["Employee Annual Salary"] = chicago["Employee Annual Salary"].astype("category")
print(chicago.head(3))

firstName = chicago["Name"].str.split(",").str.get(0)
lastName = chicago["Name"].str.split(",").str.get(1)
print(lastName)

#position = chicago["Position Title"].srt.split(" ").str.get(0).value_counts()  # no separated multiple data as Series

# split and got single name 

```

<font color="blue"> Output </font>



                    Name    Position Title   Department Employee Annual Salary
    0    AARON,  ELVIA J  WATER RATE TAKER  WATER MGMNT              $90744.00
    1  AARON,  JEFFERY M    POLICE OFFICER       POLICE              $84450.00
    2     AARON,  KARINA    POLICE OFFICER       POLICE              $84450.00
    0              ELVIA J
    1            JEFFERY M
    2               KARINA
    3          KIMBERLEI R
    4            VICENTE M
                 ...      
    32057        MICHAEL J
    32058          PETER J
    32059           MARK E
    32060          CARLO E
    32061          DARIUSZ
    Name: Name, Length: 32062, dtype: object


### some Fun With .split() and .strip()


```python
import pandas as pd
chicago = pd.read_csv("chicago.csv").dropna(how = "all")
# reduse memory size
chicago["Department"] = chicago["Department"].astype("category")
chicago["Position Title"] = chicago["Position Title"].astype("category")
chicago["Employee Annual Salary"] = chicago["Employee Annual Salary"].astype("category")
print(chicago.head(3))


# try to understand or comment 
print("\n \n \n take first part of last Name \n \n \n", chicago["Name"].str.split(",").str.get(1).str.strip().str.split(" ").str.get(0))

# try to understand or comment 
print("\n \n count last Name's first part \n \n \n", chicago["Name"].str.split(",").str.get(1).str.strip().str.split(" ").str.get(0).value_counts().head(7))
```

<font color="blue"> Output </font>


                    Name    Position Title   Department Employee Annual Salary
    0    AARON,  ELVIA J  WATER RATE TAKER  WATER MGMNT              $90744.00
    1  AARON,  JEFFERY M    POLICE OFFICER       POLICE              $84450.00
    2     AARON,  KARINA    POLICE OFFICER       POLICE              $84450.00
    
     
     
     take first part of last Name 
     
     
     0            ELVIA
    1          JEFFERY
    2           KARINA
    3        KIMBERLEI
    4          VICENTE
               ...    
    32057      MICHAEL
    32058        PETER
    32059         MARK
    32060        CARLO
    32061      DARIUSZ
    Name: Name, Length: 32062, dtype: object
    
     
     count last Name's first part 
     
     
     MICHAEL    1153
    JOHN        899
    JAMES       676
    ROBERT      622
    JOSEPH      537
    DAVID       506
    THOMAS      490
    Name: Name, dtype: int64


### more parameter of .srt.split(expend = True)

expend paramenet এর মান defaultly False থাকে। expend=True এর দ্বারা আমরা data-frame এর split করা data গুলো দ্বারা new data-frame structure পাই। যার columns নামে define করা থাকে না। 

<font color="green"> Example </font>


```python
import pandas as pd
chicago = pd.read_csv("chicago.csv").dropna(how = "all")
# reduse memory size
chicago["Department"] = chicago["Department"].astype("category")
chicago["Position Title"] = chicago["Position Title"].astype("category")
chicago["Employee Annual Salary"] = chicago["Employee Annual Salary"].astype("category")


print(chicago["Name"].str.split(",", expand=True))

chicago[["First Name", "Last Name"]] = chicago["Name"].str.split(",", expand=True)
chicago.head()
```

<font color="blue"> Output </font>


                   0              1
    0          AARON        ELVIA J
    1          AARON      JEFFERY M
    2          AARON         KARINA
    3          AARON    KIMBERLEI R
    4        ABAD JR      VICENTE M
    ...          ...            ...
    32057    ZYGADLO      MICHAEL J
    32058   ZYGOWICZ        PETER J
    32059   ZYMANTAS         MARK E
    32060  ZYRKOWSKI        CARLO E
    32061  ZYSKOWSKI        DARIUSZ
    
    [32062 rows x 2 columns]





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
      <th>Name</th>
      <th>Position Title</th>
      <th>Department</th>
      <th>Employee Annual Salary</th>
      <th>First Name</th>
      <th>Last Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>AARON,  ELVIA J</td>
      <td>WATER RATE TAKER</td>
      <td>WATER MGMNT</td>
      <td>$90744.00</td>
      <td>AARON</td>
      <td>ELVIA J</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AARON,  JEFFERY M</td>
      <td>POLICE OFFICER</td>
      <td>POLICE</td>
      <td>$84450.00</td>
      <td>AARON</td>
      <td>JEFFERY M</td>
    </tr>
    <tr>
      <th>2</th>
      <td>AARON,  KARINA</td>
      <td>POLICE OFFICER</td>
      <td>POLICE</td>
      <td>$84450.00</td>
      <td>AARON</td>
      <td>KARINA</td>
    </tr>
    <tr>
      <th>3</th>
      <td>AARON,  KIMBERLEI R</td>
      <td>CHIEF CONTRACT EXPEDITER</td>
      <td>GENERAL SERVICES</td>
      <td>$89880.00</td>
      <td>AARON</td>
      <td>KIMBERLEI R</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABAD JR,  VICENTE M</td>
      <td>CIVIL ENGINEER IV</td>
      <td>WATER MGMNT</td>
      <td>$106836.00</td>
      <td>ABAD JR</td>
      <td>VICENTE M</td>
    </tr>
  </tbody>
</table>
</div>



### more parameter of .srt.split(expend = True, n)

n এর মান define করার মাধ্যমে আমরা n পরিমাণ columns তৈরি করা যায় । <font color="green"> .str.split(expend=True, n=3 </font> দ্বারা ৩টি column create হয়। যে সব data এর ৩টি value নাই সেই সব data এর empty row তে None থাকে।   














