## Given a linked list, Construct a deep copy of the list.

### Approach 1: Brute force using Hash map 

Hashmap <node,node> to keep track of deep copy node or the original node

- Traverse the given linked list
- create a similar node, without assign any next and random pointer ans store them in the hash map
- Traverse again in the original list and check its next pointer pointing to and random pointer. Assign next and random pointer by checking its deep copy.

Time - O(N) + O(N) </br>
Space - o(N)

### Approach 2: Optimal

steps:

```c++
#include <bits/stdc++.h> 
LinkedListNode<int> *cloneRandomList(LinkedListNode<int> *head)
{
    // step 1 - create deep copy
    LinkedListNode<int> *iter = head;
    LinkedListNode<int> *front = head;
    while(iter != NULL){
        front = iter->next;
        // creating the deep copy of the current node
        LinkedListNode<int> *copy = new LinkedListNode<int> (iter->data);
        // connecting the deep copy
        iter->next = copy;
        copy->next = front;
        // move the iter pointer & repeat the process untill iter!= NULL
        iter = front;
    }
    // step 2 - pointing the dummy pointer
    iter = head;
    while(iter != NULL){
        if(iter->random != NULL){
            // iter.next means deep copy and its random pointer --> iter.random means orginal and its next 
            iter->next->random = iter->random->next;
        }
        // move iter next to next because we have to move to original node
        iter = iter->next->next;
    }
    
    // step 3: differentiate both the list mean get both list back
    iter = head;
    LinkedListNode<int> *dummy = new LinkedListNode<int> (0);
    LinkedListNode<int> *temp = dummy;
    
    while(iter != NULL){
        front = iter->next->next;
        
        // extract the deep copy list
        temp->next = iter->next;
        iter->next = front;
        // move pointer
        temp = temp->next;
        iter = iter->next;
    }
    return dummy->next;
 
}
```
Time - 0(N) + O(N) + O(N), for create node, for assign random pointer, for seperated original and deep copy </br>
Space - O(1)
