---
title: Django REST framework example
keywords: Django REST Bangla Tutorials, viewsets REST Django bangla, Bangla Python, Blog Bangla, Monad wizard
last_updated: July 20, 2020
# tags: [getting_started]
summary: 'Django REST Framework viewsets Topic with short note. '
sidebar: mydoc_sidebar
permalink: drf_viewsets.html
folder: mydoc
---

basic intro workflow এই section এর 1st post এ দেওয়া হয়েছে ।

## viewsets CLass base views

viewsets makes more easyer code structures then all class base view for principals. 😏

একই নাম এর একাধিক class এ mixins বা generic_view ব্যবহার করা যায় না। তাই DRF এ `viewSets` ব্যবহার করা হয়।

viewsets ব্যবহার করে same class এ multiple class base views operation করা যায়।

## viewsets

views.py configure as:

    viewsets --------> ViewSet
        |                   |-----------Router
        |------------>ModelViewSet
        |
        |------------>ReadOnlyModelViewSet

-   viewsets.ViewSet call করলে list(), create(), retrieve(), update(), delete() এই সব function customly নিজে নিজে করতে হয়।
-   অথবা viewsets.ModelViewSet call করলে automatic list(), create(), retrieve(), update(), delete() এই সব function execute করা যায়।
-   viewsets.ReadOnlyModelViewSet ব্যবহার করে non-id or id base operation এর list() function execute করা যায়।

<br>

-   url configuration টা একটু আলাদা। router define করতে হয়।

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

আমরা এই post এ viewsets class base view ( viewsets.ModelViewSet ) নিয়ে কাজ করেছি, যা ১ টা stage এ ঘটেছে।

-   class parameter এ viewsets.ModelViewSet define করলেই automatic সব operation করা যায়।
-   class parameter এ viewsets.ReadOnlyModelViewSet define করলে only get বা list() operation করা যায়।

### views.py

```python

from cbvApp.models import Student
from cbvApp.serializers import StudentSerializer

from rest_framework import viewsets

# just call and use handler method
class StudentViewSet(viewsets.ModelViewSet):
    queryset = Student.objects.all()
    serializer_class = StudentSerializer


class StudentReadOnlyViewSet(viewsets.ReadOnlyModelViewSet):
    queryset = Student.objects.all()
    serializer_class = StudentSerializer

```

### urls.py

urls.py এর configuration different:

-   1st need to create a router. (drf provides `DefaultRouter`)
-   2nd register viewsets. (`'url',views.YourViewClass`)
-   3rd diclar url inside urlpatterns which you expect. (`include(router.urls)`)

```python

from django.urls import path,include
from .import views
from rest_framework.routers import DefaultRouter

router = DefaultRouter()
router.register('std',views.StudentViewSet)
router.register('rostd',views.StudentReadOnlyViewSet)

urlpatterns = [
    path('', include(router.urls)),

]

```
