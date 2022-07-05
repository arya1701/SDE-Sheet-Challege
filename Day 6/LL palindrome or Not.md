## Given the head of a singly linked list, return true if it is a palindrome.

### Approach 1: Brute force
- Take all the element and put it into the temp array and then check it's pallindrome or not
and how to check palindrome or not ?

compare current index(i) with (n-i-1)
```c++
bool isPalindrome(node* head) {
    vector<int> arr;
    while(head != NULL) {
        arr.push_back(head->num);
        head = head->next;
    }
    for(int i=0;i<arr.size()/2;i++) 
        if(arr[i] != arr[arr.size()-i-1]) return false;
    return true;
}
```
Time - o(N) + O(N), for putting all the ele into the array, for checking the palindrome </br>
Space - O(N)

### Approach 2: Using two pointers, optimized
- Take two pointers, slow and fast
- Find the middle of the LL
- - Slow & fast, the moment fast pointer reach last node or the second last node - stop
- - if even length take the left node as middle
- reverse the right half of the ll
- increment slow by 1
- take a dummy node at place at head
- start traversing & move dummy and slow together and compare the node value

```c++
ListNode* reverseRightHalf(ListNode* head){
        ListNode* prev = NULL;
        ListNode* next = NULL;
        while(head!= NULL){
            next = head->next;
            head->next = prev;
            prev = head;
            head = next;
        }
        return prev;
    }
    bool isPalindrome(ListNode* head) {
        
        // find the middle of the linked list
        ListNode* slow = head;
        ListNode* fast = head;
        
        while(fast->next != NULL && fast->next->next != NULL){
            slow = slow->next;
            fast = fast->next->next;
        }
        
        // reverse the right half of the linked list i.e after the slow
        
        slow->next = reverseRightHalf(slow->next);
        
        // move slow by 1
        slow = slow ->next;
        
        // now compare the first and second half
        ListNode* dummy = head;
        while(slow != NULL){
            if(dummy->val != slow->val)
                return false;
            dummy = dummy->next;
            slow = slow->next;
            
        }
        return true;        
        
    }
```
Time - o(N/2) + O(N/2) + O(N/2), for finding the middle, for reverese the right half, compare the left and right half </br>
Space - o(1)
