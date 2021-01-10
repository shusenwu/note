```
第一轮：是个国人妹子。面经里最近的热门topic，类似于meeting room，这次换了个马甲成了program执行时间的安排。
input是一个N行2列的int[][]，每行第一个元素是程序开始时间，第二个元素是程序持续时间（这是一个改动，meeting room给的是起始时间）。然后给一个新的程序[起始时间，持续时间]，问能不能加到现有的schedule里面，不能跟现有的interval 重合。可以就加，返回true，不行就不加，返回false。我先给了个解法按开始时间sort，然后一个一个interval试着往里塞，因为要sort所以TC是O(NlogN)。写了code。
Follow up也是个热门followup，问假如已经sort好了有没有更快的解法。用binary search在所有interval的起始时间里找the largest smaller one。写了code


```


第一题，给一个0.1的matrix，类似于number of island，有点不一样的是，island定义是如果0water被1land包围住，他也属于island。最后求max size of island。  
可以从边界的0开始bfs/dfs, mark起来，剩下的没被mark的 就是都是不同的岛屿了。  

 
第二题，给一个int array，select elements,使得sum最大。条件是，选择的数字之间abs gap不能等于1.比如 [1,2,2,3,3]，最后的选择[1,3,3], return 7.不能选2是因为它和1或者3的abs diff是1。  
https://leetcode.com/problems/delete-and-earn/  
 
2. 飞机航班信息，给定一个时间问是否可以到达目的地.

```
4. 公司的组织架构（人员的report line情况），问某一个人有哪些人report， followup是如果组织架构实时改变怎么办，如何加缓存。  
 
可以维护每个人的上级以及下级，例如输入为 [0, 1, 2, 3], [1, 2, 4]，其中第一个为经理，后面的为下属，可以一次遍历建立这样的对应表（可以用嵌套列表来实现）

员工，下级，上级
0，[1, 2, 3]，[]
1，[2, 4]，[0]
2，[]，[0, 1]
3，[]，[0]
4，[]，[1]

这样无论是查找员工数量，实时更新架构都能够快速找到答案。然后更新的话也很简单，双向更新即可。
```

面经题，ceo, manager， 问某个manager底下有多少员工。大家可以搜一搜面经

最短路径，deliver 东西。 有的地方有加油站，到加油站把油加满。 问最短路径能把东西都送到客人家。

4. 套信封: 每个[长，宽]代表一个信封的长宽，给你一套信封：[[1,1],[2,2],[2,1],[3,3]]，问你最多能有多少个套一起。
这个例子的答案是 3, [1,1]->[2,2]->[3,3]
https://leetcode.com/problems/russian-doll-envelopes/


5. 系统，设计Amazon S3

4. similar to LFU/LRU: implement functions to insert/delete/increase/decrease the value of a given key, and find the keys 
with maximum/minimum value in a dictionary

```
Implement a function nGram(int n, string s) and return a dict of 1-gram to n-gram strings

Ex: string s = "I have a pen and a book"
if n = 1, dict = ["I": 1, "have": 1, "a": 2, "pen": 1, "and": 1, "book": 1]
if n = 2, dict = ["I": 1, "have": 1, "a": 2, "pen": 1, "and": 1, "book": 1, "I have": 1, "have a": 1, "a pen": 1, "pen and": 1, "and a": 1, "a book": 1]
if n = 3, dict = ["I": 1, "have": 1, "a": 2, "pen": 1, "and": 1, "book": 1, "I have": 1, "have a": 1, "a pen": 1, "pen and": 1, "and a": 1, "a book": 1, "I have a": 1, "have a pen": 1, "a pen and": 1, "pen and a": 1, "and a book": 1]

Follow up: how to reduce the memory usage of the dict
```

```
1. 1423. Maximum Points You Can Obtain from Cards  
https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/  
follow-up：还是取数组头和尾k次，新加入multiplier int[k], 每次也从multiplier 按序取出数相乘算结果，
求max，例子：k=2, array [3,2,1,4], multiplier [1,2], 第一次取结果：4*1， 第二次取 3*2, 总共10；用的dfs + memorization
```


```
第2轮：最近常见的简单雇主树结构；给adjacent list (有向图)
问1： 什么情况下valid：graph 中只有一个disjoint set并且没有cycle， 不在意是否indegree>=2
问2: Valid 下求某个人的分数，即此subtree的count
问3: Validate given graph，用topology sort
 
```


```
Delay Sechdule 
https://www.1point3acres.com/bbs/thread-161803-2-1.html
```



BQ:

另外还有一轮就是behavior. 问了challenging project,如何跟同事相处，如何处理deadline之类的。  
 
