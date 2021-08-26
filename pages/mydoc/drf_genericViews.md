---
title: Django REST framework example
keywords: Django REST Bangla Tutorials, generic Views REST Django bangla, Bangla Python, Blog Bangla, Monad wizard
last_updated: July 20, 2020
# tags: [getting_started]
summary: 'Django REST Framework generic Views Topic with short note. '
sidebar: mydoc_sidebar
permalink: drf_genericViews.html
folder: mydoc
---

basic intro workflow এই section এর 1st post এ দেওয়া হয়েছে ।

generic makes more easyer code structures for principals. 😏

## Generics

`handler methods:`

    CreateAPIView
    ListAPIView
    RetreiveAPIView
    DestroyAPIView
    UpdateAPIView

    ListCreateAPIView __(all non-id based operations)

    RetreiveUpdateAPIView
    RetreiveDestroyAPIView
    RetreiveUpdateDestroyAPIView __(all id based operations)

যে রকম Acrion Method এর out-come প্রয়োজন সেই রকম mixin class কে parameter হিসেবে define করলেই DRF বাকি সব execution নিজেই করে নিবে।

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

আমরা এই post এ generics class base view ( generics) নিয়ে কাজ করেছি, যা ২ টা stage এ ঘটেছে।

-   1.create and view(non-primary key base operations)
-   2.delete, update and view(primary key base operations).

### views.py

```python

from cbvApp.models import Student
from cbvApp.serializers import StudentSerializer

from rest_framework import generics


# just call and use handler method

# non-primery key based operations
class StudentList(generics.ListCreateAPIView):
    queryset = Student.objects.all()
    serializer_class= StudentSerializer


# primery key based operations
class StudentDetail(generics.RetrieveUpdateDestroyAPIView):
    queryset = Student.objects.all()
    serializer_class= StudentSerializer

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
