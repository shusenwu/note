1153. String Transforms Into Another String  https://leetcode.com/problems/string-transforms-into-another-string/   
```
1. Coding: 一种纸牌游戏叫game of set，网上搜的到。每张牌有四种属性（普通的扑克牌有两种属性，数字和花色，数字有13种值，花色有4种值），每个属性都有3种值。比如
大小：大中小
数字：123
颜色：红黄蓝
花色：梅心方
也就是说一共有81张不同的牌
任意三张牌可以组成一个set的条件是，对于任意一个属性，三张牌要么都是同样的值，要么都是不同的值。比如“小1红梅”， “中1蓝心”
， “大1黄方”这三张牌就能组成一个set，因为对于任意一个属性，这三张牌要么值都一样，要么值都不一样。显然三张一样的牌是可以组成一个set的。
题目是，给你三张牌，如何判断它们是不是能组成set。
followup 1: 给你12张牌，如何判断里面是不是至少有1个set
followup 2: 给你stream of cards，告诉你有一个constant time的算法可以判断什么时候有第一个set。也就是说在一定数量的牌里面一定会有一个set，
问你怎么写这个算法。这道题没做出来，面试官提示的（我的理解）是用抽屉原理（pigeonhole）找相斥。

2. Coding: 给你list of log，每个log包括[time, task_id, start/finish]，比如[[1, 1, start], [3, 2, start], [6, 2, finish], [8, 1, finish]]，整个list是按照time排序好的，然后告诉你每个task最多只能用多少时间（比如3）完成。给你这样一个list和int（最多运行时间），问你是不是有任何的task超时，如果有的话要在最早的时间返回。在上面的例子里，在时间6的时候我们就要返回超时，因为task 1已经超时了，不用等到时间8的时候再返回。用的还是sliding window的方法。

 

4. Coding: 类似刷题网五二八。给的是List[List[int]]，比如[[1, 3], [5, 10], [11, 12]]，每个sublist是排序好而且不overlap的，要求随机返回[1, 2, 3, 5, 6, 7, 8, 9, 10, 11, 12]中的一个数。用的还是binary search，先找到是哪个sublist，然后再确定是这个sublist里的第几个数。
followup 1: 如果sublist之间有overlap要怎么算。重点是先问清楚对于重复的数字，是只算一次，还是按照多个算。如果按照多个算，之前的算法还是可以用的。如果同样的数字只算一次，我说的是先merge interval然后再用之前的算法。
https://leetcode.com/problems/random-pick-with-weight/  


```

1287. Element Appearing More Than 25% In Sorted Array https://leetcode.com/problems/element-appearing-more-than-25-in-sorted-array/  

679. 24 Game https://leetcode.com/problems/24-game/   
279. Perfect Squares  https://leetcode.com/problems/perfect-squares/  

```
76. Minimum Window Substring https://leetcode.com/problems/minimum-window-substring/
```

```
1. Two Sum https://leetcode.com/problems/two-sum/
39. Combination Sum https://leetcode.com/problems/combination-sum/
```

```
833. Find And Replace in String    
https://leetcode.com/problems/find-and-replace-in-string/  
```
```
715. Range Module  
https://leetcode.com/problems/range-module/  
```
```
843. Guess the Word  
https://leetcode.com/problems/guess-the-word/  
```

```
833. Find And Replace in String  
https://leetcode.com/problems/find-and-replace-in-string/  
```

```
1293. Shortest Path in a Grid with Obstacles Elimination
https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/   
```  
Meeting room    

3. remove subtree, 但是给出的treenode是parent pointer，不是child  

 
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

```python
1. 1423. Maximum Points You Can Obtain from Cards  
https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/  
follow-up：还是取数组头和尾k次，新加入multiplier int[k], 每次也从multiplier 按序取出数相乘算结果，
求max，例子：k=2, array [3,2,1,4], multiplier [1,2], 第一次取结果：4*1， 第二次取 3*2, 总共10；用的dfs + memorization

class Solution(object):
    def max_points(self, arr, multiplier, k):
        self.memory = {}
        self.dfs(arr, multiplier, k)
        return self.memory[tuple(arr)]

    def dfs(self, arr, multiplier, k):  # assume k >= 1
        if tuple(arr) in self.memory:
            return self.memory[tuple(arr)]
        left = arr[0] * multiplier[0]
        right = arr[-1] * multiplier[0]
        if k == 1:
            self.memory[tuple(arr)] = max(left, right)
        else:
            left_sum = left + self.dfs(arr[1:], multiplier[1:], k - 1)
            right_sum = right + self.dfs(arr[:-1], multiplier[1:], k - 1)
            self.memory[tuple(arr)] = max(left_sum, right_sum)
        return self.memory[tuple(arr)]


arr = [3, 2, 1, 4]
multiplier = [1, 2]
s = Solution()

print(s.max_points(arr, multiplier, 2))
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
 
