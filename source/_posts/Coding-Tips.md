---
title: Coding Tips
date: 2017-11-15 23:39:50
tags: 
- Tips
categories: 'Coding'
---

1. Third party lib initial should be placed or created outside of main code.
When needs to use, call the object.
Reason: Third party lib like aws is alway updating. every time updating, we need to change all the code in side of our project. If we wrap it and put it outside, every time we only need to change the wrappers.

2. 第三方lib 要用wrap在外面wrap起来使用，不然升级要一个地方一个地方改

3. 问题，有的时候自己想一个问题，想不清楚，思想也不集中。但是一问别人，一开口，自己就想清楚了，就知道怎么查了，知道答案了。怎么回事怎么办？ 
	答：这是因为想问题困在一个细节上了，想了太久，困住了太久，眼睛里只有这个小问题。
	这个时候要 强迫自己 跳出小细节，在大框架下来思考问题。
	开口问别人，实际上就是跳出了小细节，在大框架下思考。
	解决办法，可以试试，想像我去问别人，然后自言自语一下，找个答案。
	或者写下来问题的解决步骤。

4. 做为一个协同开发人员，always 有空就要review code。

5. 当出现2个table对另一table 不确定数量多的col的时候，应该考虑建一个relation table。
AdminDocter -> UserProfile + Treatment
因为 admindocter 和userprofile 之间数据不唯一，所以为了保证唯一性，可以建一个 adminDocter 和 userprofile的relation table。一个aduserrel 对应一个treatment。就可以构成 关系了。
同理 证明 VideoVisit -> ActionLkp + AIresult

6. 在开始写程序或程序设计之前，先把business modle 和可能出现的情况先列出来，不然会一直要改程序。在开始写程序，先把程序设计从头到尾每个细节想清楚，不能有太多的疏漏，和没想到的点。宁愿多花点时间。否则可能整个程序会需要重新改写。

7. 遇到什么lib，想想他是怎么实现的，比如 db的 index 是用tree 和 binary search实现的。

8. 做design的时候想，那些会被reused，那应该单独拿出来放在外面

9. 永远把问题缩到，简化到最小点，在debug

10. 

