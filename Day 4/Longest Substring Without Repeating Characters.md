## Given a String, find the length of longest substring without any repeating character.


### Approach 1: Brute force

- Generate all the substring

Time - o(N^3) </br>
Space - o(N) , for hash set which will be required to check for repeating character.


### Approach 2: Optimised using two pointer and Set

- Initially, We will have two pointers left and right,both the pointer are at the starting.
- Range[l-r] has no repeating character and Length = r-l+1
- If s[i] is not present in the set, then insert and increase the right pointer.
- If s[i] is present in the set, means we have to remove untill we found that repeater charater in the set, increase the left pointer and push the current into the set.
```c++
#include <bits/stdc++.h> 
int uniqueSubstrings(string input)
{
    //Write your code here
    int ans = 0;
    int n = input.size();
    unordered_set<int> hs;
    int left = 0;
    for(int right = 0; right <n; right++){
        
        if(hs.find(input[right]) != hs.end()){
            
            while(left < right && hs.find(input[right]) != hs.end()){
                hs.erase(input[left++]);
            }
        }
        hs.insert(input[right]);
        ans = max(ans,right-left+1);
    }
    return ans;
    
}
```

Time - o(2N) becoz one chracter visited twice one by left and right pointer, </br>
Space - o(N) , we use set


### Approach 3: Optimal

Above approach can reduce to o(N) if we anyhow move left pointer directly to element, skipping the duplicate element from the set. So for that purpose we can use map
that will taking care of element with last appeared index. So that we can move our left pointer directly to the last appeared index+1, means we skip that duplicate
element.

```c++
#include <bits/stdc++.h> 
int uniqueSubstrings(string input)
{
    //Write your code here
    int ans = 0;
    int n = input.size();
    unordered_map<char,int> hs;
    int left = 0;
    for(int right = 0; right <n; right++){
        // Checking if we have already seen the element or
        // not
        if(hs.find(input[right]) != hs.end()){
            // If we have seen the number, move the start
            // pointer to position after the last occurrence
            left = max(left, hs[input[right]] + 1);
        }
         // Updating the last seen value of the character
        hs[input[right]] = right;
        ans = max(ans,right - left + 1);
    }
    return ans;
    
}
```

Time - o(N)
Space - o(N)
