Can be used as a queue, stack or linked list
```java
// Stack
Deque<Integer> s = new ArrayDeque<>();
s.addLast(1);       // 1
s.addLast(2);       // 1,2
s.addLast(3);       // 1,2,3
s.removeLast();     // 1,2
s.removeLast();     // 1

// Queue
Deque<Integer> q = new ArrayDeque<>();
q.addLast(1);       // 1
q.addLast(2);       // 1,2
q.addLast(3);       // 1,2,3
q.removeFirst();    // 2,3
q.removeFirst();    // 3

// LinkedList
Deque<Integer> ll = new ArrayDeque<>();
ll.addLast(1);      // 1
ll.addLast(2);      // 1,2
ll.addFirst(0);     // 0,1,2
ll.removeLast();    // 0,1
ll.removeFirst();   // 1
```

## Methods
- `addFirst(item)` adds to start of deque
- `addLast(item)` adds to end of deque
- `contains(item)` returns boolean if present
- `getFirst()` gets the first item in deque, doesn't remove
- `getLast()` gets the last item in deque, doesn't remove
- `removeFirst()` gets the first item in deque and removes item
- `removeLast()` gets the last item in deque and removes item
- `size()` gets the size of the deque