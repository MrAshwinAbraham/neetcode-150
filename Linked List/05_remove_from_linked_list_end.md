# Remove Node From End of Linked List

You are given the beginning of a linked list `head`, and an integer `n`.
Remove the `nth` node from the end of the list and return the beginning of the list.

#### Approach 1
Create a `dummy node` before the head to handle edge cases. Move the `fast` pointer `n` steps ahead. Move both `fast` and `slow` together until `fast` reaches the end. Delete the node after `slow` and return `dummy.next`. Can solve in a single pass, slightly more optimal.

```python
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        fast, slow = dummy, dummy
        for _ in range(n):
            fast = fast.next
        while fast.next:
            slow = slow.next
            fast = fast.next
        slow.next = slow.next.next
        return dummy.next
```

**TC : O(n)**
**SC : O(1)**

#### Approach 2
Traverse the list once to count total nodes. Compute the position of the node to delete from the start `(length - n + 1)`. If it’s the first node, return `head.next`. Otherwise, traverse to the node just before it and relink pointers to skip the target node.

```python
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        cur = head
        length = 0
        while cur:
            cur = cur.next
            length += 1
        target_pos = length - n + 1
        if target_pos == 1:
            return head.next
        cur = head
        pos = 1
        while pos < target_pos -1:
            cur = cur.next
            pos += 1
        cur.next = cur.next.next
        return head
```

**TC : O(n)**
**SC : O(1)**   
