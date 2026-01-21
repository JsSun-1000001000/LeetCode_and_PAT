## [面试题 02.07. 链表相交 - 力扣（LeetCode）](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/)
一定要注意==**链表相交是指针相同，不是值相同**==
```cpp
/**

 * Definition for singly-linked list.

 * struct ListNode {

 *     int val;

 *     ListNode *next;

 *     ListNode(int x) : val(x), next(NULL) {}

 * };

 */

class Solution {

public:

    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {

        ListNode* curA = headA;

        ListNode* curB = headB;

  

        //链表交点是指针相等 不是数值相等

        //先求长度

        int lenA = 0;

        int lenB = 0;

        while(curA != NULL){

            lenA++;

            curA = curA->next;

        }

        while(curB != NULL){

            lenB++;

            curB = curB->next;

        }

        //重新回到头节点

        curA = headA;

        curB = headB;

        //不知道lenAB大小默认长的给A

        if(lenB > lenA){

            swap(lenA,lenB);

            swap(curA,curB);

        }

        //长度差

        int gap = lenA - lenB;

        while(gap--){

            curA = curA->next;

        }

        //同时向后

        while(curA != NULL){

            if(curA == curB){

                return curA;

            }

            curA = curA->next;

            curB = curB->next;

        }

        return NULL;

    }

};
```