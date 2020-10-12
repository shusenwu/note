Java Notes
==

廖雪峰： https://www.liaoxuefeng.com/wiki/1252599548343744/1255943629175808
 


```java
// Array  List
int[] A = new int[256];
A.length; 
int[] number = new int[]{1, 2, 3, 5, 8}; // 不要指定长度 初始化array
// 排序
int[][] intervals
Arrays.sort(intervals, (i1, i2) -> Integer.compare(i1[0], i2[0]));

List<Interval> intervals
intervals.sort((i1, i2) -> Integer.compare(i1.start, i2.start));


List<String> ans = new ArrayList<>();
ans.add();

// 初始化list
List<Integer> list = new ArrayList<>(Arrays.asList(1, 2, 3));
int result = list.stream().reduce(1, (subTotal, element) -> subTotal + element);
System.out.println(result);

// List to Array
List<Integer> list = List.of(1, 2, 3);
Integer[] arr = new Integer[b2.size()];
arr = list.toArray(arr);


// 快速填充array
int[] a2 = new int[5];
Arrays.fill(a2, 1);
        
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
int max = Collections.max(Arrays.asList(num)); 

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

public static void main(String[] args) {
    Map<Person, Integer> map = new TreeMap<>(new Comparator<Person>() {
        public int compare(Person p1, Person p2) {
            return p1.name.compareTo(p2.name);
        }
    });
 

// Queue 
Queue<Character> queue = new LinkedList<>();
queue.contains(c);
queue.poll();
queue.offer(c);
queue.size();
queue.peek();
// Stack
Deque<String> stack = new LinkedList<String>();
stack.push("a");
stack.peek();
stack.pop();
stack.isEmpty();

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

// Priority Queue

Queue<ListNode> queue= new PriorityQueue<ListNode>(lists.size(),new Comparator<ListNode>(){
    @Override
    public int compare(ListNode o1,ListNode o2){
        if (o1.val<o2.val)
            return -1;
        else if (o1.val==o2.val)
            return 0;
        else 
            return 1;
    }
});

Queue<Map.Entry<String, Integer>> pq = new PriorityQueue<>(
                 (a,b) -> a.getValue()==b.getValue() ? b.getKey().compareTo(a.getKey()) : a.getValue()-b.getValue()
        );
        
queue.add(node);
queue.poll();

// Dequeue
https://www.liaoxuefeng.com/wiki/1252599548343744/1265122668445536 
Deque<String> deque = new LinkedList<>();
deque.offerLast("A"); // A
deque.offerLast("B"); // B -> A
deque.offerFirst("C"); // B -> A -> C
deque.peekFirst()
deque.peekLast()

```

Java 8 Steam  
https://www.runoob.com/java/java8-streams.html  

```java
List<Integer> intList = Arrays.asList(1, 2, 3);
String result = intList.stream().map(n -> String.valueOf(n)).collect(Collectors.joining("-", "{", "}"));
// output: {1-2-3}

```
