## Add Two Numbers(leetcode 2):
### You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.You may assume the two numbers do not contain any leading zero, except the number 0 itself.

#### Example 1:
    Input: l1 = [2,4,3], l2 = [5,6,4]
    Output: [7,0,8]
    Explanation: 342 + 465 = 807.
#### Constraints:
    1)The number of nodes in each linked list is in the range [1, 100].
    2)0 <= Node.val <= 9
    3)It is guaranteed that the list represents a number that does not have leading zeros.
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### approach and thinking for this problem :
    ->first of all it is said that the digits are stored in reverse order in memory ; if l1=[2,4,3] then in memory the linked list appears as 3->4->2. and l2=[5,6,4] ,represented as 4->6->5. 
    -> now the problem says to add the numbers and return the sum as a linked list.
    so if we take sum of these numbers as 342+564 =807. then as the queston says it in memory it saves as 7->0->8.so we do need to reverse the linked list to sum up.
    -> so simply traverse both lists , sum the digits and return the resultant             linked list .
    -> conditions and variable used : as the questions also says that there is only a single digit possible in a node and if there is two digit comes as a sum of both list nodes then we take carry as we do in normal addition , and do include the carry value in the following node sum. 
    -> we traverse both lists till both becomes null so that each of their node simultaneously sumed up 
    -> corner case: if at last l1 and l2 both are null while traversing but the carry value is not 0 then we must add a new node and give it that carry value .
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## CODE(in java):
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

