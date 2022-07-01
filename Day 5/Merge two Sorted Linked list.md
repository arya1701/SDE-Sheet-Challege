## Given two linked sorted lists, merge two sorted linked lists and return them as a sorted list.

### Approach 1: Brute force

- Create a dummy node initially pointing to the null. This will be head of our new merger sorted list. 
- Iterate the new list using pointer and find the smallest among two nodes pointed by the head pointer of both input lists, and store that data in a new list created.
- Move the head pointer to the next node of the list whose value is stored in the new list.
- Repeat the above steps till any one of the head pointers stores NULL.
- Copy remaining nodes of the list whose head is not NULL in the new list.

```c++
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1 == NULL)
            return l2;
        if(l2 == NULL)
            return l1;
        
        ListNode *dummy, *temp;
        temp = new ListNode();
        dummy = temp;
        while(l1 != NULL && l2 != NULL){
            if(l1->val < l2->val){
                dummy->next = l1;
                l1 = l1->next;
            }
            else{
                dummy->next = l2;
                l2 = l2->next;
            }
            dummy = dummy->next;
        }
        if(l1)
            dummy->next = l1;
        if(l2)
            dummy->next = l2;
        
        return temp->next;
        
    }
```

Time - o(N1 + N2) </br>
Space - o(N1 + N2)

### Approach 2: Without using extra space - Optimal
- Create two variable l1 and l2
- l1 - whichever head is smaller, other one is l2
- for every iteration, assign temp = NULL
-   Move l1 till it is smaller than l2
- l1 is always at the smaller value,
- When condition fails i.e l1>l2, temp->next = l2

```C++
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1 == NULL)
            return l2;
        if(l2 == NULL)
            return l1;
        
        if(l1->val > l2->val)
            swap(l1,l2);
        
        ListNode* res = l1;
        
        while(l1 != NULL && l2 != NULL){
            
            ListNode* temp = NULL;
            while(l1 != NULL && l1->val <= l2->val){
                temp = l1;
                l1 = l1->next;
            }
            temp->next = l2;
            swap(l1,l2);
        }
        return res;
    }
```
Time - o(N1 + N2) </br>
Space - o(1)
