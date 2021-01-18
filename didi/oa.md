Maximum sum of two elements whose digit sum is equal https://www.geeksforgeeks.org/maximum-sum-of-two-elements-whose-digit-sum-is-equal/  

```java

import java.util.HashMap;

public class Solution{

    static int digitSum(int n)
    {
        int sum = 0;
        while (n != 0)
        {
            sum += (n % 10);
            n /= 10;
        }
        return sum;
    }

    public static void main(String args[])
    {
        int ans = -1;
        int arr[] = { 55, 23, 32, 46, 88 };
        HashMap map = new HashMap();
        int mainValue = 0;
        for(int n: arr)
        {
            int addedValue = digitSum(n);
            if(addedValue > 0)
            {
                if(map.containsKey(addedValue))
                {
                    mainValue = (Integer) map.get(addedValue);
                    map.put(addedValue, mainValue+n);
                    ans = Math.max(ans, mainValue+n);
                }
                else
                {
                    map.put(addedValue, n);
                }
            }
        }
        System.out.println(ans);
    }

}
```


```c++
Min Deletions to Make Frequency of Each Letter Unique  
Given a string s consisting of n lowercase letters, you have to delete the minimum number of characters from s
so that every letter in s appears a unique number of times. We only care about the occurrences of letters 
that appear at least once in result.
https://molchevskyi.medium.com/best-solutions-for-microsoft-interview-tasks-min-deletions-to-make-frequency-of-each-letter-unique-16adb3ec694e

int solution(const string & s) {
    // counter of characters to delete
    int count = 0;
    // array of counters of occurrences for all possible characters
    vector<int> occurrences('z' - 'a', 0);
    // count the occurrences
    for (char c: s) { ++occurrences[c - 'a']; }
    priority_queue<int> pq;
    // put non zero occurrences into the queue
    for (int c: occurrences) {
        if (c != 0) { pq.push(c); }
    }
    while (!pq.empty()) {
        // take the biggest frequency of a character
        int most_frequent = pq.top(); pq.pop();
        if (pq.empty()) { return count; }
        // if this frequency is equal to the next one
        // and bigger than 1 decrease it to 1 and put
        // back to the queue
        if (most_frequent == pq.top()) {
            if (most_frequent > 1) {
                pq.push(most_frequent - 1);
            }
            count++;
        }
        // all frequencies which are bigger than
        // the next one are removed from the queue 
        // because they are unique
    }
    return count;
}

```

```python 
找index，可以把A, B 拆成2部分sum一样的。 找有几个这样的INDEX.
https://www.1point3acres.com/bbs/thread-663257-1-1.html
def findNumberOfIndex(A, B):
    sum_a = sum(A)
    sum_b = sum(B)
    if sum_a % 2 or sum_b % 2:
        return 0

    count = 0
    pre_sum_a = pre_sum_b = 0
    for i in range(len(A)):
        pre_sum_a += A[i]
        pre_sum_b += B[i]

        if pre_sum_a == sum_a / 2 and pre_sum_b == sum_b / 2:
            count += 1

    return count

A = [1, 4, 2, -2, 5]
B = [7, -2, -2, 2, 5]

print(findNumberOfIndex(A, B))
```

```python
def isCircle(A, B):
    # https://www.1point3acres.com/bbs/thread-663257-1-1.html
    if len(set(A)) != len(A) or len(set(B)) != len(B):
        return False
    m = {}
    nodes = set(A)
    for i in range(len(A)):
        m[A[i]] = B[i]

    start = dummy = A[0]
    while m[start] != dummy and len(nodes):
        nodes.remove(start)
        start = m[start]
    nodes.remove(start)
    return len(nodes) == 0

A = [3, 1, 2]
B = [2, 3, 1]

print(isCircle(A, B))  # True

print(isCircle([1, 2, 3, 4], [2, 1, 4, 4]))  # F

print(isCircle([1, 2, 3, 4], [2, 1, 4, 3]))  # F

print(isCircle([1, 2, 1], [2, 3, 3]))  # F

print(isCircle([1, 3, 2, 4], [4, 1, 3, 2]))  # T
```
