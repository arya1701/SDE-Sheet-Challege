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

### Recursive Appraoch
- Start with a curr node as head
- if curr is null then return
- if curr's next element is null, make this node as a head because the last node will be the head, return
- Recursively traverse the list
- Set curr ->next ->next = curr
- Set curr ->next = null

```c++
#include <bits/stdc++.h> 
LinkedListNode<int> *reverseLinkedList(LinkedListNode<int> *head) 
{
    // Write your code here
    if(head == NULL || head->next == NULL){
        return head;
    }
    LinkedListNode<int> *newhead = reverseLinkedList(head->next);
    head->next->next = head;
    head->next = NULL;
    return newhead;
}
```
```c++
#include <bits/stdc++.h> 
LinkedListNode<int> *reverseLinkedList(LinkedListNode<int> *head) 
{
    // Write your code here
    if(head == NULL || head->next == NULL){
        return head;
    }
    LinkedListNode<int> *newhead = reverseLinkedList(head->next);
    LinkedListNode<int> *headnext = head->next;
    headnext->next = head;
    head->next = NULL;
    return newhead;
}
```
