## Add Two Numbers(leetcode 2):
#### You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.You may assume the two numbers do not contain any leading zero, except the number 0 itself.

#### Example 1:
    Input: l1 = [2,4,3], l2 = [5,6,4]
    Output: [7,0,8]
    Explanation: 342 + 465 = 807.
#### Constraints:
    1)The number of nodes in each linked list is in the range [1, 100].
    2)0 <= Node.val <= 9
    3)It is guaranteed that the list represents a number that does not have leading zeros.

### approach and thinking for this problem :
    -> first of all, the question says that the digits are stored in reverse order.
    that means if
    l1 = [2,4,3] (linked list looks like 2->4->3) and
    l2 = [5,6,4] (linked list looks like 5->6->4),
    then these lists actually represent the numbers 342 and 465.
    
    -> now we have to add these two numbers and return the result as a linked list.
    342 + 465 = 807.
    since the answer also has to be in reverse order, the final linked list will be
    7->0->8.
    because the digits are already given in reverse order, we do not need to reverse any list.
    
    -> we simply traverse both linked lists together and keep adding the digits one by one.
    
    -> as mentioned in the problem, each node contains only a single digit (0–9).
    when the sum of two digits becomes a two-digit number, we handle it using a carry, just like normal addition.
    
    -> we keep traversing the lists while
    (l1 != null || l2 != null || carry != 0).
    this is because one list can end before the other, and we may still have a carry left.
    
    -> at each step, we first take
    sum = carry,
    then add the current values of l1 and l2 (only if they are not null).
    
    -> after calculating the sum, we create a new node that stores sum % 10.
    the carry for the next step is calculated as sum / 10.
    
    -> for example, if sum = 10,
    carry = 1 and the value stored in the node will be 0.
    
    -> we repeat this process for all nodes until both lists are finished and no carry remains.
    
    -> corner case:
    if both l1 and l2 become null but the carry is still not 0,
    we create one last node and store the carry value in it.

### Time complexity:
    O(max(n, m))
    Why? Let: n = number of nodes in l1 , m = number of nodes in l2
    You traverse each linked list once.
    Each loop iteration does constant work (addition, carry, node creation)
    The loop runs until the longer list ends (plus at most one extra step for carry)
    So the total time depends on the longer of the two lists:
    Time Complexity = O(max(n, m)).
### Space Complexity:
    O(max(n, m)).
    A new linked list is created to store the result
    Its length is at most max(n, m) + 1 (if there is a final carry)
   
### CODE(in java)(Beats >=99 % at submission):
```java
public class ListNode {
    int val;
    ListNode next;

    ListNode() {}
    ListNode(int val) {
        this.val = val;
    }
    ListNode(int val, ListNode next) {
        this.val = val;
        this.next = next;
    }
}

class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode newNode = new ListNode(0);
        ListNode curr = newNode; // dummy head
        int carry = 0;

        while (l1 != null || l2 != null || carry != 0) {
            int sum = carry;

            if (l1 != null) {
                sum += l1.val;
                l1 = l1.next;
            }
            if (l2 != null) {
                sum += l2.val;
                l2 = l2.next;
            }

            carry = sum / 10;
            curr.next = new ListNode(sum % 10);
            curr = curr.next;
        }
        return newNode.next;
    }
}
-------------------------------------------------------------------------------------------------------------

