```python
https://leetcode.com/problems/permutations-ii/submissions/ 
47. Permutations II
class Solution(object):
    def permuteUnique(self, nums):
        ans = [[]]
        for n in nums:  # 遍历list, 把每个数字插入到 ans里面的list的每个位置
            new_ans = []
            for arr in ans:
                for i in xrange(len(arr)+1):
                    new_ans.append(arr[:i]+[n]+arr[i:])
                    # print new_ans
                    if i<len(arr) and arr[i]==n: break              #handles duplication  [1 1 2]的情况 打印出来看， 第二个打印， 先把第                   
                                                                    # 二个1 加进去，然后判断 arr[0] = 1了就不继续了,  比如【1】 你插入原来1的左边1后就不插入右边1了
            ans = new_ans
            print ans
        return ans
```

```python
https://leetcode.com/problems/longest-continuous-subarray-with-absolute-diff-less-than-or-equal-to-limit/ 
1438. Longest Continuous Subarray With Absolute Diff Less Than or Equal to Limit  
class Solution(object):
    def longestSubarray(self, nums, limit):
        """
        :type nums: List[int]
        :type limit: int
        :rtype: int
        Monotonic Queue O（n）
        https://leetcode.com/problems/longest-continuous-subarray-with-absolute-diff-less-than-or-equal-to-limit/discuss/609743/Java-Detailed-Explanation-Sliding-Window-Deque-O(N)
        """
        max_deque, min_deque = deque(), deque()
        res, l = 1, 0
        for r in range(len(nums)):
            while max_deque and max_deque[-1] < nums[r]:  # max_queue 递减
                max_deque.pop()
            max_deque.append(nums[r])
            
            while min_deque and min_deque[-1] > nums[r]:  # max_queue 递增
                min_deque.pop()
            min_deque.append(nums[r])
            
            while max_deque[0] - min_deque[0] > limit:
                if max_deque[0] == nums[l]:
                    max_deque.popleft()
                    
                if min_deque[0] == nums[l]:
                    min_deque.popleft()
                
                l += 1
            res = max(res, r - l + 1)
        return res
            
```

```python
https://leetcode.com/problems/boundary-of-binary-tree/ 
545. Boundary of Binary Tree
```


```python
Sparse array search
class Solution:
    def findString(self, words, s):
        left, right = 0, len(words) - 1
        while left <= right:
            mid = (left + right) // 2
            tmp = mid  # 避免重复扫描
            while mid > left and words[mid] == '':
                mid -= 1
            if words[mid] == s:
                return mid
            elif words[mid] > s:
                right = mid - 1
            else:
                left = tmp + 1
        return -1


arr = ["", "", "", "", "", "", "", "", "", "dad", "", "ta"]
s = Solution()
re = s.findString(arr, "ta")
print(re)
```

```python
Flatten nexted list
l = [1, 2, [3, 4, [5, 6]], 7, 8, [9, [10]]]
# output list
output = []

# function used for removing nested
# lists in python.
def reemovNestings(l):
    for i in l:
        if type(i) == list:
            reemovNestings(i)
        else:
            output.append(i)
```
