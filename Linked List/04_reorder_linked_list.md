# Reorder Linked List

You are given the head of a singly linked-list.
The positions of a linked list of `length = 7` for example, can initially be represented as:
`[0, 1, 2, 3, 4, 5, 6]`
Reorder the nodes of the linked list to be in the following order:
`[0, 6, 1, 5, 2, 4, 3]`
Notice that in the general case for a list of `length = n` the nodes are reordered to be in the following order:
`[0, n-1, 1, n-2, 2, n-3, ...]`
You may not modify the values in the list's nodes, but instead you must reorder the nodes themselves.

#### Approach
Use **slow and fast pointers** to find the middle of the linked list. **Reverse** the second half of the list starting from the middle. **Merge** the two halves alternately — one node from the first half, then one from the reversed second half. Perform all operations **in-place** using pointer manipulation (O(1) space, O(n) time)

```python
class Solution:
    def reorderList(self, head: Optional[ListNode]) -> None:
        # find middle
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        # reverse second half
        prev, cur = None, slow.next
        slow.next = None
        while cur:
            nxt = cur.next
            cur.next = prev
            prev = cur
            cur = nxt
        # merge both halves
        first, second = head, prev
        while second:
            t1, t2 = first.next, second.next
            first.next = second
            second.next = t1
            first, second = t1, t2
```

**TC : O(n)**
**SC : O(1)**
