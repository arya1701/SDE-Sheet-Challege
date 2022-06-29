## An array is given consist positive and negative integers. Return the length of the longest subarray with sum 0.

### Approach 1: Brute force

- Generate all the subarray 
- Find subarray which having sum 0
- return the max length

```C++
#include <bits/stdc++.h> 
int LongestSubsetWithZeroSum(vector < int > arr) {

  // Write your code here
    int maxi = 0;
    int n = arr.size();
    for(int i = 0; i<n; i++){
        
        int sum = 0;
        
        for(int j = i; j<n; j++){
            sum += arr[j];
            if(sum == 0)
                maxi = max(maxi, j-i+1);
        }
    }
    return maxi;

}
```

Time - o(N^3) - some optimization -> o(N^2)

### Approach 2: Optimized approach

```c++
#include <bits/stdc++.h> 
int LongestSubsetWithZeroSum(vector < int > arr) {
    
    // <prefix sum index>
    unordered_map<int,int> mp;
    int sum = 0;
    int maxi = 0;
    for(int i = 0; i<arr.size(); i++){
        
        sum += arr[i];
        if(sum == 0)
            maxi = i+1;
        else{
            // if its exist in the hash map
            if(mp.find(sum) != mp.end()){
                maxi = max(maxi, i - mp[sum]);
            }else
                mp[sum] = i;
        }
    }
    return maxi;
}

Time -  o(NlogN), N for the traversal and logN for the hashmap that we are using </br>
space - o(N)
```
