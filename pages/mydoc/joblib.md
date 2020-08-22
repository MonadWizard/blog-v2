---
title: joblib
keywords: joblib  Bangla Tutorials, bangla serialization , Bangla Python, Blog Bangla, Monad wizard
last_updated: Aug 22, 2020
# tags: [getting_started]
summary: "Here I try to complete all Basic joblib Topic with short note. "
sidebar: mydoc_sidebar
permalink: joblib.html
folder: mydoc
---



scikit-learn এর specific ক্ষেত্রে large numpy array serialization এ Pickel এর থেকে joblib বেশি efficient. linear-regression এর train data joblib ব্যবহার করে একটা file এ save করে রাখা যায়। এবং প্রয়োজনে save file ব্যবহার করে previously train data থেকে test predection করা যায়। 

<mark> simple linear regression </mark>


```python
import pandas as pd
data= pd.read_csv('Salary_Data.csv')

## apply linear regression 
from sklearn import linear_model
model= linear_model.LinearRegression()

# fit data
model.fit(data[["YearsExperience"]],data["Salary"])

# predict data
model.predict([[60000]])
```



<font color="blue"> Output: </font> 



    array([5.67023531e+08])



## .dump()

joblib import করে বা joblib থেকে dump method import করে train model file এ save করে রাখা যায়।
dump function ব্যবহার করা হয় model কে extended file আকারে save করে রাখার জন্য। 

<font color="green"> joblib.dump(model, "fileName") </font> 

<mark> Save Trained Model Using joblib </mark>


```python
#import joblib
from joblib import dump

joblib.dump(model, 'model_joblib')

```




<font color="blue"> Output: </font> 






    ['model_joblib']



<mark> Save Trained Model Using joblib full code </mark>


```python
import pandas as pd
data= pd.read_csv('Salary_Data.csv')

## apply linear regression 
from sklearn import linear_model
model= linear_model.LinearRegression()

# fit data
model.fit(data[["YearsExperience"]],data["Salary"])

# predict data
print(model.predict([[60000]]))

# dump train data 
from joblib import dump
joblib.dump(model, 'model_joblib')


```




<font color="blue"> Output: </font> 





    [5.67023531e+08]


    ['model_joblib']



## .load() 

joblib import করে বা joblib থেকে load method import করে train model saved file ব্যবহার করে test purpose ব্যবহার করা যায়। load function ব্যবহার করা হয় saved model file কে আবার trained model আকারে একটা variable এ পাওয়ার জন্য ।

<font color="green"> joblib.load("fileName") </font> 

<mark> Load save model full code</mark>


```python
from joblib import load

loadModel = joblib.load('model_joblib')

from sklearn import linear_model
loadModel.predict([[60000]])
```




<font color="blue"> Output: </font> 




    array([5.67023531e+08])



## Full code 


```python
import pandas as pd
data= pd.read_csv('Salary_Data.csv')

## apply linear regression 
from sklearn import linear_model
model= linear_model.LinearRegression()

# fit data
model.fit(data[["YearsExperience"]],data["Salary"])

# predict data
print(model.predict([[60000]]))

# dump train data to save as model_joblib
from joblib import dump
joblib.dump(model, 'model_joblib')


# load train model file to predict
from joblib import load

loadModel = joblib.load('model_joblib')

from sklearn import linear_model
loadModel.predict([[60000]])
```




<font color="blue"> Output: </font> 





    [5.67023531e+08]



    array([5.67023531e+08])






