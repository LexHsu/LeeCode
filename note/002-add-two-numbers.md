Add Two numbers
===

you are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)

Output: 7 -> 0 -> 8


```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *     }
 * }
 */
public class Solution {
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode head = new ListNode(0);
    ListNode p1 = l1, p2 = l2, p = head;
    int c = 0;
    while (p1 != null || p2 != null || c == 1) {
        int add1 = (p1 == null ? 0 : p1.val);
        int add2 = (p2 == null ? 0 : p2.val);
        int k = add1 + add2 + c;
        c =  k / 10;
        p.next = new ListNode(k % 10);
        p = p.next;
        if (p1 != null) {
            p1 = p1.next;
        }
        if (p2 != null) {
            p2 = p2.next;
        }
    }
    return head.next;
}
```
