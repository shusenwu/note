### Binary Tree Path Sum
  题目是node val 只有0 1 的binary tree， 从root 到 leaf 是一个path，可以对应一个十进制的数字，然后求出sum
  ```
                       0
                    /     \
                   1       0
                 /    \    / \
                1     1  1   0
 ```
       011 -> 3       011 -> 3   001-> 1  000 -> 0    sum = 3+3+1+0 = 7
 ```python
 class Sollution:
    def binarySum(self, root):
        return self.pathSum(root, 0)

    def pathSum(self, root, val):  # preorder traversal
        if not root:
            return 0
        val = val * 2 + root.val  # 10进制的path sum就 x10
        if not root.left and not root.right:
            return val
        return self.pathSum(root.left, val) + self.pathSum(root.right, val)
```
### 269. Alien Dictionary
https://blog.csdn.net/Sengo_GWU/article/details/81966972
```python
class Solution(object):
    def alienOrder(self, words):
        self.graph = collections.defaultdict(list)
        self.visited = collections.defaultdict(int)
        self.res = ''

        for i, w1 in enumerate(words[:-1]):
            w2 = words[i+1]
            for c1, c2 in zip(w1, w2):
                if c1 == c2:
                    continue
                self.graph[c2].append(c1)
                break
        nodes = {c:0 for w in words for c in w}
        for node in nodes.keys():
            if not self.dfs(node):
                return ''
        return self.res
        
    
    def dfs(self, node):
        if self.visited[node] == -1:  # visiting
            return False
        if self.visited[node] == 1: # visited:
            return True
        self.visited[node] = -1
        for n in self.graph[node]:
            if not self.dfs(n):
                return False
        
        self.visited[node] = 1
        self.res += node
        return True
```
### 348. Design Tic-Tac-Toe
```python
class TicTacToe(object):
    def __init__(self, n):
        self.row, self.col = [0] * n, [0]*n
        self.diag = self.anti_diag = 0
        self.n = n
        
    def move(self, row, col, player):
        offset = 1 if player == 1 else -1
        if row == col:
            self.diag += offset
        if row + col == self.n - 1:
            self.anti_diag += offset
        self.row[row] += offset
        self.col[col] += offset
        if self.n in (self.row[row], self.col[col], self.diag, self.anti_diag):
            return 1
        if -self.n in (self.row[row], self.col[col], self.diag, self.anti_diag):
            return 2
        return 0
      
### 164. Maximum Gap
https://leetcode.com/problems/maximum-gap/description/ 
下面这种直接bucket sort的 testcase [1,10000000] 超时
```python
class Solution(object):
    def maximumGap(self, num):
        if len(num) < 2 or min(num) == max(num):
            return 0
        b, a = max(num), min(num)
        bucket = [[] for _ in range((b-a)+1)]
        for n in num:
            bucket[n-a] = n
        bucket = [b for b in bucket if b]
        return max(bucket[i]-bucket[i-1] for i in range(1, len(bucket)))
```
改进:
```python
class Solution(object):
    def maximumGap(self, num):
        if len(num) < 2 or min(num) == max(num):
            return 0
        a, b = min(num), max(num)
        size = (b-a)//(len(num)-1) or 1  # 一个bucket可以装多少个
        bucket = [[None, None] for _ in range((b-a)//size+1)]  # 需要几个bucket = 总的数/一个bucket的容量 
        for n in num:
            b = bucket[(n-a)//size]
            b[0] = n if b[0] is None else min(b[0], n)
            b[1] = n if b[1] is None else max(b[1], n)
        bucket = [b for b in bucket if b[0] is not None]
        return max(bucket[i][0]-bucket[i-1][1] for i in range(1, len(bucket)))
  ```
### 310. Minimum Height Trees
https://leetcode.com/problems/minimum-height-trees/description/
### 189. Rotate Array
https://leetcode.com/problems/rotate-array/description/
### 459. Repeated Substring Pattern
https://leetcode.com/problems/repeated-substring-pattern/description/
### sort colors 
```python
class Solution(object):
    def sortColors(self, nums):
        left = cur = 0
        right = len(nums) - 1
        while cur <= right:
            if nums[cur] == 0:
                nums[left], nums[cur] = nums[cur], nums[left]
                left += 1
                cur += 1
            elif nums[cur] == 1:
                cur += 1
            else:
                nums[cur], nums[right] = nums[right], nums[cur]
                right -= 1
```
### Sort colors II
https://www.jiuzhang.com/solution/sort-colors-ii/ 
```python
class Solution:
    def sortColor(self, colors, k):
        # sort colors from 1 to k  O(nlogk)
        if not colors: return []
        self.rainBowSort(colors, 0, len(colors)-1, 1, k)
        return colors

    def rainBowSort(self, colors, left, right, colorFrom, colorTo):
        if colorFrom == colorTo: return
        if left >= right: return
        colorMid = (colorFrom + colorTo) / 2
        l, r = left, right
        while l <= r:  # left part <= mid  right part > mid
            while l <= r and colors[l] <= colorMid:
                l += 1
            while l <= r and colors[r] > colorMid:
                r -= 1
            if l <= r:
                colors[l], colors[r] = colors[r], colors[l]
                l += 1
                r -= 1
        self.rainBowSort(colors, left, r, colorFrom, colorMid)
        self.rainBowSort(colors, l, right, colorMid+1, colorTo)
```
