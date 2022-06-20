## Find the majority element. A majority element is an element that occurs more than floor('N' / 2) times in the array.

### Approach 1: Brute force

Start iterting from the array and count the frequency of the ele and check it'sgreater than N/2 times then return. If not repeat the process.


Time - o(n<sub>2</sub>) </br>
space - o(1)

### Approach 2: Using the hash map
```c++
#include <bits/stdc++.h> 
int findMajorityElement(int arr[], int n) {
	// Write your code here.
    unordered_map<int,int>mp;
    for(int i = 0;i<n;i++)
        mp[arr[i]] ++;
    for(auto it: mp){
        if(it.second > floor(n/2))
            return it.first;
    }
    return -1;
}
```

Time - o(NlogN) hashmap </br>
space - o(N)

### Appraoch 3: Moore's Algorithm

```c++
#include <bits/stdc++.h> 
int findMajorityElement(int arr[], int n) {
	// Write your code here.
    
    int count = 0;
    int ele = 0;
    
    for(int i = 0;i<n;i++){
        if(count == 0)
            ele = arr[i];
        if(ele == arr[i])
            count++;
        else
            count--;
    }
    // now count the freq of the majority elements
    count = 0;
    for(int i =0; i<n; i++)
        if(arr[i] == ele)
            count++;
    return count>n/2 ? ele:-1;
}
```
