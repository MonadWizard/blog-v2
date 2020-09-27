---
title: seaborn essential charts 
keywords: seaborn  Bangla Tutorials, bangla seaborn, Bangla Python, Blog Bangla, Monad wizard
last_updated: Aug 04 , 2020
# tags: [getting_started]
summary: "Here I try to make familler to  Basic seaborn Topic with short note. "
sidebar: mydoc_sidebar
permalink: visualization_seaborn.html
folder: mydoc
---



[official Doc example gallery ](https://seaborn.pydata.org/examples/index.html)




**Seaborn** is a Python data visualization library based on Matplotlib. In this project, I explore Seaborn. I discuss Seaborn API overview, its functionality, setting Seaborn aesthetic parameters and colour palette. I discuss different distributions, various plot types and multi-plot grids with seaborn.  


The contents of this project is divided into various sections which are listed below:-



## 1. Introduction to Seaborn

**Seaborn** is a data visualization library in Python. It is used to produce statistical graphics in Python. It is built on top of Matplotlib. It also supports NumPy and Pandas data structures. It also supports statistical units from SciPy.

In the world of analytics, data visualization plays an important role to explore and understand the data. Seaborn is developed to make this process of exploring and understanding the data smooth. It provides a high-level interface to produce high quality statistical graphics. The customizability and backend options for Matplotlib makes it easy to generate publication-quality figures.

In this project, I discuss **Seaborn** and present a high level overview of various plotting functions and tools associated with Seaborn.



## 2. Comparison of Seaborn and Matplotlib

Seaborn uses Matplotlib to draw plots. Many actions can be accomplished with only Seaborn functions. Further customization options 
might require using Matplotlib directly. Seaborn is not an alternative to Matplotlib. We can think of it as a complement to Matplotlib. As it is built on top of Matplotlib, we can call Matplotlib functions directly for creating simple plots.


It is summarized that – 

**“If Matplotlib tries to make easy things easy and hard things possible, Seaborn tries to make a well-defined set of hard things easy too in a well-defined way.”**

Seaborn helps to resolve two major problems faced by Matplotlib. The problems are:-

1.	Working with Matplotlib’s default parameters

2.	Working with data frames



## 3. Seaborn API Overview

Seaborn has various types of plots which can satisfy various types of data visualization requirements. The plots can be categorized 
into seven categories – relational plots, categorical plots, distribution plots, regression plots, matrix plots and multi-plot grids.


**1.	Relational plots**

We can visualize statistical relationships with relational plots. There are three types of relational plots – **relplot()**, **scatterplot()** and **lineplot()**. We can use these plotting functions to see trends and patterns that indicate a relationship.


**2.	Categorical plots**

If one of the variable is categorical, we can visualize the relationship involving categorical data. In Seaborn, there are several different ways to visualize a relationship involving categorical data. There are various functions for plotting categorical data. 
We can plot categorical scatterplots with **stripplot()** and **swarmplot()** functions. Similarly, we can plot categorical distribution plots with **boxplot()**, **violinplot()** and **boxenplot()** functions. Also, we can plot categorical estimate plots with **pointplot()**, **barplot()** and **countplot()** functions.


**3.	Distribution plots**

We can visualize the distribution of a dataset with the distribution plotting functions. We can plot univariate distribution with **distplot()** function. It will draw a histogram and fit a kernel density estimate (KDE). The **kdeplot()** function  is used for plotting the shape of a distribution. We can use **rugplot()** function to plot data points in an array as sticks on an axis. We can draw a plot of two variables with bivariate and univariate graphs with jointplot() function. We can visualize pairwise relationships in a dataset using **pairplot()** function.



**4.	Regression plots**

In Seaborn, there are various functions for visualizing linear relationships in a dataset. There are two main functions that are used to visualize linear relationship between variables. These functions are **regplot()** and **lmplot()**. They are closely related and share much of their core functionality. There is a third function called **residplot()** which is used to plot the residuals of a linear regression model.


**5.	Matrix plots**

There are two plotting functions which are used to plot matrix plot types. These are **heatmap()** and **clustermap()**. Heatmap() is used to plot rectangular data as a colour-encoded matrix. Clustermap() is used to plot a matrix dataset as a hierarchically-clustered heatmap.


**6.	Multi-plot grids**

While exploring medium-dimensional data, a useful technique is to draw multiple instances of the same plot on different subsets of the dataset. It allows us to extract large amount of information about complex data. Seaborn provides plotting functions to link the structure of the plot to the structure of the dataset and draw multi-plot grids.


To use these features, the dataset has to be in a Pandas dataframe. It must be in the **tidy data format**. It means that the dataframe should be structured such that each column is a variable and each row is an observation.


Multi-plot grids are further divided into three categories - **Facet grids**, **Pair grids** and **Joint grids**.


Facet grids provide three functions. **FacetGrid()**, **FacetGrid.map()** and **FacetGrid.map_dataframe()**. These functions are used to visualize the distribution of a variable or the relationship between multiple variables separately within subsets of the dataset.


Pair grids provide plotting functions to visualize pairwise data relationships. The basic plotting function is **PairGrid()**. It allows us to draw a grid of small subplots using the same plot type to visualize data. In a **PairGrid()**, each row and column is assigned to a different variable. So the resulting plot shows each pairwise relationship in the dataset.


The third category of plot is Joint grids. It provide plotting functions to draw Joint plots. There are four types of Joint grid plotting functions. They are **JointGrid()**, **JointGrid.plot()**, **JointGrid.plot_joint()** and **JointGrid.plot_marginals()**. **JointGrid()** function is used to draw a bivariate plot with marginal univariate plots. **JointGrid.plot()** is a shortcut to 
draw the full plot. **JointGrid.plot_joint()** is used to draw a bivariate plot of x and y. **JointGrid.plot_marginals()** is used 
to draw univariate plots for x and y separately. 




## 4. Seaborn functionality

Seaborn offers lot of functionality which makes it effective for many data visualization tasks. These functionalities are listed 
below:-


•	Seaborn provides a dataset-oriented API to examine relationships between variables. 

•	It provides functions to fit and visualize linear regression models for different types of independent and dependent variables.

•	Seaborn provide functions for visualizing univariate and bivariate distributions and for comparing them between subsets of data.

•	It provides plotting functions for using categorical variables to show observations or aggregate statistics.

•	It helps us to visualize matrices of data and use clustering algorithms to discover structure in those matrices.

•	Seaborn provides a plotting function to plot statistical time series data. The function provides flexible estimation and representation of uncertainty around the estimate.

•	It provide tools for choosing styles, colour palettes, palette widgets and utility functions. These tools help us to make beautiful plots that reveal patterns in the data.

•	It provides several built-in themes for producing stylish looking Matplotlib graphics. 



## 5. Seaborn installation

To install the latest release of Seaborn, we can use **pip** and run the following command in the terminal:

`pip install seaborn`


It is also possible to install the released version using **conda** as follows:


`conda install seaborn`


Alternatively, we can use **pip** to install the development version directly from github:


`pip install git+https://github.com/mwaskom/seaborn.git`


**Dependencies**

•	Seaborn requires Python 2.7 or 3.5+ platform.


**Mandatory dependencies**


Seaborn requires following mandatory Python packages to be installed on the system.


•	NumPy(>= 1.9.3)

•	Scipy (>= 0.14.0)

•	Matplotlib (>= 1.4.3)

•	Pandas (>= 0.15.2)

**Recommended dependencies**

Seaborn also needs statsmodels (>= 0.5.0) package to be installed on the system.



## 6. Import Python libraries

In this section, we import the necessary Python libraries Numpy, Pandas and Matplotlib with their usual shorthand notation.

`import numpy as np`

`import pandas as pd`

`import matplotlib.pyplot as plt`

`%matplotlib inline`



## 7. Import Seaborn

We can import Seaborn as

`import seaborn`

The shorthand notation of Seaborn is **sns**. So, we can import seaborn with usual shorthand notation.

`import seaborn as sns`



## 8. Import datasets

Seaborn has few important datasets in the library. When Seaborn is installed, the datasets download automatically. We can download 
any dataset with **load_dataset()** function.

**Importing data as Pandas dataframe**

In this section, we will import a dataset. By default, this dataset loads as Pandas dataframe. There is a dataset called **tips** 
in the library. We can import this dataset with the following line of code:-


`tips = sn.load_dataset(‘tips’)`

We can view the first five lines of code with the following command:-

`print(tips.head())`

To view all the available datasets in the Seaborn library, we can use the following command with the **get_dataset_names()** function as shown below:-

`print(sns.get_dataset_names())`



## 9. Set aesthetic parameters with set( ) method

We can set the aesthetic parameters of Seaborn plots with the **set()** method. The aesthetic parameters are context, style, 
palette, font, font_scale, color_codes, dictionary of rc parameters. 

So, we can set the default aesthetic parameters by calling Seaborn's **set()** method. 

`sns.set()`



## 10. Seaborn colour palette

Colour plays very important role in data visualization. Colour adds various dimensions to a plot when used effectively. A palette 
means a flat surface on which a painter mixes paints.


Seaborn provides a function called **color_palette()**. It can be used to give colours to plots and adding aesthetic value to it. 
It return a list of colors defining a color palette.


There are several readily available Seaborn palettes. These are:-

•	Deep

•	Muted

•	Bright

•	Pastel

•	Dark

•	Colorblind


Besides these we can also create new palettes.


There is another function **seaborn.palplot()** which deals with color palettes. This function plots the color palette as a horizontal array.


**Qualitative Color Palettes**


Qualitative or categorical palettes are best suitable to plot the categorical data as follows:-

`current_palette1 = sns.color_palette()`

`sns.palplot(current_palette1)`

`plt.show()`

We can see the desired number of colors by passing a value to the n_colors parameter. Here, the **palplot()** function is used to plot the array of colors horizontally.


**Sequential Color Palettes**

Sequential plots are suitable to express the distribution of data ranging from relative lower values to higher values within a range. Appending an additional character “s” to the color passed to the color parameter will plot the Sequential plot. 


We need to append ‘s’ to the parameter like ‘Greens’ as follows:-


`current_palette2 = sns.color_palette()`

`sns.palplot( sns.color_palette(“Greens”))`

`plt.show()`
 

**Diverging Color Palette**

Diverging palettes use two different colors. Each color represents variation in the value ranging from a common point in either direction. We assume plotting the data ranging from -1 to 1. The values from -1 to 0 takes one color and 0 to +1 takes another color. 


By default, the values are centered from zero. We can control it with parameter center by passing a value as follows:-


`current_palette3 = sns.color_palette()`

`sns.palplot( sns.color_palette(“BrBG”, 7))`

`plt.show()`


**Default Color Palette**

We can set the default color palette of a Seaborn plot using **set_palette()** function. The arguments are same for both **set_palette()** and **color_palette()** functions, but the default Matplotlib parameters are changed so that the palette 
is used for all plots.



`def sinplot(flip=1):` 

`x = np.linspace(0, 15, 100)`

`for i in range(1, 5):`

`plt.plot(x, np.sin(x + i * .5) * (7 - i) * flip)` 

`sns.set_style("white")`

`sns.set_palette("husl")` 

`sinplot()` 

`plt.show()`



## 11. Plotting Univariate Distribution with distplot()


The most important thing to do while analysing the data is to understand its distribution. Seaborn helps us to understand the 
univariate distribution of data.


The **distplot()** function provides a quick look at univariate distribution. This function will plot a histogram that fits the 
kernel density estimate of the data.


We can use the **distplot()** function as follows:-


`sns.distplot(tips['total_bill'])`

`plt.show()`



## 12. Seaborn - Histogram


Histograms represent the data distribution by forming bins along the range of the data and then drawing bars to show the number of observations that fall in each bin.


We can use the same **distplot()** function to plot a histogram as follows:-


`sns.distplot(tips['total_bill'], kde=False)`

`plt.show()`


The kde parameter is set to false. As a result, the representation of the kernel estimation plot will be removed and only histogram is plotted.



## 13. Seaborn – Kernel Density Estimation


Kernel Density Estimation (KDE) is a way to estimate the probability density function of a continuous random variable. It is used for non-parametric analysis. 

Setting the hist parameter to false in distplot() function will yield the kernel density estimation plot.

`sns.distplot(tips['total_bill'], hist=False)`

`plt.show()`



## 14. Plotting Bivariate Distribution with jointplot()

Bivariate Distribution is used to determine the relation between two variables. This mainly deals with relationship between two variables and how one variable is behaving with respect to the other. 


The best way to analyze Bivariate Distribution in seaborn is by using the **jointplot()** function. 

**Jointplot()** creates a multi-panel figure that projects the bivariate relationship between two variables and also the univariate distribution of each variable on separate axes.


`sns.jointplot(x="total_bill", y="tip", data=tips)`

`plt.show()`



## 15. Seaborn – Scatter Plot

A scatter plot can be used to demonstrate relationship between two variables x and y. A simple scatter plot can be drawn as follows:-

`sns.scatterplot(x="total_bill", y="tip", data=tips)`

`plt.show()`

The relationship between the variables can be shown for different subsets of the data using the hue, size and style parameters.



## 16. Visualizing pairwise relationship with pairplot()

Some datasets contain many variables. In such cases, the relationship between each and every variable should be analysed. So, we 
need to plot pairwise relationships in a dataset.


To plot multiple pairwise bivariate distributions, we can use **pairplot()** function. This shows the relationship for (n,2) 
combination of variable in a dataframe as a matrix of plots and the diagonal plots are the univariate plots.


We can plot a pairplot as as follows:-

`sns.set_style("ticks")`

`sns.pairplot(tips)`



## 17. Plotting categorical data

So far, I have covered histogram, scatter plot and kde plots. They are used to analyze the continuous variables under study. 
These plots are not suitable when the variable under study is categorical. 

When one or both the variables under study are categorical, we can use plots like **striplot()** and **swarmplot()** to plot 
categorical data.



## 18. Seaborn – Strip Plot

A **stripplot()** is used to draw a scatterplot where one variable is categorical. It represents the data in sorted order along 
any one of the axis.

We can plot a stripplot as follows:-

`sns.stripplot(x="day", y="total_bill", data=tips)`

`plt.show()`

We can add jitter to bring out the distribution of values as follows:-

`sns.stripplot(x="day", y="total_bill", data=tips, jitter=True)`

`plt.show()`



## 19. Seaborn – Swarm Plot


Another option which can be used as an alternate to ‘jitter’ is to use function **swarmplot()**. This function positions each 
point of scatter plot on the categorical axis and thereby avoids overlapping points. 


So **swarmplot()** can be used to draw categorical scatterplot with non-overlapping points.


We can plot a swarmplot as follows:-


`sns.swarmplot(x="day", y="total_bill", data=tips)`

`plt.show()`



## 20. Distribution of Observations


When dealing with a dataset, the first thing that we want to do is get a sense for how the variables are distributed. 

We can use box plots and violin plots to plot the data distribution.



## 21. Seaborn – Box Plot


We can draw a box plot to show distributions with respect to categories. Boxplot is a convenient way to visualize the distribution 
of data through their quartiles. 


Box plots usually have vertical lines extending from the boxes which are termed as whiskers. These whiskers indicate variability 
outside the upper and lower quartiles, hence Box Plots are also termed as box-and-whisker plot. Any Outliers in the data are plotted 
as individual points.


We can plot a box-plot as follows:-


`sns.boxplot(x=tips["total_bill"])`

`plt.show()`

We can draw a vertical boxplot grouped by a categorical variable as follows:-


`sns.boxplot(x="day", y="total_bill", data=tips)`

`plt.show()`



## 22. Seaborn – Violin Plot

Violin Plots are combinations of the box plot with the kernel density estimates. So, these plots are easier to analyze and 
understand the distribution of the data.

We can draw a single horizontal violin plot as follows:-

`sns.violinplot(x=tips["total_bill"])`

`plt.show()`

We can draw a vertical violinplot grouped by a categorical variable as follows:-


`sns.violinplot(x="day", y="total_bill", data=tips)`

`plt.show()`



## 23. Statistical estimation with Seaborn

Sometimes, we need to estimate central tendency of a distribution. Mean and median are the very often used techniques to estimate 
the central tendency of the distribution.

We can use bar plot and point plot to measure the central tendency of a distribution.



## 24. Seaborn – Bar Plot

A **barplot** shows the relation between a categorical variable and a continuous variable. The data is represented in rectangular 
bars where the length of the bar represents the proportion of the data in that category. 


A barplot show point estimates and confidence intervals as rectangular bars. So, it represents the estimate of central tendency. 


We can draw a set of vertical bar plot grouped by a categorical variable as follows:-


`sns.barplot(x="day", y="total_bill", data=tips)`

`plt.show()`



## 25. Seaborn - Point Plot


Point plots serve same as bar plots but in a different style. Rather than the full bar, the value of the estimate is represented by 
the point at a certain height on the other axis. The Point plot show point estimates and confidence intervals using scatter plot glyphs.


We can draw a set of vertical point plots grouped by a categorical variable as follows:-


`sns.pointplot(x="time", y="total_bill", data=tips)`

`plt.show()`



## 26. Linear relationships with Seaborn


Many datasets contain multiple quantitative variables, and the goal of an analysis is often to relate those variables to each other. 
We can use statistical models to estimate a simple relationship between two sets of observations. These are termed as **regression models**.


While building the regression models, we often check for multicollinearity, where we had to see the correlation between all the combinations of continuous variables and will take necessary action to remove multicollinearity if exists.


There are two main functions in Seaborn to visualize a linear relationship determined through regression. These functions are **regplot()** and **lmplot()**. There is a third function **residplot()** that plot the residuals of a linear regression model.



## 27. Seaborn – Reg plot

The function **regplot()** plot data and a linear regression model fit. It draws a scatterplot of two variables, x and y, and then 
fit the regression model y ~ x and plot the resulting regression line and a 95% confidence interval for that regression.

We can draw the scatterplot and regression line using regplot() as follows:-

`sns.regplot(x="total_bill", y="tip", data=tips)`

`plt.show()`



## 28. Seaborn – Lm plot

The function **lmplot()** plot data and regression model fits across a FacetGrid. This function combines regplot() and FacetGrid. 
It is intended as a convenient interface to fit regression models across conditional subsets of a dataset.


We can plot a simple linear relationship between two variables using lmplot() as follows:-


`sns.lmplot(x="total_bill", y="tip", data=tips)`

`plt.show()`


The regplot() and lmplot() functions are closely related, but the former is an axes-level function while the latter is a figure-level function that combines regplot() and FacetGrid.



## 29. Seaborn – Resid plot


The function **residplot()** plot the residuals of a linear regression. We can plot the residuals as follows:-


`sns.residplot(x="total_bill", y="tip", data=tips)`

`plt.show()`



## 30. Matrix plots with Seaborn

There are two functions which enable us to plot data in the form of a matrix. These are heat map and cluster map.



## 31. Seaborn – Heat map

Seaborn **heatmap()** function plot rectangular data as a color-encoded matrix.

We can plot a heatmap for a numpy array as follows:-

`uniform_data = np.random.rand(10, 12)`

`sns.heatmap(uniform_data)`

`plt.show()`



## 32. Seaborn – Cluster map


Seaborn **clustermap()** function plot a matrix dataset as a hierarchically-clustered heatmap.


We can plot a clustered heatmap of tips dataset as follows:-

`df1 = tips[['total_bill', 'tip', 'size']]`

`sns.clustermap(df1)`

`plt.show()`



## 33. Multi-plot grids with Seaborn

When exploring medium-dimensional data, a useful approach is to draw multiple instances of the same plot on different subsets of the dataset. This technique is sometimes called either “lattice”, or “trellis” plotting, and it is related to the idea of drawing multiple instances of the same plot. It allows us to quickly extract a large amount of information about complex data.

Seaborn provides three types of grids – **facet grid**, **pair grid** and **joint grid** to draw multiple instances of the same plot.



## 34. Seaborn – Facet Grid

Seaborn **Facetgrid()** function enable us to draw multi-plot grid for plotting conditional relationships.

First of all, we initialize a 2x2 grid of facets using the tips dataset as follows:-


`sns.FacetGrid(tips, col="time", row="smoker")`

`plt.show()`

Initializing the grid like this sets up the matplotlib figure and axes, but doesn’t draw anything on them.


The main approach for visualizing data on this grid is with the **FacetGrid.map() method**. We need to provide it with a 
plotting function and the name(s) of variable(s) in the dataframe to plot.


We can draw a univariate plot on each facet as follows:-


`g = sns.FacetGrid(tips, col="time",  row="smoker")`

`g = g.map(plt.hist, "total_bill")`

`plt.show()`



## 35. Seaborn – Pair Grid

Seaborn **PairGrid()** function draws subplot grid for plotting pairwise relationships in a dataset.

We can draw a scatterplot for each pairwise relationship using PairGrid() function as follows:-


`g = sns.PairGrid(tips)`

`g = g.map(plt.scatter)`

`plt.show()`


We can show a univariate distribution on the diagonal as follows:-


`g = sns.PairGrid(tips)`

`g = g.map_diag(plt.hist)`

`g = g.map_offdiag(plt.scatter)`



## 36. Seaborn – Joint Grid


Seaborn **JointGrid()** function help us to set up the grid of subplots.


We can initialize the figure but don’t draw any plots onto it as follows:-


`g = sns.JointGrid(x="total_bill", y="tip", data=tips)`


We can add plots using default parameters as follows:-


`g = sns.JointGrid(x="total_bill", y="tip", data=tips)`

`g = g.plot(sns.regplot, sns.distplot)`



## 37. Summary


In this project, I present a high level overview of Seaborn and associated plots.


I discuss Seaborn and compare it with Matplotlib. I present Seaborn API overview and discuss Seaborn functionality. I discuss how 
to set aesthetic parameters of a plot and how to set color styles.


Then, I discuss various types Seaborn plots. I plot univariate distribution with distplot() function. Then, I discuss histogram and kernel density estimation plots. I plot bivariate distribution with jointplot() function and discuss Seaborn scatter plot.


I visualize pairwise relationship with pairplot() function. Then, I plot categorical data with Seaborn strip plot and swarm plot. I visualize the distribution of observations with Seaborn box plot and violin plot. I measure the statistical estimates with Seaborn bar plot and point plot.


I visualize the linear relationships between variables with Seaborn reg plot and lm plot. I visualize the residuals with Seaborn resid plot. I discuss Seaborn heat map and cluster map. Then, I discuss multi-plot grids with Seaborn. I discuss facet grid, pair grid and joint grid.



## 38. References

The Seaborn plots and galleries in this project are taken from the following websites:-

1.	Seaborn official documentation (https://seaborn.pydata.org/)

2.	https://jakevdp.github.io/PythonDataScienceHandbook/04.14-visualization-with-seaborn.html

3.	Seaborn tutorial from tutorialspoint


































