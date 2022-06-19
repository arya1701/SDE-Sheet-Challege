## Find the duplicates from the array

### Approach 1: Using hashing, keeping the count

1. Create a ds that will maintain the count of every elements
2. Traverse that ds again and if there is any ele whose count is greater than 1, that will duplicate element for sure.
3. Return that index.

Note: We can also do this in single traversal.

```c++
vector<int> freq(n,0);
    
    for(int i = 0; i<n ;i++){
        freq[arr[i]] ++;
    }
    for(int i =0; i<freq.size(); i++){
        if(freq[i]>1)
            return i;
    }
```
Using Single loop
```c++
vector<int> freq(n+1,0);
    
    for(int i = 0; i<n ;i++){
        if(freq[arr[i]] == 0)
            freq[arr[i]] ++;
        else
            return arr[i];
    }
```
Time - o(N)
space - o(N)


### Approach 2: Using linked list cyle method (Tortiose Method)

1. Take two pointer, slow and fast. Intially pointing to the starting.
2. Move slow by 1 position, fast by 2 untill that meet. 
3. When they meet, move fast to start position and again start moving slow and fast by 1 untill they meet and when they meet, that will be our answer.

```c++
int slow = arr[0];
    int fast = arr[0]; 
    
    do {
        slow = arr[slow]; // slow move by 1
        fast = arr[arr[fast]]; // fast move by 2
    }while(slow != fast); // untill they meet
    
    // move fast to starting
    fast = arr[0];
    while(slow != fast){
        slow = arr[slow];
        fast = arr[fast];
    }
    return slow;
```

Time - o(N)
space - o(1)
