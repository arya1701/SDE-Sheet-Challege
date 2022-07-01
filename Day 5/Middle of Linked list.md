### Given the head of a singly linked list, return the middle node of the linked list. If there are two middle nodes, return the second middle node.

### Approach 1: Bute force

- count the no of nodes
- Iterate again and return the middle node ( countofNode/2 )



Time - o(N) + o(N/2), for count the no of nodes and iterate to middle of the node respectively </br>
Space - o(1)

### Approach 2: Two pointer method (Tortoise method)

- Two pointer slow and fast, initially both are at the head
- Start iterating through the linked list, move the slow by 1 and fast by 2, the moment fast reach at last or cross the boundary - STOP
- return slow
```c++
ListNode* middleNode(ListNode* head) {
        ListNode *s = head;
        ListNode *f = head;
        while(f != NULL && f->next != NULL)
        {
            f = f->next->next;
            s = s->next;
        }
        return s;
        
    }
```
Time - o(N/2) because at max fast will move N/2 times. </br>
Space - o(1)
