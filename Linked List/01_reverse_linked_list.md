# Reverse Linked List

Given the beginning of a singly linked list `head`, reverse the list, and return the new beginning of the list.

#### Approach
Use pointers for the `prev` `cur`  and `nxt` nodes. In a loop continuously update the next pointer of the `cur` node to point to the `prev` one, then update `cur` to `nxt`, effectively reversing the lists direction one node at a time.

```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        cur = head
        pre = None
        while cur:
            nxt = cur.next
            cur.next = pre
            pre = cur
            cur = nxt
        return pre
```

**TC : O(n)**
**SC : O(1)**
