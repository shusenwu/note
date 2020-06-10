[105. Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
https://leetcode.com/submissions/detail/351109154/
```python
class Solution(object):
    def buildTree(self, preorder, inorder):
        """
        :type preorder: List[int]
        :type inorder: List[int]
        :rtype: TreeNode
        The basic idea is here:
Say we have 2 arrays, PRE and IN.
Preorder traversing implies that PRE[0] is the root node.
Then we can find this PRE[0] in IN, say it's IN[5].
Now we know that IN[5] is root, so we know that IN[0] - IN[4] is on the left side, IN[6] to the end is on the right side.
Recursively doing this on subarrays, we can build a tree out of it :)
        """
   
        if inorder:
            ind = inorder.index(preorder.pop(0))  # find the index of root node
            root = TreeNode(inorder[ind])
            root.left = self.buildTree(preorder, inorder[0: ind])
            root.right = self.buildTree(preorder, inorder[ind+1:])
            
            return root
```

[253. Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/)
```python

# Definition for an interval.
# class Interval(object):
#     def __init__(self, s=0, e=0):
#         self.start = s
#         self.end = e
 
 # Very similar with what we do in real life. Whenever you want to start a meeting, 
 # you go and check if any empty room available (available > 0) and
 # if so take one of them ( available -=1 ). Otherwise,
 # you need to find a new room someplace else ( numRooms += 1 ).  
 # After you finish the meeting, the room becomes available again ( available += 1 ).
    
class Solution(object):
    def minMeetingRooms(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: int
        """
        start, end = [], []
        for inter in intervals:
            start.append(inter.start)
            end.append(inter.end)
        
        start.sort()
        end.sort()
        
        index_s = index_e = 0
        available = num_rom = 0 
        while index_s < len(start):
            if start[index_s] < end[index_e]:
                if available > 0:
                    available -= 1
                else:
                    num_rom += 1
                
                index_s += 1
            else:
                available += 1
                index_e += 1

```


https://leetcode.com/problems/binary-tree-maximum-path-sum/discuss/39775/Accepted-short-solution-in-Java
改成多儿子树， 思路一样的
```python
import heapq


class TreeNode(object):
    def __init__(self, val):
        self.val = val
        self.children = []


class Solution(object):
    def maxPathSum(self, root):
        self.res = float('-inf')
        self.maxPathSumIncludeCurNode(root)
        return self.res

    def maxPathSumIncludeCurNode(self, node):
        if not node:
            return 0
        heap = []
        for child in node.children:
            childMaxSum = self.maxPathSumIncludeCurNode(child)
            heapq.heappush(heap, -childMaxSum)

        maxChild = max(0, - heapq.heappop(heap))
        secondMaxChild = max(0, - heapq.heappop(heap))
        self.res = max(self.res, node.val + maxChild + secondMaxChild)

        return node.val + maxChild
 ```
 
 [394. Decode String](https://leetcode.com/problems/decode-string/)
```python
class Solution(object):
    def decodeString(self, s):
        """
        :type s: str
        :rtype: str
        """
        stack = [["", 1]]
        num = ""
        for ch in s:
            if ch.isdigit():
                num += ch
            elif ch == '[':
                stack.append(['', int(num)])
                num = ''
            elif ch == ']':
                stri, k = stack.pop()
                stack[-1][0] += stri*k
            else:
                stack[-1][0] += ch
        return stack[0][0]
 ```
 or recrsive []里面的东西得到的结果给上一层
 ```JAVA
 class Solution {
    public String decodeString(String s) {
        Deque<Character> queue = new LinkedList<>();
        for (char c : s.toCharArray()) queue.offer(c);
        return helper(queue);
    }
    
    public String helper(Deque<Character> queue) {
        StringBuilder sb = new StringBuilder();
        int num = 0;
        while (!queue.isEmpty()) {
            char c= queue.poll();
            if (Character.isDigit(c)) {
                num = num * 10 + c - '0';
            } else if (c == '[') {
                String sub = helper(queue);  // recursion 
                for (int i = 0; i < num; i++) sb.append(sub);   
                num = 0;
            } else if (c == ']') {
                break;
            } else {
                sb.append(c);
            }
        }
        return sb.toString();
    }
}
```
[200. Number of Islands](https://leetcode.com/problems/number-of-islands/)
[98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)
https://leetcode.com/submissions/detail/223142427/

[56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)

[1429. First Unique Number](https://leetcode.com/problems/first-unique-number/)

[209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)
```python
class Solution(object):
    def minSubArrayLen(self, k, nums):
        """
        :type s: int
        :type nums: List[int]
        :rtype: int
        """
        
        
        s = 0
        res = float('inf')
        left = 0
        for i in xrange(len(nums)):
            s += nums[i]
            
            while s >= k:  # Each element can be visited atmost twice, O(n)
                s -= nums[left]
                res = min(res, i-left+1)
                left += 1
                
        return res if res != float('inf') else 0
```
```java
O(NLogN) - search if a window of size k exists that satisfy the condition

public class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        int i = 1, j = nums.length, min = 0;
        while (i <= j) {    // O(log(n))
            int mid = (i + j) / 2;
            if (windowExist(mid, nums, s)) {  
                j = mid - 1;
                min = mid;
            } else i = mid + 1;
        }
        return min;
    }


    private boolean windowExist(int size, int[] nums, int s) {
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {  // O(N)
            if (i >= size) sum -= nums[i - size];
            sum += nums[i];
            if (sum >= s) return true;
        }
        return false;
    }
}
```

 
在一个N的西洋棋盘, 一个骑士走K步，有几种走法
参考https://leetcode.com/problems/knight-probability-in-chessboard/

```python3
class Solution(object):
    def knightSteps(self, N, i, j, k):  # N 的棋盘， 起始位置i,j， 走K步
        moves = ((-1, -2), (-2, -1), (-2, 1), (-1, 2), (1, 2), (2, 1), (2, -1), (1, -2))
        memo = {}  # 如果剩下K = 100的时候都走到同一个位置， 那么不需要重复计算剩下的走法

        def dfs(x, y, k):
            if k == 0:
                return 1
            sum_p = 0
            for dx, dy in moves:
                i, j = x + dx, y + dy
                if 0 <= i < N and 0 <= j < N:
                    sum_p += dfs(i, j, k-1)
            memo[(x, y, k)] = sum_p
            return sum_p

        return dfs(i, j, k)
```
