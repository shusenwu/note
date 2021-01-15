655. Print Binary Tree https://leetcode.com/problems/print-binary-tree/  


```
题目二： 组建球队， 给一个list 是每个人的socres, 还有一个list 是每个人的ages，
同一个球队里面， 没有人数限制， 但是年长的人的score必须大于年少的人的score， 这俩人才能在一个队
age2>age1 =>  score2>score1
返回队伍的最大score
eg. scores = [4, 5, 6, 5] ages = [2, 1, 2, 1]

先根据年龄排序，然后对成绩维持一个monotonic queue 保持递增或者相等（非递减），然后每次在queue里面取max 的sum 
```


```
Given an integer array nums, find number of distinct contiguous subarrays with at most k odd elements. Two subarrays are distinct when they have at least one different element.

Example 1:

Input: nums = [3, 2, 3, 4], k = 1
Output: 7 
Explanation: [3], [2], [4], [3, 2], [2, 3], [3, 4], [2, 3, 4]
Note we did not count [3, 2, 3] since it has more than k odd elements.

class Solution {
    
    public int distinctSubarraysAtMostKOdd(int[] nums, int k) {
        int count = 0;
        StringBuilder sb = new StringBuilder();
        Set<String> set = new HashSet<String>();
        
        for (int i = 0; i < nums.length; i++) {
            int oddCount = 0;
            sb.setLength(0);
            
            for(int j = i; j < nums.length; j++) {
                if(isOdd(nums[j])) {
                    oddCount++;        
                }
                
                if(oddCount > k)
                    break;
                
                sb.append("{").append(nums[j]).append("},");
                set.add(sb.toString());
            }
        }
        
        return set.size();
    }
    
    private boolean isOdd(int x) {
        return (x & 1) == 1;
    }
    
}

public class Main { 
    
    public static void main(String[] args) {
        test(new int[] {3, 2, 3, 2}, 1, 5);
        test(new int[] {3, 2, 3, 4}, 1, 7);
        test(new int[] {1, 3, 9, 5}, 2, 7);
        test(new int[] {2, 2, 5, 6, 9, 2, 11, 9, 2, 11, 12}, 1, 18);
    }
    
    private static void test(int[] nums, int k, int expected) {
        Solution sol = new Solution();
        int actual = sol.distinctSubarraysAtMostKOdd(nums, k);
        if (actual == expected) {
            System.out.println(actual);
        } else {
            throw new AssertionError(String.format("Expected %d, but actual %d", expected, actual));
        }
    }
}
```

```
汇率转换
399. Evaluate Division  
https://leetcode.com/problems/evaluate-division/
https://leetcode.com/submissions/detail/206565428/
```
