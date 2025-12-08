# LRU Cache

Implement the Least Recently Used (LRU) cache class `LRUCache`. The class should support the following operations
- `LRUCache(int capacity)` Initialize the LRU cache of size `capacity`.
- `int get(int key)` Return the value corresponding to the `key` if the `key` exists, otherwise return `-1`.
- `void put(int key, int value)` Update the `value` of the `key` if the `key` exists. Otherwise, add the `key`-`value` pair to the cache. If the introduction of the new pair causes the cache to exceed its capacity, remove the least recently used key.

A key is considered used if a `get` or a `put` operation is called on it.
Ensure that `get` and `put` each run in O(1)O(1) average time complexity.

#### Approach
Use a **HashMap** to store `key → node`, enabling O(1) lookup. Maintain a **doubly linked list** where the right end is the most recently used and the left end is the least recently used. On every `get` or `put`, move the accessed node to the MRU end. If capacity is exceeded, evict the node at the LRU end of the list.

```python
class Node:
    def __init__(self, key, val):
        self.key, self.val = key, val
        self.prev = self.next = None

class LRUCache:
    def __init__(self, capacity: int):
        self.cap = capacity
        self.cache = {}
        self.right, self.left = Node(0,0), Node(0,0)
        self.left.next, self.right.prev = self.right, self.left

    def insert(self, node):
        prv, nxt = self.right.prev, self.right
        prv.next = node
        node.prev = prv        
        node.next = nxt
        nxt.prev = node
  
    def remove(self, node):
        prv, nxt = node.prev, node.next
        prv.next = nxt
        nxt.prev = prv

    def get(self, key: int) -> int:
        if key not in self.cache:
            return -1
        node = self.cache[key]
        self.remove(node)
        self.insert(node)
        return node.val

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            self.remove(self.cache[key])
        self.cache[key] = Node(key, value)
        self.insert(self.cache[key])
        if len(self.cache) > self.cap:
            lru = self.left.next
            self.remove(lru)
            del self.cache[lru.key]
```

**TC : O(1)**
**SC : O(n)**
