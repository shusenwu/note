# System Design

第一轮设计题，设计一个在线的下棋游戏  

系统设计 + OOD, 设计game engine， 从单机到多人到multi billion user的case。  

考的设计云存储服务  

Design rate limiter  
频率限制器，几种use case如何应对，比如一分钟发10条推，跟随20个人，等等。回答说每种case用一个队列，问能不能优化到所有case共用同一个数据结构，没想出来。另外还要画系统结构图，所有api   
Rate limit 10 tweets in 15 mins  
 

tic-tac-toe     
1.设计Server和Client Class，设计这两个的API，要求2个玩家联机对战，从连服务器开始的所有过程都要考虑；    
2.尝试Implement一些自己设计的API；  
3.high-level design，假设1亿名玩家同时在线  
4.新增的服务器有哪些API  
5.各个high-level component的具体实现和细节问题，问的非常随机和分散。  

event counter 
实现一个eventCounter， 感觉地里也有人发过， 实际要求实现的功能有三个，不同的counting的功能 。
实现这个class的几个功能。记录一个event（id 和timestamp）， 读取一段时间里每个小时的event数量。 还有另外一个功能也是读取event的，具体的要求忘记了

设计一个twitter用户上传文件的系统。  

1. Design a tweet service, return the latest 1000 tweets from all the people that I'm following  

system design, kv store， 要实现3个method, set, get, delete。着重讨论数据如何存取以及replication, load balancing, durability, how to add/delete hosts in the cluster, metrics to monitor, estimate request latency.   

# Algorithm  
AutoComplete  

212. Word Search II   https://leetcode.com/problems/word-search-ii/  

add(), delete(), remove(), O(1)  

Hashmap的具体实现，用linear probe，  
实现哈希表，讨论了几种碰撞处理，然后要求实现单数组实现的那种，然后不断加要求，比如软删除，硬删除，resize等。所谓软删除就是那个位上对应的flag设一下就行了  

https://www.geeksforgeeks.org/boggle-set-2-using-trie/  


2. First Non-repeating char in a string, followup, in a stream. 2nd, the shortest path between two nodes on graph. 
https://leetcode.com/problems/first-unique-character-in-a-string/   
```PYTHON
class Solution(object):
    def firstUniqChar(self, s):
        """
        :type s: str
        :rtype: int
        先One loop 数每个字母的频率
        再one loop找屏幕是1 的
        """
        if not s: return -1
        d = collections.defaultdict(int)

        for char in s:
            d[char] += 1

        for i, c in enumerate(s):
              if d[c] == 1:
                    return i
        return -1
    ```    
        
Coding. Auto complete system, 用trie实现， follow 是如何delete word from trie 和 achieve concurrency.  

https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/   

3. Reverse words in place.
https://leetcode.com/problems/reverse-words-in-a-string-ii/   
# BQ  
经理和一个小姐姐，和你一起回顾人生经历，你觉得你的过往mentor、manager会怎么评价你，如果你再有机会实习、工作之前的内容，哪些方面会做的不一样。每次经历都要重复这几个问题。  
 Behavior，从简历上每一段经历开始讲起(even internship and grad school)， why did you do this, how do you like it, what did you learn, what's your feedback, what's your weakness   
 每段经历都要问，哪些做得好，哪些做得不好，举例说明，老板怎么样，老板对你有哪些评价   
