# Merge Two Sorted Linked Lists

You are given the heads of two sorted linked lists `list1` and `list2`. Merge the two lists into one **sorted** linked list and return the head of the new sorted linked list.

The new list should be made up of nodes from `list1` and `list2`.

#### Approach
Create a `dummy` pointer(node) to head the merged list and `node` pointer to point to the start of the new list. Iteratively compare nodes from list1 and list2, add the smaller one to the list and advance `node` pointer. Once a list is exhausted, add the remainder of the other.

```python
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = node = ListNode()
        while list1 and list2:
            if list1.val <= list2.val:
                node.next = list1
                list1 = list1.next
            else:
                node.next = list2
                list2 = list2.next
            node = node.next
        node.next = list1 or list2
        return dummy.next
```

**TC : O(n+m)**
**SC : O(1)**
