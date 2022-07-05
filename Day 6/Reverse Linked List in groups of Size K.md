## Given the head of a linked list, reverse the nodes of the list k at a time, and return the modified list.

### Approach 1: Using pointers

In order to solve this problem, pointers play an important role. 

```c++
#include <bits/stdc++.h> 
Node *getListAfterReverseOperation(Node *head, int n, int b[]){
	// Write your code here.
    Node *dummy = new Node(0);
    dummy->next = head;
    
    Node* curr = dummy;
    Node* nex = dummy;
    Node* pre = dummy;
    Node* temp = dummy;
    int count = 0,j=0;
    while(temp->next != NULL){
        temp = temp->next;
        count++;
    }
    while(count > 0 && j<n){
        curr = pre->next;
        nex = curr->next;
        int x = (b[j] <= count ? b[j]: count);
        if(x == 0){
            j++;
            continue;
        }
        for(int i = 1; i<x ;i++){
            curr->next = nex->next;
            nex->next = pre->next ;
            pre->next = nex;
            nex = curr->next;
        }
        pre = curr;
        count -= b[j];
        j++;
    }
    return dummy->next;
}
```
Time - o(N) </br>
Space - o(1)
