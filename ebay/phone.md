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
