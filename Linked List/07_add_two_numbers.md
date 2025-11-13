# Add Two Numbers

You are given two **non-empty** linked lists, `l1` and `l2`, where each represents a non-negative integer.

The digits are stored in **reverse order**, e.g. the number 321 is represented as `1 -> 2 -> 3 ->` in the linked list.

Each of the nodes contains a single digit. You may assume the two numbers do not contain any leading zero, except the number `0` itself.

Return the sum of the two numbers as a linked list.

#### Approach
Traverse both linked lists, summing corresponding `values` and `carry`. Create new nodes for each `value` of the `sum (total%10)`. Update the `carry` as `total//10`. Continue until both `lists` and `carry` are processed, then return the result list starting from `dummy.next`.

```python
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(0)
        cur= dummy
        carry = 0
        while l1 or l2 or carry:
            val1 = l1.val if l1 else 0
            val2 = l2.val if l2 else 0
            total = val1 + val2 + carry
            carry = total // 10
            total = total % 10
            cur.next = ListNode(total)
            # traversal
            cur = cur.next
            l1 = l1.next if l1 else None
            l2 = l2.next if l2 else None
        return dummy.next
```

**TC : O(m+n)**
**SC : O(1)**
