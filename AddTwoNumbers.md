## 2. [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/) (Medium)

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse** order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**

```
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

**Example 2:**

```
Input: l1 = [0], l2 = [0]
Output: [0]
```

**Example 3:**

```
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

**Constraints:**

- The number of nodes in each linked list is in the range `[1, 100]`.
- `0 <= Node.val <= 9`
- It is guaranteed that the list represents a number that does not have leading zeros.

### 解题思路
这道题没有太多技巧，就是按照小学时学的算术从低位到高位依次做加法，注意进位的情况就可以，特别是如果当退出循环后还要检查一下是否进位值为1，如果为1的话还要多加一位。另外一个小技巧是可以用一个dummy node作为开始，这样在循环代码的处理中就会方便很多。

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        head = ListNode(0)
        currentNode = head
        carry = 0
        while l1 or l2 or carry > 0:
            currentSum = carry
            if l1:
                currentSum += l1.val
                l1 = l1.next
            if l2:
                currentSum += l2.val
                l2 = l2.next
            carry = currentSum // 10
            currentNode.next = ListNode(currentSum % 10)
            currentNode = currentNode.next
        if carry > 0:
                currentNode.next = ListNode(1)
        return head.next
```
以上解法的时间复杂度是O(n)，因为需要线性遍历两个输入链表，空间复杂度是O(1)。




