### Given a Linked List of size N, where every node represents a sub-linked-list and contains two pointers:

(i) a next pointer to the next node,
(ii) a bottom pointer to a linked list where this node is head.

Each of the sub-linked-list is in sorted order.
Flatten the Link List such that all the nodes appear in a single level while maintaining the sorted order


### Approach 1: Using merge sort technique

- We will recurse until the head pointer moves null. The main motive is to merge each list from the last.
- Merge each list chosen using the merge algorithm.
```c++
#include <bits/stdc++.h> 

Node* Merge(Node* a, Node* b){
    Node* temp = new Node(0);
    Node* res = temp;
    
    while(a != NULL && b != NULL){
        
        if(a->data < b->data){
            temp-> child = a;
            temp = temp->child;
            a = a->child;
        }else{
            temp-> child = b;
            temp = temp->child;
            b = b->child;
        }
    }
    if(a)
        temp -> child = a;
    if(b)
        temp -> child = b;
    res->child->next = NULL;
    return res->child;
    
}

Node* flattenLinkedList(Node* root) 
{
	// base case
    if(root == NULL || root->next == NULL)
        return root;
    root->next = flattenLinkedList(root -> next);
    
    // now merge
    root = Merge(root, root->next);
    return root;
}

```

Time: O(N), where N is the total number of nodes present </br>
Space: O(1)
