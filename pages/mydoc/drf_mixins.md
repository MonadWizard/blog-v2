---
title: Django REST framework example
keywords: Django REST Bangla Tutorials, mixins REST Django bangla, Bangla Python, Blog Bangla, Monad wizard
last_updated: July 20, 2020
# tags: [getting_started]
summary: 'Django REST Framework mixins Topic with short note. '
sidebar: mydoc_sidebar
permalink: drf_mixins.html
folder: mydoc
---

basic intro workflow এই section এর 1st post এ দেওয়া হয়েছে ।

## Mixins CLass base views

mixin simplify our work and implement as dry(don't repeate yourself) principals. 😏

Mixins:

    ListModelMixin
    CreateModelMixin
    RetrieveModelMixin
    UpdateModelMixin
    DestroyModelMixin

Mixins provided us

| Action methods | mixin Classes      | Handler Methods |
| -------------- | ------------------ | --------------- |
| list()         | ListModelMixin     | get()           |
| create()       | CreateModelMixin   | post()          |
| retrieve()     | RetrieveModelMixin | get()           |
| update()       | UpdateModelMixin   | put()           |
| destroy()      | DestroyModelMixin  | delete()        |

যে রকম Acrion Method এর out-come প্রয়োজন সেই রকম mixins class কে parameter হিসেবে define করতে হবে এবং Handler Method কে call করলেই DRF বাকি সব execution নিজেই করে নিবে।

<br>

[github link](https://github.com/MonadWizard/Django_rest-framework_Views_DEMO/tree/0.3_mixins)

<br>

একটি demo DataBase table same as funcrion and classbase:

### models.py

```python

from django.db import models

# Create your models here.
class Student(models.Model):
    id = models.IntegerField(primary_key=True)
    name = models.CharField(max_length=20)
    score = models.DecimalField(max_digits=10,decimal_places=3)

    def __str__(self):
        return self.name

```

then serializer data-base table for querify and work in Views.py as DRF procedure

### serializers.py

```python

from rest_framework import serializers
from .models import Student

class StudentSerializer(serializers.ModelSerializer):
    class Meta:
        model=Student
        fields=['id', 'name','score']

```

আমরা এই post এ Mixins class base view ( generics,mixins) নিয়ে কাজ করেছি, যা ২ টা stage এ ঘটেছে।

-   1.create and view(non-primary key base operations)
-   2.delete, update and view(primary key base operations).

### views.py

```python

from django.shortcuts import render

from cbvApp.models import Student
from cbvApp.serializers import StudentSerializer

from rest_framework import generics,mixins


# just call and use handler method

# non-primery key based operations
class StudentList(mixins.ListModelMixin,mixins.CreateModelMixin,generics.GenericAPIView):
    queryset = Student.objects.all()
    serializer_class= StudentSerializer

    def get(self,request):
        return self.list(request)

    def post(self,request):
        return self.create(request)


# primery key based operations

class StudentDetail(mixins.RetrieveModelMixin,mixins.UpdateModelMixin,mixins.DestroyModelMixin,generics.GenericAPIView):
    queryset = Student.objects.all()
    serializer_class= StudentSerializer

    def get(self,request,pk):
        return self.retrieve(request,pk)

    def put(self,request,pk):
        return self.update(request,pk)

    def delete(self,request,pk):
        return self.destroy(request,pk)

```

### urls.py

same as class base views

```python

from django.urls import path
from .import views

urlpatterns = [
    path('s/',views.StudentList.as_view()),
    path('s/<int:pk>',views.StudentDetail.as_view()),

]

```
