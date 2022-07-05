## Detect a loop in a linked list.

### Approach 1: Using hash table
- Start iterating through the lists.
- If the current node is present in the hash table already, this indicates the cycle is present in the linked list and returns true.
- Else move insert the node in the hash table and move ahead.
- If we reach the end of the list, which is NULL, then we can say that the given list does not have a cycle in it and hence we return false.

```c++
bool cycleDetect(node* head) {
    unordered_set<node*> hashTable;
    while(head != NULL) {
        if(hashTable.find(head) != hashTable.end()) return true;
        hashTable.insert(head);
        head = head->next;
    }
    return false;
}
```
Time - o(N) </br>
Space - o(N)

### Approach 2: Using fast and slow pointer

- Take two pointer slow and fast, slow move by 1 and fast move by 2.
- If they collide that means there is a loop else no loop return false.

```c++
bool hasCycle(ListNode *head) {
        
        // if a null linked list or a single length linked list
        if(head == NULL || head->next == NULL )
            return false;
        
        ListNode* slow = head;
        ListNode* fast = head;
        
         // if a the last node is null and the second last node is null then we stop
        while(fast->next && fast->next->next){
            fast = fast->next->next;
            slow = slow->next;
            if(fast == slow)
                return true;
        }
        return false;
    }
```
Time - o(N) </br>
Space - o(1)

## Follow up: Find the starting point of the loop

### Approach 1: Using hashing

 - Hash the node, if it's present the move ahead else put that node into the hashmap. and if we reach null that means no cycle 
 - if we reach the same node that was present in the hash map, that is our starting point.

```c++
node* detectCycle(node* head) {
    unordered_set<node*> st;
    while(head != NULL) {
        if(st.find(head) != st.end()) return head;
        st.insert(head);
        head = head->next;
    }
    return NULL;
}
```

### Approach 2: Using slow and fast pointer

continuation of above approach, when the slow and fast pointer colloide, move the fast pointer to the head and now again start moving slow and fast simaltaneously
when then meet, that will be our starting point.

```c++
ListNode *detectCycle(ListNode *head) {
        // if the given linked list is null or only the single node given in the linked list
        
        
        if(head == NULL || head->next == NULL)
            return NULL;
        
        ListNode* slow = head;
        ListNode* fast = head;
        ListNode* entry = head;
        
        while(fast->next && fast->next->next){
            
            slow = slow->next;
            fast = fast->next->next;
            
            if(slow == fast){ // means there is a collision point
                while(slow != entry){
                    slow = slow->next;
                    entry = entry->next;
                }
                return entry;
            }
        }
        // if the loop is over that means there is no cycle so retrun null
        return NULL;
        
    }
```
 Time - o(N) </br>
 space - o(1)
 
