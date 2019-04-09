OA2 Coding
===
### 5. Longest Palindromic Substring
https://leetcode.com/problems/longest-palindromic-substring/description/
```python
class Solution(object):
    def longestPalindrome(self, s):
        self.n = len(s)
        self.long = self.left = 0
        for i in xrange(self.n):
            # even
            self.helper(i, i+1, s)
            self.helper(i-1, i+1, s)
        return s[self.left: self.left+self.long]
    
    def helper(self, l, r, s):
        while 0 <= l and r < self.n and s[l] == s[r]:
            l -= 1
            r += 1
        l += 1
        r -= 1
        if r - l + 1 > self.long:
            self.long = r - l + 1
            self.left = l
```
### 937. Reorder Log Files
```python
class Solution(object):
    def reorderLogFiles(self, logs):
        digits = []
        letters = []
		# divide logs into two parts, one is digit logs, the other is letter logs
        for log in logs:
            if log.split()[1].isdigit():
                digits.append(log)
            else:
                letters.append(log)
        letters.sort(key = lambda x: (x.split()[1:], x.split()[0])) 
        result = letters + digits  #put digit logs after letter logs
        return result
```
### Length K substring with k-1 distinct characters 
![distinck-k](https://github.com/shusenwu/note/blob/master/amazon/123125pkmerno0xkm4rrp7.png)
```python
def subStringLessKDist(inputString, num):
    if not inputString or len(inputString) == 0 or num <= 1 or inputString <= num:
        return []
    res = set()
    for i in xrange(len(inputString)-num+1):
        cur = inputString[i: i+num]
        if len(set(cur)) == num - 1:
            res.add(cur)
    return list(res)
```
### 819. Most Common Word
https://leetcode.com/problems/most-common-word/description/  
```python
class Solution(object):
    def mostCommonWord(self, paragraph, banned):
        paragraph = re.findall(r'\b[a-zA-Z]+', paragraph.lower())
        dic = collections.Counter(paragraph).most_common()
        for x in dic:
            if x[0] not in banned:
                return x[0]
                break
```
### Maximum Minimum Path 
You are gonna climb mountains represented by a matrix. Each integer in the matrix represents the altitude at that point. You are supposed to climb from the top-left corner to the bottom-right corner and only move rightward or downward in each step. You can have many paths to do so. Each path has a minimum altitude. Find the maximum among all the minimum altitudes of all paths. e.g.
```
[[5, 4, 5], [1, 3, 6]]
```
Three paths: 5 1 3 6,5 4 3 6,5 4 5 6. Minimums are 1, 3, 4 respectively. Return the maximum in them which is 4. another example:
```
[[8, 4, 7], [6, 5, 9]]
```
3 paths:
```
8-4-7-9 min: 4 8-4-5-9 min: 4 8-6-5-9 min: 5 return: 5
```

```python
class Solution:
    def minMaxPath(self, matrix):
        if len(matrix) == 0 or len(matrix[0]): return float('-inf')
        r, c = len(matrix), len(matrix[0])
        self.re = float('-inf')
        def dfs(i, j, pathMin):
            if i >= r or j >= c:
                return
            pathMin = min(pathMin, matrix[i][j])
            if i == r-1 and j == c-1:
                self.re = max(self.re, pathMin)
                return
            dfs(i+1, j, pathMin)
            dfs(i, j+1, pathMin)

        dfs(0, 0, float('inf'))
        return self.re
```
### Count Number of substrings with exactly k distinct characters 
https://www.geeksforgeeks.org/count-number-of-substrings-with-exactly-k-distinct-characters/
```python
def countkDist(str1, k):
    # Consider all substrings between str[i..j] 
    res = 0
    for i in xrange(len(str1)):
        count = 0
        dic = {}
        for j in xrange(i, len(str1)):
            c = str1[j]
            if c not in dic:
                count += 1
                dic[c] = 1
            else:
                dic[c] += 1
            if count == k:
                res += 1
            elif count > k:
                break
    return res
```
### Two sum closest diff
http://www.noteanddata.com/Amazon-OA-2-sum-closest.html  
```python
def twoSumClosestDiff(arr, target):
    arr.sort()
    res = float('inf')
    l, r = 0, len(arr) - 1
    while l < r:
        s = arr[l] + arr[r]
        res = min(res, abs(s-target))
        if s < target:
            l += 1
        elif s > target:
            r -= 1
        else:
            return 0
    return res
```
### Two Sum Closest
Given two sorted arrays and a number x, ﬁnd the pair whose sum is closest to x and << x and the pair has an element from each array. We are given two arrays ar1[0…m-1] and ar2[0..n-1] and a number x, we need to ﬁnd the pair ar1[i] + ar2[j] such that absolute value of (ar1[i] + ar2[j] – x) is minimum  
```
Input:  ar1[] = {1, 4, 5, 7};        ar2[] = {10, 20, 30, 40};        x = 32       Output:  1 and 30
 
Input:  ar1[] = {1, 4, 5, 7};        ar2[] = {10, 20, 30, 40};        x = 50       Output:  7 and 40
```
```python
def closesTwoSum(arr1, arr2, x):
    arr1.sort()
    arr2.sort()
    n1, n2 = len(arr1), len(arr2)
    p1, p2 = 0, n2-1
    minDiff = float('inf')
    res = [float('inf'), float('inf')]
    while p1 < n1 and p2 >= 0:
        curDiff = x - arr1[p1] - arr2[p2]
        if 0 < curDiff < minDiff:
            minDiff = curDiff
            res = [arr1[p1], arr2[p2]]
        if curDiff > 0:
            p1 += 1
        else:
            p2 -= 1
    return res
```
### Subtree with Maximum Average
Description Given a binary tree, ﬁnd the subtree with maximum average. Return the root of the subtree. Example Given a binary tree: 1 / \ -5 11 / \ / \ 1 2 4 -2 return the node 11. Your problem can be diﬀerent in ways like -- it may not be a binary tree or the average doesn't include the root of the substree.  
https://blog.csdn.net/sinat_32547403/article/details/77824104  
```
class Solution:
    def findSubtree2(self, root):
        if not root:
            return
        self.avg, self.node = float('inf'), None

    def helper(self, root):
        if not root: return 0, 0
        sumLeft, countLeft = self.helper(root.left)
        sumRight, countRight = self.helper(root.right)
        sumRoot = sumLeft + sumRight + root.val
        countRoot = countLeft + countLeft + 1
        avg = sumRoot * 1.0 / countRoot
        if avg > self.avg:
            self.avg = avg
            self.node = root
        return sumRoot, countRoot
```
变形：
Maximum Subtree of Average
就是给一棵多叉树，表示公司内部的上下级关系。每个节点表示一个员工，节点包含的成员是他工作了几个月(int)，以及一个下属数组(ArrayList)。目标就是找到一棵子树，满足：这棵子树所有节点的工作月数的平均数是所有子树中最大的。最后返回这棵子树的根节点。这题补充一点，返回的不能是叶子节点(因为叶子节点没有下属)，一定要是一个有子节点的节点。  
https://www.jianshu.com/p/3c1a6726651e  
```python

class Node:
    def __init__(self, val):
        self.val = val
        self.children = []
class Solution:
    def find(self, Node):
        self.avg = float('-inf')
        self.node = None
        self.dfs(root)
        return self.node

    def dfs(self, root):
        if not root: return 0, 0  # sum, count
        if not root.children:
            return root.val, 1
        sumRoot, countRoot = root.val, 1
        for node in root.children:
            sumChild, countChild = self.dfs(node)
            sumRoot += sumChild
            countRoot += countChild
        if countRoot > 1 and sumRoot * 1.0 / countRoot > self.avg:
            self.avg = sumRoot * 1.0 / countRoot
            self.node = root
        return sumRoot, countRoot
```

 
