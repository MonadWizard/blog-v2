---
title: Django REST framework example
keywords: Django REST Bangla Tutorials, bangla Function Base View, Bangla REST, Blog Bangla, Monad wizard
last_updated: July 20, 2021
# tags: [getting_started]
summary: 'Django REST Framework function base view Topic with short note. '
sidebar: mydoc_sidebar
permalink: drf_fbv.html
folder: mydoc
---


আমি মনে করতেছি আপনারা django-rest-framework সম্পর্কে অনেকটা জানেন,
আমি just কিছু coding structure দেখাব, যেন প্রয়োজনে code এর structure নিয়ে কাজ করতে সুবিধা হয়।

কয়েকটা step এ Django-Rest-Framework ব্যবহার করে বেশ কিছু project তৈরি করব। একের পর এক function-base views, class-base views, Mixins, Generic Views, ViewSets, Nested Serializers, Pagination, Security, Validation, Token Auth ব্যবহার korbo.

## Function base views

সকল কাজ ২ টি step এ complete হয়ে থাকে ।

-   settings.py + urls.py (in project dir)

-   models.py + serializers.py + views.py + urls.py (in app directory)

এই post এ আমরা just coding demo দেখব। সব code এর পরিবর্তন app dir তে হয়েছে ।

<br>

একটি demo DataBase table :

### models.py

```python

from django.db import models

# Create your models here.
class Student(models.Model):
    id = models.IntegerField(primary_key=True)
    name = models.CharField(max_length=200)
    score = models.DecimalField(max_digits=5,decimal_places=2)

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

আমরা এই post এ function base view (api_view)decorator নিয়ে কাজ করেছি, যা ২ টা stage এ ঘটেছে।

-   1.create and view(non-primary key base operations)
-   2.delete, update and view(primary key base operations).

### views.py

```python

from django.shortcuts import render

from .models import Student
from .serializers import StudentSerializer

from rest_framework.response import Response
from rest_framework import status
from rest_framework.decorators import api_view


# Create your views here.
@api_view(['GET','POST'])
def student_list(request):
    if request.method =='GET':
        students = Student.objects.all()
        serializer=StudentSerializer(students,many=True)
        return Response(serializer.data)

    elif request.method == 'POST':
        serializer = StudentSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data,status=status.HTTP_201_CREATED)
        return Response(serializer.errors,status=status.HTTP_400_BAD_REQUEST)


@api_view(['GET','PUT','DELETE'])
def student_detail(request,pk):
    try:
        student = Student.objects.get(pk=pk)
    except Student.DoesNotExist:
        return Response(status=status.HTTP_404_NOT_FOUND)

    if request.method=='GET':
        serializer = StudentSerializer(student)
        return Response(serializer.data)

    elif request.method == 'PUT':
        serializer = StudentSerializer(student,data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors,status=status.HTTP_400_BAD_REQUEST)

    elif request.method == 'DELETE':
        student.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)

```

### urls.py

```python

from django.urls import path
from .import views

urlpatterns = [
    path('s/', views.student_list),
    path('s/<int:pk>', views.student_detail),
]

```
