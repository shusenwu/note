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
