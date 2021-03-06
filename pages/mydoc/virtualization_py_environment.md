---
title: python virtual environment
keywords: pickel  Bangla Tutorials, virtualization bangla, virtual environment bangla, venv , Bangla env, Blog Bangla, Monad wizard
last_updated: July 20, 2020
# tags: [getting_started]
summary: "Here I try to complete all Basic Virtual Environment Topic with short note. "
sidebar: mydoc_sidebar
permalink: virtualization_py_environment.html
folder: mydoc
---


<h1 style='color:pink'> linux user দের  জন্য  </h1> 

## create python3 virtual environment

project directory তে python এর virtual environment তৈরি করে সেই virtual environment এ python library install দিয়ে প্রয়োজনীয় project complete করা যায়।


1st python3-venv install দিতে হবে , যেন venv ব্যবহার করে যেকোনো directory তে যে কোন নাম এর ভার্চুয়াল environment তৈরি করা যায়। open terminal & type 


```

    # setup py3 env

    sudo apt install -y python3-venv

```

2nd যে directory তে প্রোজেক্ট বা py file নিয়ে কাজ করব বা যে directory তে virtual environment তৈরি করতে চাই সেই directory তে গিয়ে terminal এ টাইপ করতে হবে <a style='color:green'> python3 -m venv environmentName </a> 
 

```
    
    # create venv     
    
    python3 -m venv env


```


3rd তৈরিকৃত venv ফাইল যে directory তে আছে সেই directory তে গিয়ে environment টা কে active করতে হবে। 

```

    # activate venv

    source env/bin/activate


```

এখন আমরা terminal এ পরিবর্তন দেখতে পাব। বুঝতে পারব আমরা new environment এ আছি। 



### install library under virtual environment

[pypi](https://pypi.org/) থেকে যে কোন লাইব্রেরি এর যে কোন ভার্সন install দিতে পারা যায়। লাইব্রেরি এর নাম লিখে search দিয়ে specific library ইন্সটল দাওয়ার script পাওয়া যায়। 

বা google এ pip install libraryName লিখে search দিলে pypi এর যে link সার্চ এ আসবে সেই link এ গিয়ে ইন্সটল script নিতে পারা যায়। 

### use requirment.txt file 

1st create requirment.txt file বা যে কোন নাম এর txt ফাইল যার ভিতরে যে সব লাইব্রেরি install দিতে হবে তার সব library এর নাম এবং version উল্লেখ করতে হবে। example: 

```

#type under requirment.txt

django==3.0.4
djangorestframework==3.11.0


```

requirment.txt file এ যে সব library এর নাম লিখা হয়েছে তার সব লাইব্রেরি গুলো এক সঙ্ঘে install দিতে type on terminal: 

```

pip3 install -r requirements.txt

```


virtual environment টার under এ কি কি library ইন্সটল দাওয়া আছে টা দেখতে type on terminal:

```

pip freeze

```


### include ipython kernel to virtual environment



make sure যে IPython kernel কে virtual environment এ install দাওয়া আছে। 
virtual environment এ manually kernel কে বিভিন্ন version এর python এ add করা যায়, 
<a style='color:green'> pip install ipykernel </a> দ্বারা। 

১ম virtual environment কে activate করতে হবে 

তারপর <a style='color:green'> python -m ipykernel install --user --name=envName
 </a> --name=virtualEnv এর নাম দিতে হবে। 

এখন jupyter notebook এ গিয়ে New button এ ক্লিক করলে নিউ environment টি দেখতে পারা যাবে এবং প্রয়োজন মত ব্যবহার করা যাবে। 


```

# install ipython consol in virtual environment
pip install ipykernel

# now add python and ipykernel to jupyter notebook
python -m ipykernel install --user --name=env


```



পূর্বের ব্যবহার করা virtual environment কে jupyter notebook এ ব্যবহার করতে চাইলে এই প্রক্রিয়া টি ব্যবহার করতে পারেন। 

```
    # create venv     
    python3 -m venv env

    # activate venv
    source env/bin/activate

    # install ipython consol in virtual environment
    pip install ipykernel

    # now add python and ipykernel to jupyter notebook
    python -m ipykernel install --user --name=env

    # open jupyterNotebook if Installed
    jupyter notebook

```

এখন jupyter notebook এ নতুন env টি দেখতে এবং ব্যবহার করতে পারা যাবে। 

![image](https://drive.google.com/uc?export=view&id=1t40yKloEg57jiog7KqUqfg_iyEKdSvrO)





## create virtual environment with virtualenv 

১ম virtualenv কে OS এ ইন্সটল দিতে হবে যেন যে কোন directory তে virtualenv ব্যবহার করে environment তৈরি করতে পারি। open terminal and type: 

```

    #install virtualenv:
	
    pip install virtualenv

```


২য় যে কোন directory তে  virtual environment  create করা যায় by type on terminal 

```

    #create virtual environment:
	
    virtualenv envName

```


৩য় virtual environment activate করতে type on terminal :

```

    #activate virtualenv:
	
    cd envName
	cd Scripts
	activate


```


<mark> library install এবং ব্যবহার সব টাইপ এর environment এ প্রায় same </mark>





## create virtual environment with anaconda 

[follow official instruction](https://docs.anaconda.com/anaconda/install/linux/)


### create environment 

python এর যে কোন version এবং যে কোন নাম এর virtual environment তৈরি করার জন্য anaconda বিশেষভাবে popular.   

virtual environment তৈরি করার জন্য terminal এ গিয়ে type করতে হবে,
<a style='color:green'> conda create --name envName python=3.XX </a> envName = environmentName , python=3.6 python's specific version 

```

conda create --name envName python=3.6


or

conda create -n envName python=3.5 anaconda


```


<mark> library install এবং ব্যবহার সব টাইপ এর environment এ প্রায় same </mark>

pipline ব্যবহার করে বা pip install এর দ্বারা সব library activated environment এ install দাওয়া যায়। 




### activate anaconda environment

anaconda environment activate করার জন্য <a style='color:green'> conda activate environmentName </a> ব্যবহার করা হয়।  

environment list দেখার জন্য <a style='color:green'> conda env list </a> ব্যবহার করা হয়। 

activated environment এ installed libraries এর list দেখার জন্য <a style='color:green'> conda list </a> ব্যবহার করা হয়। 


```
# to activated environment 

conda activate environmentName


# to deactivated environment

conda deactivate


# to see environment list 

conda env list


# to see installed library 

conda list


```
### Save installed package to be reinstalled formate


installed packages গুলো requirements.txt বা environment.yml file এ save করতে নিম্নের command ব্যবহার করা যায়। 

For conda, I would first export the environment list as environment.yml and omit the package build numbers, which is often what makes it hard to reproduce the environment on another OS.

```
conda env export > environment.yml --no-builds

```


Output:

```
name: myenv
channels:
  - defaults
  - conda-forge
dependencies:
  - blas=1.0
  - ca-certificates=2020.10.14
  - certifi=2020.6.20
...

```

For pip, what you describe above is apparently a well-known issue in more recent versions of pip. The workaround to get a "clean" requirements.txt file, is to export as such:


```
pip list --format=freeze > requirements.txt

```

Output:

```
certifi==2020.6.20
cycler==0.10.0
kiwisolver==1.2.0
matplotlib==3.3.2
mkl-fft==1.2.0
...

```





