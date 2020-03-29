---
title: Formula_in_Data_Anaysis_for_ML
date: 2019-09-17 23:53:22
tags:
- Data Analytic
- Formula
categories: 'Machine Learn'
---

Data Analytic Formula

Min-Max normalization:
Minmax normalization is a normalization strategy which linearly transforms x to y= (x-min)/(max-min), where min and max are the minimum and maximum values in X, where X is the set of observed values of x. 

It can be easily seen that when x=min, then y=0, and
When x=max, then y=1.
This means, the minimum value in X is mapped to 0 and the maximum value in X is mapped to 1. So, the entire range of values of X from min to max are mapped to the range 0 to 1.


Jaccard Similarity: 
sim(x,y)=(xny)/(xuy). 
Jaccard Distance is used to measure similarities. Using similars between x and y devided total of x and y. We can describe how similar they are. we can use this to build recommand system.

Example: 
https://docs.google.com/spreadsheets/d/1RmRt5rk1_RF_tRA80boNz3bNNAbUJ_-6TnhZ3cFZIEg/edit?usp=sharing

here leo has 5 interest tags. the big lebowski has 2 included interested tag. So sim = 2/5

不管是我的1 还是 电影的1 应该是等价的，所以都应该被算在内。相当于 6个feature里 我有5个是不喜欢的。 上面是 5个feature里有3个是我不喜欢的。

