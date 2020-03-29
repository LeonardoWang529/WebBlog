---
title: Formula_in_Data_Anaysis_for_ML_2
tags:
  - Data Analytic
  - Formula
categories: Machine Learn
date: 2019-09-28 02:13:57
---



Content-based recommendations
 -Recommendation systems
	Main idea: recommend items to customer C similar to previous items rated highly by C
	1. For each user, create a user profile based on the content the user has consumed(when utility matrix is not binary, using normalization: Mean-centering)
	2. Calculate Similarities(Jaccard Similarity: sim(x,y)=(xny)/(xuy). here leo has 5 interest tags. the big lebowski has 2(正好在这5个tags里) included interested tag. So sim = 2/5)(不管是我的1 还是 电影的1 应该是等价的，所以都应该被算在内。相当于 6个feature里 我有5个是不喜欢的。 上面是 5个feature里有3个是我不喜欢的。)
	3. Rank
	4. Recommend

	当utility matrix 不是01时，可能会出现 cos similarity 无比相似的情况，这个时候，需要Min-max scaling (normalization) which is divide by mean.

Neighborhood-based collaborative filtering
 -User-based Collaborative Filtering
	INTUITION: Users with similar ratings/purchases have analogous interests
	  • Phase1:NeighborhoodFormation	
	     Mean-centered
		1. take average
		2. each mins avg num
	     Cos similarity	
		3. cos simiarlarity between each people and me on each iteam.
		4.find highest 2 person
	  • Phase2:Recommendationphase
	     Average/Weighted Average/Mean-centered
		5. calculate the one I have not rated

	Problems:
		1. not scalable
		2. cold start

 -Item-based Collaborative Filtering
	Main idea: Compare items based on their pattern ratings across users
	  • Compute pair-wise similarities of items(Big advantage: This step can be performed offline!!!)
	     Mean-centered
		1. take average for all the rating for each person
		2. each mins avg num on this col		
	  • Adjusted cosine similarity	
	     Adjusted Cos similarity
		3. cos simiarlarity between each iteam and my unreated iteam 
	  • Recommendationphase
		4. based on adjusted cos value, find the cloest rating iteam from the film I have rated. Use these rating * ralated cos val. then add them together to get sum. Add the cos value we just used take abs value and add together to get sum1. use sum/sum1. in the end plus the mean value of mine. get the perdict rating. (根据adjusted cos值，找出和你要预测的电影相关性最高的几部你已经rate过的电影。分别用这几部电影的rate值乘以相对应的cos值，然后相加计算出一个sum。再将刚才用到的cos值，取绝对值后相加算一个sum1. 用sum/sum1. 最后加上我的rating的平局值。


	     


