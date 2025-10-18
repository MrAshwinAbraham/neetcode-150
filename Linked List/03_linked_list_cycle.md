# Linked List Cycle Detection

Given the beginning of a linked list `head`, return `true` if there is a cycle in the linked list. Otherwise, return `false`. There is a cycle in a linked list if at least one node in the list can be visited again by following the `next` pointer.

Internally, `index` determines the index of the beginning of the cycle, if it exists. The tail node of the list will set it's `next` pointer to the `index-th` node. If `index = -1`, then the tail node points to `null` and no cycle exists.

#### Approach 1
Use 2 pointers `slow` and `fast` to check if they point to the same node at any point, if so return `true` else return `false`.

```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True
        return False
```

**TC : O(n)**
**SC : O(1)**

#### Approach 2
Use `set`, Iterate to check if the `cur` node in the `set`, if so return `true` otherwise add `cur` to set. If it exits the loop return `false`.

```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        visited = set()
        cur = head
        while cur:
            if cur in visited:
                return True
            visited.add(cur)
            cur = cur.next
        return False
```

**TC : O(n)**
**SC : O(n)**
