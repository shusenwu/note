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
