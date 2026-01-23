<h1>Problem:</h1>

<h4><a href="https://leetcode.com/problems/linked-list-cycle/description/">Linked List Cycle</a></h4>

Given head, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Return true if there is a cycle in the linked list. Otherwise, return false.
 

Example 1:

<img src="https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png">
Input: head = [3,2,0,-4], pos = 1<br>
Output: true<br>
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).<br>


Example 2:<br>

<img src="https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png">
Input: head = [1,2], pos = 0<br>
Output: true<br>
Explanation: There is a cycle in the linked list, where the tail connects to the 0th node.<br>


Example 3:<br>

<img src="https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png">
Input: head = [1], pos = -1<br>
Output: false<br>
Explanation: There is no cycle in the linked list.<br>


<h1>Solution:</h1>

<h3>The Logic:</h3>

1. If there is no cycle (a straight line): The Fast runner will reach the end (null) before the Slow runner.<br>
2. If there is a cycle (a circular track):<br>
          The Fast runner will eventually lap the Slow runner. Even if they start at different times, because they are moving in a closed loop, the Fast runner is guaranteed to crash into the Slow runner eventually.

<h3>Algorithm Steps:</h3>

1. Initialize two pointers, slow and fast, both pointing to the head.<br>
2. Loop while fast and fast.next are not null:
<ul>
  <ul>
    <li>Move slow one step: slow = slow.next</li>
    <li>Move fast two steps: fast = fast.next.next</li>
<li>Check if slow == fast:</li>
    <ul>
      <li>If they are at the exact same node, they have collided. A cycle exists. Return True.</li>
    </ul>
  </ul>
</ul>
3. If the loop finishes (meaning fast hit null), return False.<br>

<h3>Code:</h3>

<pre>
  /**
  * Definition for singly-linked list.
  * struct ListNode {
  *     int val;
  *     ListNode *next;
  *     ListNode(int x) : val(x), next(NULL) {}
  * };
  */
  class Solution {
  public:
      bool hasCycle(ListNode *head) {
          ListNode* slow = head;
          ListNode* fast = head;
  
          while(fast != NULL && fast->next != NULL){
              slow = slow->next;
              fast = fast->next->next;
  
              if(slow == fast) return true;
          }
          return false;
      }
  };
</pre>
