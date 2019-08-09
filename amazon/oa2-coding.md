OA2 Coding
===
### two sum
https://leetcode.com/problems/two-sum/discuss/17/Here-is-a-Python-solution-in-O(n)-time
```python
class Solution(object):
    def twoSum(self, nums, target):
        if len(nums) <= 1:
            return False
        buff_dict = {}
        for i in range(len(nums)):
            if nums[i] in buff_dict:
                return [buff_dict[nums[i]], i]
            else:
                buff_dict[target - nums[i]] = i
```
### 5. Longest Palindromic Substring
https://leetcode.com/problems/longest-palindromic-substring/description/
```python
class Solution(object):
    def longestPalindrome(self, s):
        self.n = len(s)
        self.long = self.left = 0
        for i in xrange(self.n):
            # even
            self.helper(i, i+1, s)
            self.helper(i-1, i+1, s)
        return s[self.left: self.left+self.long]
    
    def helper(self, l, r, s):
        while 0 <= l and r < self.n and s[l] == s[r]:
            l -= 1
            r += 1
        l += 1
        r -= 1
        if r - l + 1 > self.long:
            self.long = r - l + 1
            self.left = l
```
### 937. Reorder Log Files
```python
class Solution(object):
    def reorderLogFiles(self, logs):
        digits = []
        letters = []
		# divide logs into two parts, one is digit logs, the other is letter logs
        for log in logs:
            if log.split()[1].isdigit():
                digits.append(log)
            else:
                letters.append(log)
        letters.sort(key = lambda x: (x.split()[1:], x.split()[0])) 
        result = letters + digits  #put digit logs after letter logs
        return result
```
### Length K substring with k-1 distinct characters 
![distinck-k](https://github.com/shusenwu/note/blob/master/amazon/123125pkmerno0xkm4rrp7.png)
```python
def subStringLessKDist(inputString, num):
    if not inputString or len(inputString) == 0 or num <= 1 or inputString <= num:
        return []
    res = set()
    for i in xrange(len(inputString)-num+1):
        cur = inputString[i: i+num]
        if len(set(cur)) == num - 1:
            res.add(cur)
    return list(res)
```
### 819. Most Common Word
https://leetcode.com/problems/most-common-word/description/  
```python
class Solution(object):
    def mostCommonWord(self, paragraph, banned):
        paragraph = re.findall(r'\b[a-zA-Z]+', paragraph.lower())
        dic = collections.Counter(paragraph).most_common()
        for x in dic:
            if x[0] not in banned:
                return x[0]
                break
```
### Maximum Minimum Path 
You are gonna climb mountains represented by a matrix. Each integer in the matrix represents the altitude at that point. You are supposed to climb from the top-left corner to the bottom-right corner and only move rightward or downward in each step. You can have many paths to do so. Each path has a minimum altitude. Find the maximum among all the minimum altitudes of all paths. e.g.
```
[[5, 4, 5], [1, 3, 6]]
```
Three paths: 5 1 3 6,5 4 3 6,5 4 5 6. Minimums are 1, 3, 4 respectively. Return the maximum in them which is 4. another example:
```
[[8, 4, 7], [6, 5, 9]]
```
3 paths:
```
8-4-7-9 min: 4 8-4-5-9 min: 4 8-6-5-9 min: 5 return: 5
```

```python
class Solution:
    def minMaxPath(self, matrix):
        if len(matrix) == 0 or len(matrix[0]): return float('-inf')
        r, c = len(matrix), len(matrix[0])
        self.re = float('-inf')
        def dfs(i, j, pathMin):
            if i >= r or j >= c:
                return
            pathMin = min(pathMin, matrix[i][j])
            if i == r-1 and j == c-1:
                self.re = max(self.re, pathMin)
                return
            dfs(i+1, j, pathMin)
            dfs(i, j+1, pathMin)

        dfs(0, 0, float('inf'))
        return self.re
```
### Count Number of substrings with exactly k distinct characters 
https://www.geeksforgeeks.org/count-number-of-substrings-with-exactly-k-distinct-characters/
```python
def countkDist(str1, k):
    # Consider all substrings between str[i..j] 
    res = 0
    for i in xrange(len(str1)):
        count = 0
        dic = {}
        for j in xrange(i, len(str1)):
            c = str1[j]
            if c not in dic:
                count += 1
                dic[c] = 1
            else:
                dic[c] += 1
            if count == k:
                res += 1
            elif count > k:
                break
    return res
```
### Two sum closest diff
http://www.noteanddata.com/Amazon-OA-2-sum-closest.html  
```python
def twoSumClosestDiff(arr, target):
    arr.sort()
    res = float('inf')
    l, r = 0, len(arr) - 1
    while l < r:
        s = arr[l] + arr[r]
        res = min(res, abs(s-target))
        if s < target:
            l += 1
        elif s > target:
            r -= 1
        else:
            return 0
    return res
```
### Two Sum Closest
Given two sorted arrays and a number x, ﬁnd the pair whose sum is closest to x and << x and the pair has an element from each array. We are given two arrays ar1[0…m-1] and ar2[0..n-1] and a number x, we need to ﬁnd the pair ar1[i] + ar2[j] such that absolute value of (ar1[i] + ar2[j] – x) is minimum  
```
Input:  ar1[] = {1, 4, 5, 7};        ar2[] = {10, 20, 30, 40};        x = 32       Output:  1 and 30
 
Input:  ar1[] = {1, 4, 5, 7};        ar2[] = {10, 20, 30, 40};        x = 50       Output:  7 and 40
```
```python
def closesTwoSum(arr1, arr2, x):
    arr1.sort()
    arr2.sort()
    n1, n2 = len(arr1), len(arr2)
    p1, p2 = 0, n2-1
    minDiff = float('inf')
    res = [float('inf'), float('inf')]
    while p1 < n1 and p2 >= 0:
        curDiff = x - arr1[p1] - arr2[p2]
        if 0 < curDiff < minDiff:
            minDiff = curDiff
            res = [arr1[p1], arr2[p2]]
        if curDiff > 0:
            p1 += 1
        else:
            p2 -= 1
    return res
```
### Subtree with Maximum Average
Description Given a binary tree, ﬁnd the subtree with maximum average. Return the root of the subtree. Example Given a binary tree: 1 / \ -5 11 / \ / \ 1 2 4 -2 return the node 11. Your problem can be diﬀerent in ways like -- it may not be a binary tree or the average doesn't include the root of the substree.  
https://blog.csdn.net/sinat_32547403/article/details/77824104  
```
class Solution:
    def findSubtree2(self, root):
        if not root:
            return
        self.avg, self.node = float('inf'), None

    def helper(self, root):
        if not root: return 0, 0
        sumLeft, countLeft = self.helper(root.left)
        sumRight, countRight = self.helper(root.right)
        sumRoot = sumLeft + sumRight + root.val
        countRoot = countLeft + countLeft + 1
        avg = sumRoot * 1.0 / countRoot
        if avg > self.avg:
            self.avg = avg
            self.node = root
        return sumRoot, countRoot
```
变形：
Maximum Subtree of Average
就是给一棵多叉树，表示公司内部的上下级关系。每个节点表示一个员工，节点包含的成员是他工作了几个月(int)，以及一个下属数组(ArrayList)。目标就是找到一棵子树，满足：这棵子树所有节点的工作月数的平均数是所有子树中最大的。最后返回这棵子树的根节点。这题补充一点，返回的不能是叶子节点(因为叶子节点没有下属)，一定要是一个有子节点的节点。  
https://www.jianshu.com/p/3c1a6726651e  
```python

class Node:
    def __init__(self, val):
        self.val = val
        self.children = []
class Solution:
    def find(self, Node):
        self.avg = float('-inf')
        self.node = None
        self.dfs(root)
        return self.node

    def dfs(self, root):
        if not root: return 0, 0  # sum, count
        if not root.children:
            return root.val, 1
        sumRoot, countRoot = root.val, 1
        for node in root.children:
            sumChild, countChild = self.dfs(node)
            sumRoot += sumChild
            countRoot += countChild
        if countRoot > 1 and sumRoot * 1.0 / countRoot > self.avg:
            self.avg = sumRoot * 1.0 / countRoot
            self.node = root
        return sumRoot, countRoot
```
### 7. K minimum Distances
A 2D matrix with 0, 1, 9. Get minimum number of steps to achieve 9.    
0 -- obstable  
1--path  
9--gold  
```python
class Solution:
    def removeObstacle(self, m, n, lot):
        self.res = float('inf')
        self.dfs(lot, m, n, 0)
        return self.res

    def dfs(self, lot, i, j, step):
        if 0 <= i < len(lot) and 0 <= j < len(lot[0]) and lot[i][j] != 0:
            if lot[i][j] == 9:
                self.res = min(self.res, step)
                return
            lot[i][j] = 0
            self.dfs(lot, i-1, j, step+1)
            self.dfs(lot, i+1, j, step+1)
            self.dfs(lot, i, j-1, step+1)
            self.dfs(lot, i, j+1, step+1)
            lot[i][j] = 1
```
### K Nearest Points 
Load goods into a truck. Truck is at the origin and you are given the coordinates of all goos, ﬁnd the k nearest goods.   
https://blog.csdn.net/Sengo_GWU/article/details/82490880  
O(n + klogn)  
```python
import heapq
def findKClosest(p, k):
    nums = [(x*x+y*y, x, y) for x, y in p]
    heapq.heapify(nums)
    res = []
    for _ in xrange(k):
        if nums:
            res.append(heapq.heappop(nums)[1:])
    return res
```
### high five
Description There are two properties in the node student id and scores, to ensure that each student will have at least 5 points, ﬁnd the average of 5 highest scores for each person.   
```python
from heapq import heappush, heappushpop
def highfive(students):
    result = {}
    for student in students:
        id = student[0]
        mark = student[1]
        if id not in result:
            result[id] = [mark]
        else:
            marks = result[id]
            if len(marks) < 5:
                heappush(marks, mark)
            elif mark > marks[0]:
                heappushpop(marks, mark)
    for id, marks in result.items():
        result[id] = sum(marks) / 5
    return result
```
### Flight
Amazon Prime Air Shipping Routes
Amazon Prime Air is developing a system that divides shipping routes using flight optimization routing systems to a cluster of aircraft that can fulfill these routes. Each shipping route is identified by a unique integer identifier, requires a fixed non-zero amount of travel distance between airports, and is defined to be either a forward shipping route or a return shipping route. Identifiers are guaranteed to be unique within their own route type, but not across route types. from aonecode.com

Each aircraft should be assigned two shipping routes at once: one forward route and one return route. Due to the complex scheduling of flight plans, all aircraft have a fixed maximum operating travel distance, and cannot be scheduled to fly a shipping route that requires more travel distance than the prescribed maximum operating travel distance. The goal of the system is to optimize the total operating travel distance of a given aircraft. A forward/return shipping route pair is considered to be "optimal" if there does not exist another pair that has a higher operating travel distance than this pair, and also has a total less than or equal to the maximum operating travel distance of the aircraft. from aonecode.com

For example, if the aircraft has a maximum operating travel distance of 3000 miles, a forward/return shipping route pair using a total of 2900 miles would be optimal if there does not exist a pair that uses a total operating travel distance of 3000 miles, but would not be considered optimal if such a pair did exist. from aonecode.com

Your task is to write an algorithm to optimize the sets of forward/return shipping route pairs that allow the aircraft to be optimally utilized, given a list of forward shipping routes and a list of return shipping routes. from aonecode.com

Input
The input to the function/method consists of three arguments: from aonecode.com
maxTravelDist, an integer representing the maximum operating travel distance of the given aircraft;from aonecode.com
forwardRouteList, a list of pairs of integers where the first integer represents the unique identifier of a forward shipping route and the second integer represents the amount of travel distance required by this shipping route; 
retumRouteList, a list of pairs of integers where the first integer represents the unique identifier of a return shipping route and the second integer represents the amount of travel distance required by this shipping route. 

Output from aonecode.com
Return a list of pairs of integers representing the pads of IDs of forward and return shipping routes that optimally utilize the given aircraft. If no route is possible, return an empty list. from aonecode.com

Examples from aonecode.com
Example 1: Input: maxTravelDist= 7000 forwardRouteList = [[1,2000],[2,4000],[3,6000]] retumRouteList = [[1,2000]] 

Output: [[2,1]] from aonecode.com

Explanation: There are only three combinations, [1,1], [2,1], and [3,1], which have a total of 4000, 6000, and 8000 miles, respectively. Since 6000 is the largest use that does not exceed 7000, [2,1] is the only optimal pair.from aonecode.com 

Example 2: Input: maxTravelDist= 10000 forwardRouteList = [[1, 3000], [2, 5000], [3, 7000], [4, 10000]] retumRouteList= [[1, 2000], [2, 3000], [3, 4000], [4, 5000]] from aonecode.com

Output: [[2, 4], [3, 2]] 

Explanation: There are two pairs of forward and return shipping routes possible that optimally utilizes the given aircraft. Shipping Route ID#2 from the forwardShippingRouteList requires 5000 miles travelled, and Shipping Route ID84 from returnShippingRouteList also requires 5000 miles travelled. Combined, they add up to 10000 miles travelled. Similarly, Shipping Route ID#3 from forwardShippingRouteList requires 7000 miles travelled, and Shipping Route ID#2 from returnShippingRouteList requires 3000 miles travelled. These also add up to 10000 miles travelled. Therefore, the pairs of forward and return shipping routes that optimally utilize the aircraft are [2, 4] and [3, 2]. 
```python
def flight(forward, back, maxDist):
    res = []
    if not forward or not back:
        return res
    dist = 0
    for a, d1 in forward:
        for b, d2 in back:
            if dist < d1 + d2 <= maxDist:
                res = [[a, b]]
                dist = d1 + d2
            elif d1 + d2 == dist:
                res.append([a, b])
    return res

F = [[1, 3000], [2, 5000], [3, 7000], [4, 10000]]
B = [[1, 2000], [2, 3000], [3, 4000], [4, 5000]]
M = 10000
print flight(F, B, M)
```

### 505. The Maze II
https://leetcode.com/problems/the-maze-ii/description/ 
```python
class Solution(object):
    def shortestDistance(self, maze, start, destination):
        des = tuple(destination)
        r, c = len(maze), len(maze[0])
        
        def go(x, y, dx, dy):
            step = 0
            while 0 <= x+dx < r and 0 <= y+dy < c and maze[x+dx][y+dy] == 0:
                x += dx
                y += dy
                step += 1
            return (x, y), step
        
        heap = [(0, tuple(start))]
        visited = {}
        while heap:
            distance, cur = heapq.heappop(heap)
            if cur in visited and visited[cur] <= distance:
                continue
            if cur == des: return distance
            visited[cur] = distance
            
            for dx, dy in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
                nextCur, step = go(cur[0], cur[1], dx, dy)
                heapq.heappush(heap, (distance+step, nextCur))
        return -1
```
### MST
城市连接问题: https://www.ctolib.com/topics-80931.html  
题目内容是这样的，给十几个城市供电，连接不同城市的花费不同，让花费最小同时连到所有的边。给出一系列connection类，里面是edge两端的城市名和它们之间的一个cost，找出要你挑一些边，把所有城市连接起来并且总花费最小。不能有环，最后所以城市要连成一个连通块。  
不能的话输出空表，最后还要按城市名字排序输出，按照node1来排序,如果一样的话再排node2。  
输入:  
 
{"Acity","Bcity",1}  

("Acity","Ccity",2}  

("Bcity","Ccity",3}  

输出：  

("Acity","Bcity",1}  

("Acity","Ccity",2}  

补充一句，test case一共有6个
写了一遍没有测试用例试也是感觉很虚
```python
class Solution:
    def getLowCost(self, connections):
        if not connections: return []
        # sort for kruskal
        connections.sort(key=lambda cnt: cnt[2])
        res = []
        # init
        self.parents = {}
        for c1, c2, cost in connections:
            if c1 not in self.parents:
                self.parents[c1] = c1
            if c2 not in self.parents:
                self.parents[c2] = c2
            if self.union(c1, c2):  # if not circle, union else drop
                res.append([c1, c2, cost])

        # check all the city is in the same root
        root = ''
        for c in self.parents.keys():
            if not root:
                root = self.find(c)
            elif self.find(c) != root:
                return []
        # sort city name according to city1 name then city2 name
        res.sort()
        return res

    def union(self, city1, city2):
        p1 = self.find(city1)
        p2 = self.find(city2)
        if p1 == p2:  # circle
            return False
        else:
            self.parents[p2] = p1
            return True

    def find(self, city):
        if self.parents[city] == city:
            return city
        self.parents[city] = self.find(self.parents[city])
        return self.parents[city]
```
### shoppers  partition labels
https://leetcode.com/problems/partition-labels/description/
![shoppers](https://github.com/shusenwu/note/blob/master/amazon/OA2-shopper.jpeg?raw=true)
O(n) 24 char
```python
class Solution(object):
    def partitionLabels(self, s):
        dic = {}
        for i, char in enumerate(s):
            dic[char] = i
        
        res = []
        l , r = 0, 0
        for i, char in enumerate(s):
            r = max(r, dic[char])
            if i == r:
                res.append(r-l+1)
                l = r + 1
        return res
```
```python
import collections
def shopper(shops):
    if not shops: return []
    d = collections.defaultdict(list)
    for i, s in enumerate(shops):
        d[s].append(i)

    intervals = d.values()
    intervals.sort()
    for i, inter in enumerate(intervals):
        if len(inter) == 1:
            intervals[i] = inter + inter
        else:
            intervals[i] = [inter[0], inter[-1]]
    res = [intervals[0]]
    for start, end in intervals[1:]:
        if start <= res[-1][1]:
            res[-1][1] = max(res[-1][1], end)
        else:
            res.append([start, end])
    return [end - start + 1 for start, end in res]
```
### 138. Copy List with Random Pointer
https://leetcode.com/problems/copy-list-with-random-pointer/description/ 
```python
# Definition for singly-linked list with a random pointer.
# class RandomListNode(object):
#     def __init__(self, x):
#         self.label = x
#         self.next = None
#         self.random = None
 
class Solution(object):
    def copyRandomList(self, head):
        d = dict()
        p1 = p2 = head
        
        while p1:
            d[p1] = RandomListNode(p1.label)
            p1 = p1.next
            
        while p2:
            d[p2].next = d.get(p2.next)
            d[p2].random = d.get(p2.random)
            p2 = p2.next
        return d.get(head)
```
### Order Dependency 
https://leetcode.com/problems/course-schedule/description/ 
https://blog.csdn.net/Sengo_GWU/article/details/81966972 
### Window Sum
```java
public static ArrayList<Integer> getWindowSum(ArrayList<Integer> list, int k){ 
	if(list == null || list.size() == 0) return new ArrayList<Integer>(); 
	if(k < 1 || k > list.size()) return null; 
	ArrayList<Integer> ans = new ArrayList<Integer>(); 
	int len = list.size(); 
	int sum = 0; 
	for(int i = 0; i < len; i++){ 
		sum += list.get(i);
		if(i-k+1 >= 0){ 
			ans.add(sum); 
			sum -= list.get(i-k+1); 
		} 
	} 
	return ans; 
}
```
### 零件组装
题目意思就是有一堆零件，每个零件的尺寸和组装需要的时间是一样的。输入各个零件的尺寸的list，要求输出最短的总的 accumulated 组装时间。这么说估计也很难描述清楚，直接上例子： 
比如输入的list是 {8， 4， 6， 12}。
1. 先选 4 和 6组装到一起，形成 size 为 10 的新零件。目前为止耗时为10。零件的 list 变为 {8， 10， 12}
2. 再选 8 和 10 组装到一起，形成 size 为 18 的新零件。目前为止耗时为 10 + 18 = 28。零件的 list 变为 {12， 18}
3. 最后 把 12 和 18 组装到一起，形成 size 为 30 的新零件。目前为止耗时为 10 + 18 + 30 = 58。
最后输出 58 就可以了。
```python
import heapq
def accumateTime(sizes):
    heapq.heapify(sizes)
    res = 0
    while len(sizes) >= 2:
        a, b = heapq.heappop(sizes), heapq.heappop(sizes)
        res += a+b
        heapq.heappush(sizes, a+b)
    return res

print accumateTime([8, 4, 6, 12])
```
### 1000. Minimum Cost to Merge Stones 
https://blog.csdn.net/Sengo_GWU/article/details/81603006 
