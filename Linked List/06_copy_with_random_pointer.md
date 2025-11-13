# Copy Linked List with Random Pointer

You are given the head of a linked list of length `n`. Unlike a singly linked list, each node contains an additional pointer `random`, which may point to any node in the list, or `null`.

Create a **deep copy** of the list.
The deep copy should consist of exactly `n` **new** nodes, each including:
- The original value `val` of the copied node
- A `next` pointer to the new node corresponding to the `next` pointer of the original node
- A `random` pointer to the new node corresponding to the `random` pointer of the original node

Note: None of the pointers in the new list should point to nodes in the original list

#### Approach
Traverse the original list and create a `copy` of each node, storing the mapping of `original → copied node` in a dictionary. Traverse the list again to assign each copied node’s next and random pointers using the dictionary. Return the copied head node from the dictionary.

```python
class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        cur = head
        copyMap = {None : None}
        while cur:
            copy = Node(cur.val)
            copyMap[cur] = copy
            cur = cur.next
        cur = head
        while cur:
            copy = copyMap[cur]
            copy.next = copyMap[cur.next]
            copy.random = copyMap[cur.random]
            cur = cur.next
        return copyMap[head]
```

**TC : O(n)**
**SC : O(n)**
