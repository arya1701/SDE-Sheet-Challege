## Given an array and integer X, return the count of subarray that has XOR of the elements equal to X.

### Approach 1: Brute force
- Generate all the subarray
- For each subarray, find the XOR and if's equal to the given X, increase the count of subarray by 1

```c++
#include <bits/stdc++.h> 
int subarraysXor(vector<int> &arr, int x)
{
    //    Write your code here.
    int ans = 0;
    int n = arr.size();
    for(int i = 0; i<n; i++){
        int xor_ele = 0;
        for(int j = i; j<n; j++){
            xor_ele ^= arr[j];
            if(xor_ele == x)
                ans++;
        }
    }
    return ans;
}
```

Time - o(N^2) </br>
Space - o(1)

### Approach 2: Optimized approach


```c++
#include <bits/stdc++.h> 
int subarraysXor(vector<int> &arr, int x)
{
    //    Write your code here.
    int cnt = 0;
    int xorr = 0;
    int n = arr.size();
    unordered_map<int,int> mp;
    for(int i = 0; i<n; i++){
        xorr ^= arr[i];
        
        if(xorr == x)
            cnt++;
        if(mp.find(xorr ^ x) != mp.end())
            cnt += mp[xorr ^ x];
        mp[xorr] += 1;
    }
    return cnt;
}
```

Time - o(NlogN) </br>
Space - o(N)
