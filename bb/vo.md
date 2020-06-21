[329. Longest Increasing Path in a Matrix](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/)  

[301. Remove Invalid Parentheses](https://leetcode.com/problems/remove-invalid-parentheses/)  

[934. Shortest Bridge](https://leetcode.com/problems/shortest-bridge/)  
```python
class Solution:
    def shortestBridge(self, A):
        '''
        dea is straightforward.
        We get root of first island from "first" function
        We dfs root and add indexes to bfs
        We bfs and expand the first island in other words
        Finally return step number when facing other island
        Note: This can also be done with referenced array if you don't want to modify A.
        '''
        def dfs(i, j):
            A[i][j] = -1
            bfs.append((i, j))
            for x, y in ((i - 1, j), (i + 1, j), (i, j - 1), (i, j + 1)):
                if 0 <= x < n and 0 <= y < n and A[x][y] == 1:
                    dfs(x, y)
        def first():
            for i in range(n):
                for j in range(n):
                    if A[i][j]:
                        return i, j
        n, step, bfs = len(A), 0, []
        dfs(*first())
        while bfs:
            new = []
            for i, j in bfs:
                for x, y in ((i - 1, j), (i + 1, j), (i, j - 1), (i, j + 1)):
                    if 0 <= x < n and 0 <= y < n:
                        if A[x][y] == 1:
                            return step
                        elif not A[x][y]:
                            A[x][y] = -1
                            new.append((x, y))
            step += 1
            bfs = new
```
[621. Task Scheduler](https://leetcode.com/problems/task-scheduler/)  
```python
class Solution(object):
    def leastInterval(self, tasks, n):
        """
        :type tasks: List[str]
        :type n: int
        :rtype: int
        https://leetcode.com/problems/task-scheduler/discuss/104500/Java-O(n)-time-O(1)-space-1-pass-no-sorting-solution-with-detailed-explanation
        """
        counter = collections.Counter(tasks)
        task_list = [[value, key] for key, value in counter.items()]
        task_list.sort(reverse=True)
        most = task_list[0][0]
        sameLength = sum([1 for value, key in task_list if value == most])
        return max((most-1) * (n+1) + sameLength, len(tasks))
        
```  
[63. Unique Paths II](https://leetcode.com/problems/unique-paths-ii/)   
```python
class Solution(object):
    def uniquePathsWithObstacles(self, O):
        """
        :type obstacleGrid: List[List[int]]
        :rtype: int
        """
        if not O: return 0
        r, c = len(O), len(O[0])
        
        for i in range(r):
            for j in range(c):
                if O[i][j] == 1:
                    O[i][j] = 0
                elif i == 0 and j == 0:
                    O[i][j] = 1
                elif i == 0:
                    O[i][j] = O[i][j-1] * 1  # For row 0, if there are no paths to left cell, then its 0,else 1
                elif j == 0:
                    O[i][j] = O[i-1][j] * 1   # For col 0, if there are no paths to upper cell, then its 0,else 1
                else:
                    O[i][j] = O[i-1][j] + O[i][j-1]
 
        return O[r-1][c-1]
``` 
[426. Convert Binary Search Tree to Sorted Doubly Linked List](https://blog.csdn.net/Sengo_GWU/article/details/81879502)   
[81. Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)  
```python
class Solution(object):
    def search(self, nums, target):
        if not nums:
            return False
        l, r = 0, len(nums)-1
        while l < r:
            mid = l + (r-l)//2
            if nums[mid] == target:
                return True
             # the right half is ordered
            if nums[mid] < nums[r]:
                # target is in right half
                if nums[mid] < target <= nums[r]:
                    l = mid + 1
                else:
                    r = mid - 1
            #  # the left half is ordered
            elif nums[mid] > nums[r]:
                # target is in the left half
                if nums[l] <= target < nums[mid]:
                    r = mid - 1
                else:
                    l = mid + 1
            else:  # we don't know which part is ordered, e.g, mid=0 right=0 [2 5 6 0 0 1 2] or [1 2 0 0 2 5 6]
                r -= 1
        return nums[l] == target
```


[Find the repeating and the missing](https://www.geeksforgeeks.org/find-a-repeating-and-a-missing-number/) 
idea:    
1. 假设x,y是repeating 和 missing的数字，得到x, y的xor 
```
res = arr[0]^arr[1]^arr[2].....arr[n-1]
res = res^1^2^3^......^n
```   
2. 我们知道xor异或是不相等的位为1，所以我们找上一步res中的任意一位1的位，在这一位x,y是不相同的。  
3. 通过set_bit = res ^ ~(res-1)取最右侧非零的位，其他位都会变成0。通过此bit来区分x,y
4. 把所有number 分为2个集合，此bit 为1的为一个集合，此bit为0的为一个集合。
5.  异或2个集合，
```        
           for (i = 0; i < n; i++) { 
            if ((arr[i] & set_bit_no) != 0) 
                /* arr[i] belongs to first set */
                x = x ^ arr[i]; 
  
            else
                /* arr[i] belongs to second set*/
                y = y ^ arr[i]; 
        }
```
6. 再异或一次1~n ，加上5的异或，出现1次的num 会被异或2次抵消掉。 剩下x,y分别  
```
       for (i = 1; i <= n; i++) { 
            if ((i & set_bit_no) != 0) 
                /* i belongs to first set */
                x = x ^ i; 
  
            else
                /* i belongs to second set*/
                y = y ^ i; 
        } 
```
```JAVA
import java.io.*; 
  
class GFG { 
    static int x, y; 
  
    static void getTwoElements(int arr[], int n) 
    { 
        /* Will hold xor of all elements 
       and numbers from 1 to n  */
        int xor1; 
  
        /* Will have only single set bit of xor1 */
        int set_bit_no; 
  
        int i; 
        x = 0; 
        y = 0; 
  
        xor1 = arr[0]; 
  
        /* Get the xor of all array elements  */
        for (i = 1; i < n; i++) 
            xor1 = xor1 ^ arr[i]; 
  
        /* XOR the previous result with numbers from  
       1 to n*/
        for (i = 1; i <= n; i++) 
            xor1 = xor1 ^ i; 
  
        /* Get the rightmost set bit in set_bit_no */
        set_bit_no = xor1 & ~(xor1 - 1); 
  
        /* Now divide elements into two sets by comparing 
    rightmost set bit of xor1 with the bit at the same  
    position in each element. Also, get XORs of two 
    sets. The two XORs are the output elements. The  
    following two for loops serve the purpose */
        for (i = 0; i < n; i++) { 
            if ((arr[i] & set_bit_no) != 0) 
                /* arr[i] belongs to first set */
                x = x ^ arr[i]; 
  
            else
                /* arr[i] belongs to second set*/
                y = y ^ arr[i]; 
        } 
        for (i = 1; i <= n; i++) { 
            if ((i & set_bit_no) != 0) 
                /* i belongs to first set */
                x = x ^ i; 
  
            else
                /* i belongs to second set*/
                y = y ^ i; 
        } 
  
        /* *x and *y hold the desired output elements */
    } 
    /* Driver program to test above function */
    public static void main(String[] args) 
    { 
        int arr[] = { 1, 3, 4, 5, 1, 6, 2 }; 
  
        int n = arr.length; 
        getTwoElements(arr, n); 
        System.out.println(" The missing element is  "
                           + x + "and the "
                           + "repeating number is "
                           + y); 
    } 
} 
  
// This code is contributed by Gitanjali. 
```



[ Kth Missing Element In Sorted Array](https://strstr.io/Leetcode1060-Missing-Element-in-Sorted-Array/)    

[160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)  

[438. Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)   

[703. Kth Largest Element in a Stream](https://leetcode.com/submissions/detail/189780304/)    

[611. Valid Triangle Number](https://leetcode.com/problems/valid-triangle-number/)  
  
[1244. Design A Leaderboard](https://leetcode.com/problems/design-a-leaderboard/)   

[https://leetcode.com/problems/island-perimeter/](https://leetcode.com/problems/island-perimeter/)   

[797. All Paths From Source to Target](https://leetcode.com/problems/all-paths-from-source-to-target/)  
  
[1209. Remove All Adjacent Duplicates in String II](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/)   
https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/discuss/393149/JavaPython-3-O(n)-codes-using-Stack-w-brief-explanation-and-analysis.
  
[Josephus problem](https://www.geeksforgeeks.org/josephus-problem-set-1-a-on-solution/)  
  
[99. Recover Binary Search Tree](https://leetcode.com/problems/recover-binary-search-tree/)     

[面试题 16.10. 生存人数living-people-lcci](https://leetcode-cn.com/problems/living-people-lcci/)
```java
class Solution {
    public int maxAliveYear(int[] birth, int[] death) {
        int[] count = new int[102];
        for (int j = 0; j < birth.length; j++) {
            count[birth[j] - 1900] += 1;
            count[death[j] - 1899] -= 1;
        }
        int maxIndex = 0;
        int maxCount = -1;
        for (int i = 1; i < 102; i++) {
            count[i] = count[i] + count[i - 1];
            if (count[i] > maxCount) {
                maxCount = count[i];
                maxIndex = i;
            }
        }
        return maxIndex + 1900;
    }
}
```

[Stable Marriage Problem](https://www.geeksforgeeks.org/stable-marriage-problem/)   
[8. String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)  
[445. Add Two Numbers II](https://leetcode.com/problems/add-two-numbers-ii/)    

[422. Valid Word Square](https://leetcode.com/problems/valid-word-square/)   
1. 晚了10分钟，只做了一题。外星人字典变种。    
输入：给一个字典如 a, b, c, d, ch, dd, e, r ..., 一个word list 如 ddr, dea, ab, chc    
思路 第一步： 269. Alien Dictionary https://blog.csdn.net/Sengo_GWU/article/details/81966972   拓扑排序输出各个字母的顺序  
第二部： 比如字母的顺序是【d, e, g ...】给他们一个数字顺序【1， 2， 3】.  
第三部： 把word list的里面的word 根据第二步的结果转化为数字比如 112 223之类的  
第四部，排序  

重点是字典里的"字母"可能是长度为2的
输出：sorted word list： ab, dea, chc, ddr
解法：自己设计输入的数据结构。字典可以为<string, int> map。把word拆成int tuple，然后sort tuple。不难，一开始很容易想复杂了。

[在浏览器输入 URL 回车之后发生了什么](https://juejin.im/post/5d5e795ff265da03e275f29e)  

[365. Water and Jug Problem](https://leetcode.com/problems/water-and-jug-problem/)倒水问题    

[Find minimum number of coins that make a given value](https://www.geeksforgeeks.org/find-minimum-number-of-coins-that-make-a-change/)  
```python

'''
If T == 0, then 0 coins required.
If T > 0
   minCoins(coins[0..m-1], T) = min {1 + minCoins(T-coin[i])} 
                               where i varies from 0 to m-1 
                               and coin[i] <= T
'''
def minCoinToTarget(coins, T):
    if T == 0:
        return 0

    res = float('inf')
    for i in range(len(coins)):
        if coins[i] <= T:
            pre_counts = minCoinToTarget(coins, T-coins[i])
            if pre_counts != float('inf'):  # find the min one
                res = min(res, pre_counts + 1)

    return res if res != float('inf') else -1

coins = [9, 6, 5, 1]
print(minCoinToTarget(coins, 11))

'''
dp
'''

def minCoins(coins, T):
    dp = [0 for _ in range(T + 1)]

    dp[0] = 0  # base case when T = 0

    for i in range(1, T+1):
        dp[i] = float('inf')

    # Compute minimum coins required
    # for all values from 1 to V
    for t in range(1, T+1):
        for i in range(len(coins)):
            if coins[i] <= t:
                pre_count = dp[t-coins[i]]
                if pre_count != float('inf'):
                    dp[t] = min(dp[t], pre_count+1)

    return dp[-1]


coins = [9, 6, 5, 1]
print(minCoins(coins, 11))
```

[121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)  
[297. Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)  
[128. Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)   
Given an unsorted array of integers, find the length of the longest consecutive elements sequence.   

[1123. Lowest Common Ancestor of Deepest Leaves](https://leetcode.com/problems/lowest-common-ancestor-of-deepest-leaves/discuss/334577/JavaC%2B%2BPython-Two-Recursive-Solution)    
  
[694. Number of Distinct Islands](https://leetcode.com/problems/number-of-distinct-islands/)  
```python

class Solution(object):
    def numDistinctIslands(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        
        def dfs(i, j, shape, dirc):
            if i < 0 or i >= len(grid) or j < 0 or j >= len(grid[0]) or grid[i][j] != 1:
                return
            grid[i][j] = 0
            shape.append(dirc)
            dfs(i-1, j, shape, 'u')
            dfs(i+1, j, shape, 'd')
            dfs(i, j-1, shape, 'l')
            dfs(i, j+1, shape, 'r')
            shape.append('b')  # back  没有back 就失败了
            return shape
        
        re = set()
        for i in xrange(len(grid)):
            for j in xrange(len(grid[0])):
                if grid[i][j]:
                    shape = dfs(i, j, [], 'o')
                    re.add(''.join(shape))
       
        return len(re)
 ```

1。design 一个超市的purchase record。因为没准备这种类型问题，一开始有点发懵，加上一上来俩硬度人有点虚就慌了一下。但后来通过交流知道要干什么了也design出来了。

[117. Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/)  
[116. Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)  


[314. Binary Tree Vertical Order Traversal](https://leetcode.com/problems/binary-tree-vertical-order-traversal/)  
[987. Vertical Order Traversal of a Binary Tree](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/)  

[320. Generalized Abbreviation](https://leetcode.com/problems/generalized-abbreviation/)  
```
Input: "word"
Output:
["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]
```
```python
class Solution:
    def generateAbbreviations(self, word: str) -> List[str]:
        self.res = []
        self.helper(0, '', 0, word)
        return self.res
    
    def helper(self, pos, cur_s, count, word):
            if pos == len(word):
                if count > 0:
                    cur_s += str(count)
                self.res.append(cur_s)
            else:
                self.helper(pos+1, cur_s, count+1, word)  # case 1 count+1
                self.helper(pos+1, cur_s + (str(count) if count > 0 else '') + word[pos], 0, word)
```

[430. Flatten a Multilevel Doubly Linked List](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/)    

给一个target数字。然后从1开始，最少几个operation能到target value。有两种operations（x2 或者 /3）。比如说 1 * 2 * 2 * 2 * 2 / 3 * 2 = 10。注意 /3之后要floor。这道题我用的bfs。然后用一个hashmap记录已经visit过的。   


设计一个class。有两个function。 append(value) -> void, get_indexs -> indexs.  
比如说[120, 150, 125, 130] -> 相对应的index就是[3, -1, 3, -1]. 找出最后一个比你大的数字的index。  
这个时候如果append(126). 那么你见过的所有的数字就是[120,150,125,130,126]。 相对应的index就是[4, -1, 4, -1, -1].  
上来我就写了一个linear的solution。但是可以比linear更快。interviewer很多hint砸在我脸上之后。我懂了。  
trick就是要用一个bst寻找所有比新加的value小的数字, 这样比value大的数字就都不用看了。  


https://1o24bbs.com/t/topic/2690

[3. Longest Substring Without Repeating Characters ](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

在一个长得像V的数组，就是先递减再递增的数组里面找一个数。找到最小值后在两边binary search.   
https://knaidu.gitbooks.io/problem-solving/searching/Increasing-Decreasing%20Array.html   
  
[451. Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency/)  
```python
class Solution(object):
    def frequencySort(self, s):
        """
        :type s: str
        :rtype: str
        """
        result = ''
        bucket = [None for i in range(len(s) + 1)]  # store freq to list of char
        char_2_count = {}
        
        for char in s:
            char_2_count[char] = char_2_count.get(char, 0) + 1
            
        for key, value in char_2_count.items():
            if bucket[value] is None:
                bucket[value] = []
            
            bucket[value].append(key)
            
        for i in reversed(range(len(bucket))):
            if bucket[i] is not None:
                for char in bucket[i]:
                    result += char * i
                    
        return result
```

[140. Word Break II](https://leetcode.com/submissions/detail/225997402/)
改变版本， 只返回任意一种组合：
```python
class Solution(object):
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: List[str]
        :rtype: List[str]
        """
        wordDict = set(wordDict)
        
        def dfs(s):
            for word in wordDict:
                if not s.startswith(word): continue
                if len(word) == len(s):
                    return [word]
                else:
                    restOfWords = dfs(s[len(word):])
                    if restOfWords:
                        return [word] + restOfWords
        return dfs(s)
```


[273. Integer to English Words](https://leetcode.com/problems/integer-to-english-words/)

[62. Unique Paths](https://leetcode.com/problems/unique-paths/)

[1029. Two City Scheduling](https://leetcode.com/problems/two-city-scheduling/)

[546. Remove Boxes](https://leetcode.com/problems/remove-boxes/) https://www.youtube.com/watch?v=wT7aS5fHZhs  
  
[Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
回朔和Iterative 2种解法

给一个array， 里面只有1 和0， 求找出 连续最多1 的个数  
【00011110110000111111】
https://leetcode.com/problems/max-consecutive-ones/
```python
class Solution(object):
    def findMaxConsecutiveOnes(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        for i in range(1, len(nums)):
            if nums[i]:
                nums[i] += nums[i - 1]
        return max(nums)
```
follow up 把一个0 变为1， 找最长的1的长度。  

```python
# idea:
# 第一维https://leetcode.com/problems/max-consecutive-ones/
# 第二维存的是 如果加上虚拟的0的情况
class Solution(object):
    def findLongest(self, nums):
        for i in range(0, len(nums)):
            if i == 0 and nums[i] == 0:
                nums[i] = 0, 1
            else:
                nums[i] = (nums[i], 0)
        print(nums)
        for i in range(1, len(nums)):

            if nums[i][0]:
                nums[i] = (nums[i][0]+nums[i-1][0], 0)
        print(nums)

        for i in range(1, len(nums)):
            if nums[i][0] == 0:
                nums[i] = (nums[i][0], nums[i-1][0] + 1)
            else:
                nums[i] = (nums[i][0],  nums[i-1][1] + 1)

        print(nums)
        return max(max(num) for num in nums)

if __name__ == '__main__':
    nums = [0, 0, 1, 1]
    s = Solution()
    print(s.findLongest(nums))
```

[1396. Design Underground System](https://leetcode.com/problems/design-underground-system/)  

[160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)    

[283. Move Zeroes](https://leetcode.com/problems/move-zeroes/)  
  
[1382. Balance a Binary Search Tree](https://leetcode.com/problems/balance-a-binary-search-tree/)    

  
2中做法，  
一种Inorder的[解法](https://leetcode.com/problems/balance-a-binary-search-tree/discuss/539735/Clean-Python-3-inorder-%2B-rebuild-tree-O(N))  
旋转的解法 https://leetcode.com/submissions/detail/346539349/  
https://en.wikipedia.org/wiki/AVL_tree  

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
 [443. String Compression](https://leetcode.com/problems/string-compression/)  
 ```
 Input:
["a","a","b","b","c","c","c"]

Output:
Return 6, and the first 6 characters of the input array should be: ["a","2","b","2","c","3"]
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
[387. First Unique Character in a String](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/)  

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
[20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/) 
Stack 或者 replace函数，都在做题submission历史里面。  
  
  
判断算式是否包括多余的括号 如((a) + b), ((a + b))都是包含多余的  
((a+b)+c) false  
(a) ture base case  

```python3
class Solution(object):
    def checkRedundant(self, s):
        stack = []

        for c in s:
            if c != ')':  # 不是右括号
                stack.append(c)
            else:  # 是右括号的，一直pop到左括号
                evaluation = c
                while True:
                    ch = stack.pop()
                    evaluation = ch + evaluation
                    if ch == '(':
                        break
                if len(evaluation) == 3:
                    return False
                else:
                    stack.append('a')
        return True

if __name__ == '__main__':
    s = Solution()
    s1 = '(a)'
    s2 = '((a+b))'
    s3 = '((a+b)+c)'
    print(s.checkRedundant(s3))
```

一个未排序数组，让你返回若以数组中的数为三角形三边可以组成多少个三角形  
a + b > c
b + c > a
c + a > b
排序数组 
a < b < c
只要判断
a + b > c
```python3
def triangle(nums):
    nums = sorted(nums)
    res = []
    for i, a in enumerate(nums):
        for j, b in enumerate(nums):
            if j <= i:  # 跳过前面重复的
                continue

            for k, c in enumerate(nums):
                if k <= j:  # 跳过前面重复的
                    continue

                if a + b > c:
                    res.append([a, b, c])
                else:
                    break  # 如果不满足上面的if了，后面的不用再去循环了，肯定也不满足了
    return res


if __name__ == '__main__':
    nums = [1, 5, 2, 3, 7, 9]
    print(triangle(nums))
```
第二题： 给你各个机场间的航线，让你返回从一始发地到目的地的所有路线（不仅仅是最短的）
BFS

马拉松
一个马拉松比赛，假设路上有10个marker，然后你需要设计几个函数 Top(k)    
返回跑在前面的k个人的id， Update（runnerId，markerId）每次跑到某个marker的时候 call这个函数。    
Hashmap + linkedlist （虽然这里我觉得好像和LRU没太大的关系。别人的面经）    
k can is given at runtime.  
```python

class Node(object):
    def __init__(self, val, pre=None, next=None):
        self.val = val
        self.next = next
        self.pre = pre


class Malasong(object):

    def __init__(self, runners):  # runners 假设是list  [1, 5, 7] 编号的人
        # 10 marker
        # 1 2 3 4 5 这个人跑到了下个marker就删掉上一个地方的这个人 所以删掉1234
        # key marker1 value: [1 2 3 4] 删掉23
        # [2 3] 删掉3
        # [3]
        head = pre = Node(-1)
        self.num_2_node = {}
        self.total_runnre = len(runners)

        for runner in runners:  # 生成初始化的linkedlist
            cur = Node(runner)
            cur.pre = pre
            pre.next = cur
            pre = cur
            self.num_2_node[runner] = cur

        self.marker_2_linkedList = {}
        self.marker_2_linkedList[-1] = (head, head)  # 开跑前也当做一个marker 存head, tail

        for i in range(10):
            head = Node(-1)
            self.marker_2_linkedList[i] = (head, head)

    def Update(self, rid, markerId):
        # 去上个marker删掉，加到这个marker
        node = self.num_2_node[rid]
        pre = node.pre
        next = node.next
        pre.next = next  # 删掉了

        head, tail = self.marker_2_linkedList[markerId]
        tail.next = node
        node.pre = tail
        node.next = None
        self.marker_2_linkedList[markerId] = (head, node)

    def topK(self, k):
        if k > self.total_runnre or k < 0:
            return "error"

        res = []
        # find from the last marker
        for i in range(9, -1, -1):
            head, _ = self.marker_2_linkedList[i]
            while head.next:
                res.append(head.next.val)
                if len(res) == k:
                    return res
```
[173. Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator/)
```python
class BSTIterator(object):
    def __init__(self, root):
        """
        :type root: TreeNode
        """
        self.stack = []
        self.push(root)
        

    def hasNext(self):
        """
        :rtype: bool
        """
        return self.stack != []
    

    def next(self):
        """
        :rtype: int
        """
        tempNode = self.stack.pop()
        self.push(tempNode.right)
        return tempNode.val
        
        
    def push(self, node):
        while node:
            self.stack.append(node)
            node = node.left
```

给一串字母 连着取一串只有两种字母的字串 问最长可以取到的字串长度。
two pointer

```python
def findLongest(s):
    re = left = right = 0
    cache = {}  # key: c value: number of this char
    for i, c in enumerate(s):
        if c not in cache and len(cache) == 2:
            while len(cache) == 2:
                # remove left
                left_c = s[left]
                cache[left_c] -= 1
                if cache[left_c] == 0:
                    cache.pop(left_c)
                left += 1
            cache[c] = 1
        else:
            cache[c] = cache.get(c, 0) + 1
            right = i
            re = max(re, right - left + 1)
    return re


if __name__ == '__main__':
    s = 'aaabbcaadddddd'
    print(findLongest(s))
```
[LRU Cache](https://leetcode.com/problems/lru-cache/)


给你两个不同容量的杯子，和无尽的水，能有几种容量的水被量出来  
5 7  
max water: 5+7 = 12  
7-5 = 2    
5-（7-5）=3  

```python
class Solution(object):
    def findAllLiters(self, a, b):
        self.res = set()
        self.res.add(a)
        self.res.add(b)
        self.res.add(abs(a-b))
        visited = set()
        needVisit = [a, b]

        while needVisit:
            num = needVisit.pop(0)
            if num in visited:
                continue
            else:
                visited.add(num)

            new_find1 = self._findGap(a, b, num)
            new_find2 = self._findGap(b, a, num)
            if new_find1: needVisit.append(new_find1)
            if new_find2: needVisit.append(new_find2)

        self.res.add(a+b)
        return self.res

    def _findGap(self, a, b, num):
        temp_b = 0
        if b - num > 0:
            temp_b = b - num

            while temp_b > 0:  # 要一直减 如果 b 远大于a
                temp_b -= a
            temp_b += a

        if temp_b != 0 and a - temp_b > 0:
            new_num = a - temp_b
            self.res.add(new_num)
            print(self.res)
            return new_num


if __name__ == '__main__':
    s = Solution()
    print(s.findAllLiters(5, 18))
``` 
