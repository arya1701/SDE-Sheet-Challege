### Given the heads of two singly linked-lists headA and headB, return the node at which the two lists intersect.

### Approach 1: Brute Force

Common node value does't give us the right answer always, for the intersection point it is the node itself that is the intersection point.
- Start traversing any of the linked list and compare the node itself in the other list, if its is present then return that node else NULL

```c++
//utility function to check presence of intersection
node* intersectionPresent(node* head1,node* head2) {
    while(head2 != NULL) {
        node* temp = head1;
        while(temp != NULL) {
            //if both nodes are same
            if(temp == head2) return head2;
            temp = temp->next;
        }
        head2 = head2->next;
    }
    //intersection is not present between the lists return null
    return NULL;
}
```

Time - o(N*M)

### Approach 2: Hashing - above approach we can optimise the searching using hashing

- Iterate through the list1 and mapped the addresses.
- Iterate the other list and if we find the node there that means that is our intersetion point.

```c++
node* intersectionPresent(node* head1,node* head2) {
     unordered_set<node*> st;
    while(head1 != NULL) {
       st.insert(head1);
       head1 = head1->next;
    }
    while(head2 != NULL) {
        if(st.find(head2) != st.end()) return head2;
        head2 = head2->next;
    }
    return NULL;

}
```
Time - o(N+M) </br>
Space - o(N)

### Approach 3: Difference method 

We can reduce the search length, let see how:
- find the length of both the linked list
- move the dummy pointer to the length difference of longer list
- Now simaltenousy move both the pointer on the two list
- the moment they colloide that is our intersection point.
```c++
node* intersectionPresent(node* head1,node* head2) {
 int diff = getDifference(head1,head2);
        if(diff < 0) 
            while(diff++ != 0) head2 = head2->next; 
        else while(diff-- != 0) head1 = head1->next;
        while(head1 != NULL) {
            if(head1 == head2) return head1;
            head2 = head2->next;
            head1 = head1->next;
        }
        return head1;


}
```
Intuition: Becuase we already covered the extra distance from the longer linked list by moving dummy pointer to the difference length means both the pointer are 
at the same position if there is intersection point then they will colliode for sure else return NULL.

Time - o(M) + O(M-N) + O(N), for finding the length of both the linked list, moving to the difference, traversing respectively </br>
Spave - o(1)

### Approach 4: Optimcal approach


Take two dummy nodes for each list. Point each to the head of the lists.
Iterate over them. If anyone becomes null, point them to the head of the opposite lists and continue iterating until they collide.

```c++
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        
        ListNode* a = headA;
        ListNode* b = headB;
        
        // if a and b having the different length then we will stop the loop after the second iteration
        
        while(a!=b) // untill when both the node are not equal i.e at intersection
        {
            a = a == NULL ? headB:a->next;
            b = b == NULL ? headA:b->next;
        }
        return a;
        
    }
```
Time - same as above
