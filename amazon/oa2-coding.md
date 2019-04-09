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
