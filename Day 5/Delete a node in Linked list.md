## Given the address of the node that is to be deleted.

### Approach 1: Brute force

We can access the node after the given nodes but before we can't access
- Copy the next node’s value in the deleted node. Then, link node to next of next node. 
- This does not delete that node but indirectly it removes that node from the linked list.

```c++
void deleteNode(ListNode* node) {
        node->val = node->next ->val;
        node->next = node->next->next;
    }
 ```
Time & Space - O(1)
