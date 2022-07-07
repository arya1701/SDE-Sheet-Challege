## Given the head of a linked list, rotate the list to the right by k places.


### Approach 1: Brute force
- picking up the last node and put it at the front, again pick the last and put it at the front
- Keep doing k times

```c++
#include <bits/stdc++.h> 
Node *rotate(Node *head, int k) {
    if(head == NULL||head->next == NULL) return head;
    
  //putting the last node to the front k times
    for(int i=0;i<k;i++) {
        Node* temp = head;
        while(temp->next != NULL) temp = temp->next;
        Node* end = temp->next;
        temp->next = NULL;
        end->next = head;
        head = end;
    }
    return head;
}
```
Time - o(K*N) </br>
Space - o(1)

### Approach 2: Optimal
- Any multiple of length will always give the original linked list, like k = 5, so for k = 10,15,20, 25 answer will be same.
- This gives us the hint, if k is greater than length of the linked list, we just have to rotate k % length times. 


Steps-

- find the length of the list.
- Connect the last node to the first node, converting it to a circular linked list.
- Get the (length - kth) node points to the NULL
```c++
#include <bits/stdc++.h> 

Node *rotate(Node *head, int k) {
     if(!head || !head->next || k == 0)
            return head;
        
        Node* curr = head;
        int len = 1;
        while(curr -> next){
            len++;
            curr = curr->next;
        }
        
        curr->next = head;
        k = k % len;
        k = len - k;
        while(k--)
            curr = curr->next;
        
        head = curr->next;
        curr->next = NULL;
        
        return head;
}
```


Time - o(N) + O(N- ((N % K)), for find the no of nodes, for traversing </br>
Space - o(1)
