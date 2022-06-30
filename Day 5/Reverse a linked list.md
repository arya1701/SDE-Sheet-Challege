### Given a singly linked list of integers. Return the head of the reversed linked list.

```c++
#include <bits/stdc++.h> 
LinkedListNode<int> *reverseLinkedList(LinkedListNode<int> *head) 
{
    // Write your code here
    LinkedListNode<int> *temp = NULL;
    
    while(head != NULL){
        LinkedListNode<int> *next = head->next;
        head->next = temp;
        temp = head;
        head = next;
    }
    return temp;
    
}
```
Time - o(N) </br>
Space - o(1)
