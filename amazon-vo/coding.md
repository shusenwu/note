### 停车场OOD
###  string是否是回文
### two sum
### reverse linked list  
### N个骰子，N面，求组合target
比如 2个色子，每个色子3面，target 4， 则有 {{1,3}, {2,2}} =2 种情况。1，3 和 3，1 是重复的
```python
def NSum(n, m, target):  # n个塞骰子， m面[1, 2, .. m]
    res = set()
    q = [[n, [], 0]]
    while q:
        steps, cur, Sum = q.pop(0)
        if steps == 0 and Sum == target:
            res.add(tuple(sorted(cur)))
        if steps > 0 and Sum < target:
            steps -= 1
            for i in xrange(1, target-Sum+1):
                q.append([steps, cur+[i], Sum+i])
    return [list(e) for e in res]
```
### 863. All Nodes Distance K in Binary Tree
https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/discuss/281224/Python-without-using-graph  
```python
class Solution(object):
    def distanceK(self, root, target, K):
        self.res = []
        self.findBelow(target, K)
        self.findAbove(root, target, K)
        return self.res
    
    def findBelow(self, node, disK):
        if not node or disK < 0:
            return
        
        if disK == 0:
            self.res.append(node.val)
        if node.left:
            self.findBelow(node.left, disK-1)
        if node.right:
            self.findBelow(node.right, disK-1)
        
    
    def findAbove(self, root, target, disK):
        if not root: return float('-inf')
        if root == target:
            return 0
        
        leftDis = self.findAbove(root.left, target, disK)  # left Node's distance to target
        rightDis = self.findAbove(root.right, target, disK)
        
        # 就在target上方的
        if disK in (leftDis+1, rightDis+1):
            self.res.append(root.val)
        
        curDis = float('-inf')
        if leftDis >= 0:  # the target will only appear on only on side
            curDis = leftDis+1  # cur node's distance to target
            self.findBelow(root.right, disK-curDis-1)
        elif rightDis >= 0:
            curDis = rightDis+1
            self.findBelow(root.left, disK-curDis-1)
        
        return curDis
```
### 472. Concatenated Words
https://leetcode.com/problems/concatenated-words/  
```python
class Solution(object):
    def findAllConcatenatedWordsInADict(self, words):
        words = set(words)
        res = []
        res2 = []
        for w in words:
            if not w: continue
            stack = [[0, []]]  # how far we can make up
            seen = {0}  # 注意是set
            while stack:
                cur, ws = stack.pop()
                if cur == len(w):
                    res.append(w)
                    res2.append(ws)
                    break  # 
                for far in xrange(cur+1, len(w)+1): 
                    if far not in seen and w[cur: far] in words and not (cur == 0 and far == len(w)):
                        stack.append([far, ws+[w[cur: far]]])
                        seen.add(far)
        return res
```
### 31. Next Permutation  
https://leetcode.com/problems/next-permutation/ 
### 114. Flatten Binary Tree to Linked List
https://leetcode.com/problems/flatten-binary-tree-to-linked-list/discuss/281072/Python-with-explain-idea-is-simple 
### 287. Find the Duplicate Number
```python
class Solution(object):
    def findDuplicate(self, nums):
        if len(nums) > 1:
            slow = nums[0]
            fast = nums[nums[0]]
            while slow != fast:
                slow = nums[slow]
                fast = nums[nums[fast]]
            
            fast = 0
            while slow != fast:
                slow = nums[slow]
                fast = nums[fast]
            return fast
        return -1
```
```python
        l, r = 1, len(nums) - 1
        while l < r:
            mid = (l+r) / 2
            count = 0
            for n in nums:
                if n <= mid:
                    count += 1
            if count > mid:
                r = mid
            else:
                l = mid + 1
        return l
```
### 472. Concatenated Words
```python
class Solution(object):
    def findAllConcatenatedWordsInADict(self, words):
        words = set(words)
        res = []
        res2 = []
        for w in words:
            if not w: continue
            stack = [[0, []]]  # how far we can make up
            seen = {0}  # 注意是set
            while stack:
                cur, ws = stack.pop()
                if cur == len(w):
                    res.append(w)
                    res2.append(ws)
                    break  # 
                for far in xrange(cur+1, len(w)+1): 
                    if far not in seen and w[cur: far] in words and not (cur == 0 and far == len(w)):
                        stack.append([far, ws+[w[cur: far]]])
                        seen.add(far)
        return res
```
### 41. First Missing Positive
```python
class Solution(object):
    def firstMissingPositive(self, nums):
        nums.append(0)  # because the missing positive interger will be in the range from [1, n+1]
        n = len(nums)
        for i in xrange(n):  # [7, 8, 9, 0] => [0, 0, 0, 0]
            if nums[i] < 0 or nums[i] >= n:  
                nums[i] = 0
        
        for i in xrange(n):  # use the index to store the frequence of the num
            nums[nums[i]%n] += n  # 这里要取余，因为之前可能被加了n

        for i in xrange(1, n):
            if nums[i] / n == 0:
                return i
        return n
```
### 103. Binary Tree Zigzag Level Order Traversal
```python
class Solution(object):
    def zigzagLevelOrder(self, root):
        if not root: return []
        level = [root]
        re = []
        flag = 1
        while level:
            Next = []
            temp = []
            while level:
                node = level.pop(0)
                temp.append(node.val)
                if node.left: Next.append(node.left)
                if node.right: Next.append(node.right)
            level = Next
            re.append(temp[::flag])
            flag *= -1
        return re
```
### 503. Next Greater Element II
https://leetcode.com/problems/next-greater-element-ii/  
circular:
```python
class Solution(object):
    def nextGreaterElements(self, nums):
        re = []
        length = len(nums)
        for i, n in enumerate(nums):
            for idx in xrange(i+1, length+i):
                idx = idx % length
                if nums[idx] > n:
                    re.append(nums[idx])
                    break
            else:
                re.append(-1)
        return re
```
无circular:
```python
def nextGreater(nums):
    # [1, 2, 1] -> [2, -1, -1]
    stack = []
    for i, n in enumerate(nums):
        while stack and n > stack[-1][1]:
            nums[stack[-1][0]] = n
            stack.pop()
        stack.append([i, n])
    while stack:
        idx, _ = stack.pop()
        nums[idx] = -1
    return nums
```
### 151. Reverse Words in a String
```python
class Solution(object):
    def reverseWords(self, s):
        s = s[::-1]
        word = words = ''
        for i, c in enumerate(s):
            if c != ' ' and word != '' and i > 0  and s[i-1] == ' ':
                words += word + ' '
                word = c
            elif c != ' ':
                word = c + word
        words += word
        return words
```

### 273. Integer to English Words
https://blog.csdn.net/Sengo_GWU/article/details/81989359 
### 794. Valid Tic-Tac-Toe State
https://leetcode.com/problems/valid-tic-tac-toe-state/submissions/  
```python
class Solution(object):
    def validTicTacToe(self, board):
        r, c = [0]*3, [0]*3
        dia, anti_dia = 0, 0
        count = 0
        for i in xrange(3):
            for j in xrange(3):
                offset = 0
                if board[i][j] == 'X':
                    offset = 1
                    count += 1
                elif board[i][j] == 'O':
                    offset = -1
                    count -= 1
                r[i] += offset
                c[j] += offset
                if i == j:
                    dia += offset
                if i + j == 2:
                    anti_dia += offset
        if 3 in (r+c+[dia]+[anti_dia]) and (-3 in (r+c+[dia]+[anti_dia]) or count != 1):
            return False
        
        if count < 0 or count > 1:
            return False
        
        if -3 in (r+c+[dia]+[anti_dia]) and count != 0:
            return False
        return True
```
### binary tree top view
```python
def topView(root):
    if not root:
        return
    q = [(root, 0)]
    seen = {}
    re = []
    while q:
        node, pos = q.pop(0)
        if pos not in seen:
            seen[pos] = node.val
        if node.left:
            q.append((node.left, pos-1))
        if node.right:
            q.append((node.right, pos+1))
    for key in sorted(seen.keys()):
        re.append(seen[key])
    return re
```
### 162. Find Peak Element
https://leetcode.com/problems/find-peak-element/
```python
class Solution(object):
    def findPeakElement(self, nums):
        left = 0
        right = len(nums) - 1
        while left < right:
            mid = (left+right) / 2
            if nums[mid] < nums[mid+1]:
                left = mid + 1
            else:
                right = mid
                
        return left  
```
### find duplicate
nums = [1, 1, 2, 3, 4, 5, 6, 7] 
连续的排序数组里面有一个duplicate
```python
def findDuplicate(nums):
    l, r = 0, len(nums)-1
    while l < r:
        mid = (l + r) / 2
        if nums[mid] == nums[l] + mid:
            l = mid + 1
        else:
            r = mid
    return nums[l]
```
### 380. Insert Delete GetRandom O(1)
https://leetcode.com/problems/insert-delete-getrandom-o1/
```python
class RandomizedSet(object):
    def __init__(self):
        self.nums, self.pos = [], {}
        
    def insert(self, val):
        if val not in self.pos:
            self.nums.append(val)
            self.pos[val] = len(self.nums) - 1
            return True
        return False
        

    def remove(self, val):
        if val in self.pos:
            idx, last = self.pos[val], self.nums[-1]
            self.nums[idx], self.pos[last] = last, idx
            self.nums.pop(); self.pos.pop(val, 0)
            return True
        return False
            
    def getRandom(self):
        return self.nums[random.randint(0, len(self.nums) - 1)]
```


### Convert a Binary Tree to Threaded binary tree
https://www.geeksforgeeks.org/convert-binary-tree-threaded-binary-tree-set-2-efficient/
```python
class Node:
    def __init__(self, val):
        self.val = val
        self.left = self.right = None
        self.isThreaded = False

def createThreaded(root):
    # Base cases: Tree is empty or has single node
    if not root: return None
    if not root.left and not root.right:
        return root
    # find predecessor
    if root.left:
        l = createThreaded(root.left)  # Find predecessor of root (Rightmost
        l.right = root  # Link a thread from predecessor
        l.isThreaded = True
    if not root.right:
        return root
    return createThreaded(root.right)
```

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
