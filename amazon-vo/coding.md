### two sum


### ID generate
```
get() -> 1
get() -> 2
get() -> 3
put(2)
get() -> 2
get() -> 4
put(3)
get() -> 3
get() -> 5
```
```python
import heapq
class Generate:
    def __init__(self):
        self.cur = 1
        self.buffer = []

    def get(self):
        if self.buffer and self.buffer[0] < self.cur:
            res = heapq.heappop(self.buffer)
        elif self.buffer and self.buffer[0] == self.cur:
            self.cur += 1
            res = heapq.heappop(self.buffer)
        else:
            res = self.cur
            self.cur += 1
        return res

    def put(self, id):
        heapq.heappush(self.buffer, id)
        return True
```

### 49. Group Anagrams
https://leetcode.com/problems/group-anagrams/description/
```python
class Solution(object):
    def groupAnagrams(self, strs):
        d = {}
        for s in strs:
            key = tuple(sorted(s))  # 注意这里有tuple
            d[key] = d.get(key, []) + [s]
        return d.values()
```

### 146. LRU Cache
https://blog.csdn.net/Sengo_GWU/article/details/82930179

### 124. Binary Tree Maximum Path Sum
https://leetcode.com/problems/binary-tree-maximum-path-sum/description/
```python
class Solution(object):
    def maxPathSum(self, root):
        # left max + right max + cur node
        self.res = float('-inf')
        def maxPath(root):
            if not root:
                return 0
            left = max(0, maxPath(root.left))
            right = max(0, maxPath(root.right))
            self.res = max(self.res, left+right+root.val)
            return max(left, right) + root.val  # 注意这里只能是 左边或者右边的path加当前节点
        maxPath(root)
        return self.res
```
### 112. Path Sum
https://leetcode.com/problems/path-sum/description/
```python
class Solution(object):
    def hasPathSum(self, root, sum):
        if not root: return False
        if not root.left and not root.right and sum == root.val:
            return True
        sum -= root.val
        return self.hasPathSum(root.left, sum) or self.hasPathSum(root.right, sum)
```

### 3 sum
https://leetcode.com/problems/3sum/ 
```python
class Solution(object):
    def threeSum(self, nums):
        nums.sort()
        res = []
        n = len(nums)
        for i in xrange(n):
            if i > 0 and nums[i] == nums[i-1]:
                continue
            j = i+1
            k = n-1
            while j < k:
                s = nums[i] + nums[j] + nums[k]
                if s > 0:
                    k -= 1
                    while 0 < k-1 and nums[k] == nums[k+1]:
                        k -= 1
                elif s < 0:
                    j += 1
                    while j+1 < n-1 and nums[j] == nums[j-1]:
                        j += 1
                else:
                    res.append([nums[i], nums[j], nums[k]])
                    j += 1
                    while j+1 < n-1 and nums[j] == nums[j-1]:
                        j += 1
                    k -= 1
                    while 0 < k-1 and nums[k] == nums[k+1]:
                        k -= 1
        return res
```
### 判断是不是2的N次方
* 一个数如果是2的n次方，那么这个数二进制中只有一位是1，其余是0
* 如果该数减1，则其二进制与上面的完全不同，
* 利用这点，如果n是2的n次方，那么n&(n-1)必为0
```python
def isPower2(n):
    if n < 1: return False
    return (n-1) & n == 0
```
* 利用位移，从1开始，每次位移一位，看会不会等于这个数
```python
def isPower(n):
    if n < 1: return False
    i = 1
    while i <= n:
        if i == n:
            return True
        i <<= 1
    return False
```

### Longest repeating substing
https://www.geeksforgeeks.org/longest-repeating-and-non-overlapping-substring/  
e.g.  
abcab -> string   
12345 -> index   
dp[i][j]记录的是character string[i-1]=string[j-1]的时候，end为i或者为j的最长的重复子串的长度。
对于重复的a在index1, 4: dp[1][4] = dp[0][0]+1   
对于重复的b在index2, 5: dp[2][5] = dp[1][4]+1 
下面是non-overlap的
```python
def longestRepeatedSubstring(s):
    n = len(s)
    dp = [[0] * (n+1) for _ in xrange(n+1)]
    res = ''
    res_length = 0
    index = 0
    for i in xrange(1, n+1):
        for j in xrange(i, n+1):
            # dp[i-1][j-1] < j-i to remove overlapping
            if s[i-1] == s[j-1] and dp[i-1][j-1] < j-i:
                dp[i][j] = dp[i-1][j-1] + 1
                if dp[i][j] > res_length:
                    res_length = dp[i][j]
                    index = max(i, index)
            else:
                dp[i][j] = 0
    if res_length:
        for i in xrange(index-res_length+1, index+1):
            res += s[i-1]
    return res
```
看到亚麻别人VO要求banana要求返回ana是Overlap的上面代码稍微修改下：
```python
def longestRepeatedSubstring(s):
    n = len(s)
    dp = [[0] * (n+1) for _ in xrange(n+1)]
    res = ''
    res_length = 0
    index = 0
    for i in xrange(1, n+1):
        for j in xrange(i+1, n+1):
            # dp[i-1][j-1] < j-i to remove overlapping
            if s[i-1] == s[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
                if dp[i][j] > res_length:
                    res_length = dp[i][j]
                    index = max(i, index)
            else:
                dp[i][j] = 0
    if res_length:
        for i in xrange(index-res_length+1, index+1):
            res += s[i-1]
    return res
```
### 98. Validate Binary Search Tree
https://leetcode.com/problems/validate-binary-search-tree/description/
```python
class Solution(object):
    def isValidBST(self, root, largerThan=float('-inf'), smallerThan=float('inf')):
        if not root:
            return True
        if root.val >= smallerThan or root.val <= largerThan:
            return False
        return self.isValidBST(root.left, largerThan, min(smallerThan, root.val)) and self.isValidBST(root.right, max(largerThan, root.val), smallerThan)
```

### 23. Merge k Sorted Lists
https://leetcode.com/problems/merge-k-sorted-lists/description/
```python
class Solution(object):
    def mergeKLists(self, lists):
        dummy = head = ListNode(-1)
        h = []
        for node in lists:
            if not node: continue
            h.append([node.val, node])
        heapq.heapify(h) 
        while h:
            v, n = heapq.heappop(h)
            head.next = ListNode(v)
            head = head.next
            if n.next:
                heapq.heappush(h, [n.next.val, n.next])
        return dummy.next
```

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
```python
class Solution(object):
    def findMinHeightTrees(self, n, edges):
       
        if n == 1: return [0]
        neighbors = collections.defaultdict(list)
        degress = collections.defaultdict(int)
        
        for u,v in edges:
            neighbors[u].append(v)
            neighbors[v].append(u)
            degress[u] += 1
            degress[v] += 1
        
        level = []
        for i in xrange(n):  # 找到入度为1的
            if degress[i] == 1:
                level.append(i)
        unvisited = set(range(n))
        while len(unvisited) > 2:  # 这里是unvisited >2 不是len(level)
            nextLevel = []
            for u in level:
                unvisited.remove(u)
                for neighbor in neighbors[u]:
                    if neighbor in unvisited:
                        degress[neighbor] -= 1
                        if degress[neighbor] == 1:
                            nextLevel.append(neighbor)
            level = nextLevel
        return level
```
### 189. Rotate Array
https://leetcode.com/problems/rotate-array/description/
1. reverse the first n - k elements  
2. reverse the rest of them  
3. reverse the entire array  
```python
class Solution(object):
    def rotate(self, nums, k):
        # O(n) in time, O(1) in space
        if not k or k <= 0: return 
        k, end = k % len(nums), len(nums) - 1
        self.reverse(0, end-k, nums)
        self.reverse(end-k+1, end, nums)  # end-k+1 不是 k+1
        self.reverse(0, end, nums)
    
    def reverse(self, start, end, nums):
        while start < end:
            nums[start], nums[end] = nums[end], nums[start]
            start += 1
            end -= 1
```
### 459. Repeated Substring Pattern
https://leetcode.com/problems/repeated-substring-pattern/description/  
Basic idea:  

- First char of input string is first char of repeated substring  
- Last char of input string is last char of repeated substring  
- Let S1 = S + S (where S in input string)
- Remove 1 and last char of S1. Let this be S2
- If S exists in S2 then return true else false 
- Let i be index in S2 where S starts then repeated substring length i + 1 and repeated substring S[0: i+1]
```python
def repeatedSubstringPattern(self, str):
        if not s: return False
        s1 = s + s
        s2 = s1[1:-1]
        return s2.find(s) != -1
```
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
除了下面这种在原来数组操作的，牺牲空间的话，可以用数组记录color出现的数次，或者bucket sort
```python
class Solution:
    def sortColor(self, colors, k):
        # sort colors from 1 to k  O(nlogk) 为啥不是nlogn?
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
### 496. Next Greater Element I
https://leetcode.com/problems/next-greater-element-i/description/ 
常规解： O(n^2)
```python
class Solution(object):
    def nextGreaterElement(self, nums1, nums2):
        d = {}     
        for i,num1 in enumerate(nums2):
            for num2 in nums2[i+1:]:
                 if num1 < num2:
                    d[num1] = num2
                    break
        return [d.get(num1,-1) for num1 in nums1]
```
用Stack O（n） ， stack 部分 O(1)
```python
        st, d = [], {}  # stack
        for n in nums:
            while st and st[-1] < n:  # At max it can go up to 2*i operations for any given i. But overall it is not n^2
                d[st.pop()] = n
            st.append(n)
        
        return [d.get(x, -1) for x in findNums]
```

### 415. Add Strings 
https://leetcode.com/problems/add-strings/description/
```python
class Solution(object):
    def addStrings(self, num1, num2):
        num1, num2 = list(num1), list(num2)
        res = []
        carry = 0
        while len(num1) or len(num2) or carry:
            a = ord(num1.pop()) - ord('0') if num1 else 0
            b = ord(num2.pop()) - ord('0') if num2 else 0
            total = a + b + carry
            carry = total / 10
            res = [total % 10] + res
        return ''.join(str(c) for c in res)
```
