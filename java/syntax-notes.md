Java 算法常用语法整理
==


```java
// Array
int[] A = new int[256];
A.length; 

List<String> ans = new ArrayList<>();
ans.add();

// max value
Integer.MAX_VALUE
Integer.MIN_VALUE
LONG.MAX_VALUE
LONG.MIN_VALUE
Byte.MAX_VALUE
Byte.MIN_VALUE
Short.MAX_VALUE
Short.MIN_VALUE

Math.max();


// String  
s.toCharArray()
s.length();

// String buffer
StringBuilder sb = new StringBuilder();
sb.append(" ");
sb.toString();

// Map
HashMap<Character, Integer> map = new HashMap<Character, Integer>();
map.containsKey(s.charAt(i));

// Queue 
Queue<Character> queue = new LinkedList<>();
queue.contains(c);
queue.poll();
queue.offer(c);
queue.size();

// Stack
Stack<Integer> stack = new Stack<Integer>();
stack.push(j); 
stack.isEmpty();
stack.pop();
stack.peek();

Deque stack = new ArrayDeque<>(s.length());
//Stack and ArrayDeque are implemented with resizable array, and every time it is full, 
// all of the elements will be copied to a new allocated array, which is costly if this process 
// is invoked repeatedly and thus leads to TLE on large test cases. Specifying an initial **capacity** 
// can prevent this from happening.


//Set
Set<String> fwd = new HashSet<String>();
fwd.add(beginWord);
fwd.isEmpty();
fwd.remove(beginWord);
for(String str : fwd)

// Single linked list
public class ListNode {
    int val;
    ListNode next;
    ListNode() {}  // 这个和下面都是构造方法
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}
```
