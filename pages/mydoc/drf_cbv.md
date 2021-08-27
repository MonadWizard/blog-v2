---
title: Django REST framework example
keywords: Django REST Bangla Tutorials, bangla Class Base View, Bangla REST, Blog Bangla, Monad wizard
last_updated: July 20, 2021
# tags: [getting_started]
summary: 'Django REST Framework class base view Topic with short note. '
sidebar: mydoc_sidebar
permalink: drf_cbv.html
folder: mydoc
---

basic intro workflow এই section এর 1st post এ দেওয়া হয়েছে ।

## CLass base views

APIView parameter ব্যবহার করে list=get(), create=post(), update=put(), delete() method ব্যবহার করে REST API তৈরি করা যায়।

<br>

[github link](https://github.com/MonadWizard/Django_rest-framework_Views_DEMO/tree/classBaseView)

<br>

একটি demo DataBase table :

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

আমরা এই post এ class base view ( APIView) নিয়ে কাজ করেছি, যা ২ টা stage এ ঘটেছে।

-   1.create and view(non-primary key base operations)
-   2.delete, update and view(primary key base operations).

### views.py

```python

from django.shortcuts import render

from cbvApp.models import Student
from cbvApp.serializers import StudentSerializer

from rest_framework.response import Response
from rest_framework import status
from rest_framework.views import APIView
from django.http import Http404



# Create your views here.
class StudentList(APIView):

    def get(self,request):
        students = Student.objects.all()
        serializer = StudentSerializer(students,many=True)
        return Response(serializer.data)

    def post(self,request):
        serializer = StudentSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data,status=status.HTTP_201_CREATED)
        return Response(serializer.errors,status=status.HTTP_400_BAD_REQUEST)

class StudentDetail(APIView):
    def get_object(self,pk):
        try:
            return Student.objects.get(pk=pk)
        except Student.DoesNotExist:
            raise Http404

    def get(self,request,pk):
        student = self.get_object(pk)
        serializer = StudentSerializer(student)
        return Response(serializer.data)

    def put(self,request,pk):
        student = self.get_object(pk)
        serializer = StudentSerializer(student,data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors,status=status.HTTP_400_BAD_REQUEST)

    def delete(self,request,pk):
        student = self.get_object(pk)
        student.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)


```

### urls.py

```python

from django.urls import path
from .import views

urlpatterns = [
    path('s/',views.StudentList.as_view()),
    path('s/<int:pk>',views.StudentDetail.as_view()),

]

```
