Question 1. Implement a moving average function which takes an array of numbers ("arr") and a window size ("k");   
and returns an array of numbers which represents the moving average of "arr" given "k".  
Question 1:Example 1:arr = [1, 2, 3, 4, 5.75]  
k = 3returns [2, 3, 4.25]  
Provide Answer for Question 1 here:  
```python
def movingAverage(arr, k):
    windows_sum = 0
    res = []
    for i, n in enumerate(arr):
        windows_sum += n
        if i >= k-1:
            res.append(windows_sum / k)
            windows_sum -= arr[i-k+1]
    return res


print(movingAverage([1, 2, 3, 4, 5.75], 3))
```



Question 2. Given an infinite stream of positive integers ("s"), and a target positive integer ("t"), implement a function that iterates through the "s"
and returns when and only when a combination of the numbers seen so far sums to "t"  
Question 2:Example 1:stream = [3, 8, 15, 8, 15, 18, 14, 22, 10, 21, ...]  
target = 33returns at the 2nd 15, because 3 + 15 + 15 = 33  
Example 2:stream = [2, 2, 2, ..., 1, ...] = (a stream consisting of 10 trillion 2's followed by a 1)  
target = 5  
returns at the 1, because 2 + 2 + 1 = 5  

```Python
def findTargetCombination(stream, t):
    dp = [False] * (t+1)
    for i, n in enumerate(stream):  # O(N*T) N is length of the stream to current number, T is target number
        _dp = dp[:]
        for j in range(len(dp)):  # iterator the dp and find exist sum, make (exist sum)+ (cur num) to be exist
            if dp[j] and j + n < len(dp):
                _dp[j+n] = True
        if n < len(dp): _dp[n] = True
        dp = _dp
        # print(dp)
        if dp[t]:
            return n


if __name__ == '__main__':
    s = [3, 8, 15, 8, 15, 18, 14, 22, 10, 21]
    s1 = [2, 2, 2, 2, 2, 2, 1]
    print(findTargetCombination(s1, 5))
```

Alexa is given n piles of equal or unequal heights. In one step, Alexa can remove any number of boxes from the pile  
which has the maximum height and try to make it equal to the one which is just lower than the maximum height of the  
stack. Determine the minimum number of steps required to make all of the piles equal in height.  

Example 1:  

Input: piles = [5, 2, 1]  
Output: 3  
Explanation:  
Step 1: reducing 5 -> 2 [2, 2, 1]  
Step 2: reducing 2 -> 1 [2, 1, 1]  
Step 3: reducing 2 -> 1 [1, 1, 1]  
So final number of steps required is 3.  
```python
def minSteps(piles):
    n = len(piles)
    if n <= 1: return 0
    piles.sort()  # [1,2,2,5]
    moves = res = 0
    for i in range(1, n):
        if piles[i] == piles[i-1]:
            res += moves
        else:
            moves += 1
            res += moves
    return res

print(minSteps([1,2,5]))
```
findMostFrequent  
```python
import collections
def findMostFrequent(s):
    d = collections.OrderedDict()
    for c in s:
        d[c] = d.get(c, 0) + 1

    most = 0
    res = ""
    for k, v in d.items():
        if v > most:
            most = v
            res = k

    return res

if __name__ == '__main__':
    print(findMostFrequent("aabbcdef"))
```
