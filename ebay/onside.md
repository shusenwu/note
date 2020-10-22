 给一个list a，要求找到里面的peak （比两边的元素大，首尾的两个元素只考虑一边就行）, 移走最小的peak, 再重新找所有peak, 直到都移走为止。按顺序把移走的peak们放进一个list里输出   
Two peaks can never be adjacent.  
Removing a min peak may turn at most one neighboring element into a peak.  
total runtime complexity is O(n log n) using additional O(n) space.  
 ```PYTHON
 def min_peaks(arr):
  n = len(arr)

  # add sentinel
  arr.append(float('-inf'))
  ans = []

  # represents doubly-linked list
  # 0 <-> 1 <-> ... <-> n <-> 0
  prv = [n] + range(n)
  nxt = range(1, n+1) + [0]

  # initialize min-heap of peaks
  peaks = []
  def _check_peak(i):
    if arr[prv[i]] < arr[i] > arr[nxt[i]]:
      heappush(peaks, (arr[i], i))
  for i in xrange(n):
    _check_peak(i)

  # remove min peak and check neighbors
  while peaks:
    val, i = heappop(peaks)
    ans.append(val)
    # before: j <-> i <-> k
    j, k = prv[i], nxt[i]
    prv[k] = j
    nxt[j] = k
    # after: j <-> k
    _check_peak(j)
    _check_peak(k)

  # remove sentinel (optional)
  arr.pop()
  return ans
  ```
