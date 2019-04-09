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
