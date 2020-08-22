---
title: pickel
keywords: pickel  Bangla Tutorials, checksum bangla, serialization bangla, pickel , Bangla pickel, Blog Bangla, Monad wizard
last_updated: July 20, 2020
# tags: [getting_started]
summary: "Here I try to complete all Basic pickel Topic with short note. "
sidebar: mydoc_sidebar
permalink: pickel.html
folder: mydoc
---




meshine learning এ অনেক সময় data-set কে train করে তারপরে test করা সময় সাপেক্ষ ব্যাপার হয়ে দ্বারায়, বা অনেক সময় পূর্ববর্তী train data ব্যবহার করে নতুন execution এ test data পাওয়ার দরকার হয়। 

মানে আমি বোঝাই তে চাইছি , যদি pre-trained data ব্যবহার করে আমরা test output পাইতে চাই তা হইলে আমাদের পূর্বেই data train করে রাখতে হবে। 
কিন্তু  আমরা জানি computer এ code মূলত RAM এর memory তে run হয় , তাই train data তো RAM এর memory তেই থাকে, যা code terminate হওয়ার সঙ্ঘে সঙ্ঘে remove হয়ে যায়। 

এখন যদি time complexity কমানোর জন্য pre-trained dataকে পরবর্তীতে code execution এর দ্বারা test result পাইতে ব্যবহার করতে হয় তবে , trained data কে local memory তে store করে রাখতে হবে। python এর অনেক library এই কাজ করে থাকে। sklearn.externals এর joblib বা pickle দ্বারা এই ধরনের কাজ করা যায়। 
এই পোস্ট এ আমরা pickle নিয়ে আলোচনা করব ।

Pickle পাইথন অবজেক্ট স্ট্রাকচারকে serializing  এবং de-serializing করার জন্য ব্যবহৃত হয়, যাকে marshaling  বা flattening বলাও হয়। সিরিয়ালাইজেশন বলতে কোনও জিনিসকে মেমরিতে কোনও বাইট স্ট্রিমে রূপান্তর করার প্রক্রিয়া বোঝায় যা disk এ সঞ্চয় করা যায় বা একটি নেটওয়ার্কের মাধ্যমে প্রেরণ করা যায়। পরে এই অক্ষর stream টি পুনরুদ্ধার করা যায় এবং পাইথন অবজেক্টে ডি-সিরিয়ালাইজ করা যায়। Pickling এবং compression এর মধ্যে বিভ্রান্ত হওয়ার দরকার নেই! Pickling হল একটি উপস্থাপনা (RAM data) থেকে অন্যটিতে (text on disk) রূপান্তর করা। এই পরবর্তীটি ডিস্কের স্থান বাঁচানোর জন্য কম বিট সহ ডেটা encoding প্রক্রিয়া সম্পাদন করে।

 আপনি যদি বিভিন্ন প্রোগ্রামিং ল্যাঙ্গুয়েজে ডেটা ব্যবহার করতে চান তবে Pickle, recommended নয়। এমন কি python এর বিভিন্ন version এ pickling করা data অন্য বিভিন্ন version এ সঠিকভাবে Unpickling করতে পারে না। 

আবার python এর lambda function এ pickle কাজ করে না। যদি lambda function এ pickling খুব দরকার হয় তবে আমাদের এর একটা library <font color="green"> dill </font> use করতে হবে। এই problem নিয়ে আমরা নিম্নে আলোচনা করবো । 

c programming language এ  <font color="green"> cPickle </font> use করা হয়। যা python এর <font color="green"> pickle </font> এর একই type এর data ব্যবহার করে। 

আমরা  pre-trained data pickling করবো তারপর শুধু store করা pickle data ব্যবহার করে predict করে দেখব।কথা না বাড়িয়া চল implementation part এ যাই। 

নিচে কত বৎসর অভিজ্ঞতা এর কর্মী এর বেতন কত হওয়া উচিৎ তা একটা simple linear Regression এ data-set ব্যবহার করে predict করা হয়েছে। এই code এর train-data pickling এর দ্বারা file এ store করে  store-data unpickling করে predict করে দেখব।

 <font color="blue"> DATA SET: </font> 

![image](https://drive.google.com/uc?export=view&id=1r0m0v0fuLbATzR1P9JfOLtp3BtxMnVbU)

```python
import pandas as pd
data= pd.read_csv('Salary_Data.csv')

##  apply linear regression 

from sklearn import linear_model
model= linear_model.LinearRegression()

# fit data
model.fit(data[["YearsExperience"]],data["Salary"])

# predict data
model.predict([[60000]])
```
<font color="blue"> OUTPUT: 5.67023531e+08</font>



এইবার code টির train-data কে python এর pickle library ব্যবহার করে file এ store করবো।

প্রথমে আমাদের pickle লাইব্রেরি import করতে হবে।

```python

import pickle

```

এরপর একটা binarry file তৈরি করতে হবে। আমরা train data কে serializing করে binary file এ store করে রাখতেছি । <font color="green">wb</font> দ্বারা  <font color="gray">write binary</font> premission দাওয়া হয়। 

```python

with open("model_pickle", "wb") as f:
    pickle.dump(model,f)

```

এখন binary file টিকে read করে de-serializing করতে হবে, যার ফলে আমরা binary file এ save করে রাখা data use করে prediction করতে পারি।
<font color="green">rb</font> দ্বারা  <font color="gray">read binary</font> premission দাওয়া হয়। 

```python

with open("model_pickle", "rb") as f:
    mp=pickle.load(f)

```

আমাদের pickle complete হয়েছে। এখন আমরা data-set preprocess বা train না করেই predict করে দেখতে পারি। 

```python

mp.predict([[60000]])

```

<font color="green"> OUTPUT: 5.67023531e+08</font>


### সম্পূর্ণ pickle তৈরী code STEP 1 : 

```python

import pandas as pd
data= pd.read_csv('Salary_Data.csv')

# apply linear regression
from sklearn import linear_model
model= linear_model.LinearRegression()

# fit data
model.fit(data[["YearsExperience"]],data["Salary"])

# predict data
model.predict([[60000]])

#.....................................................

# use pickle 
import pickle

# creating binary file
with open("model_pickle", "wb") as f:
    pickle.dump(model,f)


```


### সম্পূর্ণ pickle execute করে prediction code STEP 2 : 



```python

import pickle
# reading binary file
with open("model_pickle", "rb") as f:
    mp=pickle.load(f)
    
# predict 
print(mp.predict([[60000]]))

```




### সম্পূর্ণ pickle এবং unpickle codeটি এই : 

```python

# import data set
import pandas as pd
data= pd.read_csv('Salary_Data.csv')

# apply linear regression
from sklearn import linear_model
model= linear_model.LinearRegression()

# fit data
model.fit(data[["YearsExperience"]],data["Salary"])

# predict data
model.predict([[60000]])

#................................................

# use pickle 
import pickle

# creating binary file
with open("model_pickle", "wb") as f:
    pickle.dump(model,f)


# reading binary file
with open("model_pickle", "rb") as f:
    mp=pickle.load(f)
    
# predict 
mp.predict([[60000]])




```










