```python
merge two sort intervals  
2 pointers 分别指向Interval1 和Interval 对应的index
给一个变量指向当前的Interval 
给一个变量指向下一个最小的interval  

def mergeIntervals(int1, int2):
    if not int1 or not int2:
        return int1 or int2
    ret = []
    i = 0
    j = 0
    if int1[0][0] < int2[0][0]:
        curr = int1[0]
        i = 1
    else:
        curr = int2[0]
        j = 1
    
    while i < len(int1) or j < len(int2):
        if j == len(int2) or int1[i][0] < int2[j][0]:
            nxt = int1[i]
            i += 1
        else:
            nxt = int2[j]
            j += 1
        if curr[1] < nxt[0]:
            ret.append(curr)
            curr = nxt
        else:
            curr[1] = max(curr[1], nxt[1])
    ret.append(curr)

    return ret

```

986. Interval List Intersections  https://leetcode.com/problems/interval-list-intersections/  
143. Reorder List  https://leetcode.com/problems/reorder-list/  

31. Next Permutation  https://leetcode.com/problems/next-permutation/  

655. Print Binary Tree https://leetcode.com/problems/print-binary-tree/  


```
题目二： 组建球队， 给一个list 是每个人的socres, 还有一个list 是每个人的ages，
同一个球队里面， 没有人数限制， 但是年长的人的score必须大于年少的人的score， 这俩人才能在一个队
age2>age1 =>  score2>score1
返回队伍的最大score
eg. scores = [4, 5, 6, 5] ages = [2, 1, 2, 1]

先根据年龄排序，然后对成绩维持一个monotonic queue 保持递增或者相等（非递减），然后每次在queue里面取max 的sum 
```


```java
Given an integer array nums, find number of distinct contiguous subarrays with at most k odd elements.
Two subarrays are distinct when they have at least one different element.

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
# BQ
general BQ，怎么跟组员相处，有conflict怎么解决，  
BQ 1: showcase technical skill  
BQ 1: resolved conflict  
BQ 3: career discussion  

# System Design
## 设计uber 

## Design a location tracking service.  
Imagine there are a lot of Uber driver running on the road and each of their uber app will send location periodically.   
Design a service that keep track of thos locations to support other backend services.  
This system will  
1. record the driver's latest location  
2. reply the query of : how many drivers are in a specific geo fence and who are those drivers  
req: lat/long radius  
## 一轮 SystemDesign RateLimiter

## 第二轮：1小时， system design，要求设计一个实时评论显示系统，给你一个Post component和一个Command component，
其他的什么storage啊 traffic都已经take care了，然后不刷新页面，如何在别人评论了之后看到这条评论。聊到了使用websocket和pub-sub的一些。

## 系统设计: tinyUrl  

## 基本围绕简历，how did you collaborate, constructive feedback，some mentorship details.  
```
 设计一个交通的heat map。每个司机每秒会把自己的位置发给系统，然后通过这些信息来显示某个区域，
 比如三番，的实时交通密度情况。主要有两个要求，第一个要求是以每分钟为一个bucket来统计，然后需要记录过去二十分钟的数据，
 这个要求对realtime的要求比较高。第二个要求是保存过去两年的数据，只需要每天更新一次就行，主要用于offline的研究
 。问了面试官如果一个司机在一分钟的时间里去过地图上不同的点（把地图分成很多个grid的话一分钟内去过多个grid），
 那这个司机是算一次还是多次。面试官的回答是多次，我觉得多次应该也比较好算一点。我的感觉就是设计data pipeline来收集和汇总数据，
 然后同时满足realtime和batch处理的需求。
 ```
