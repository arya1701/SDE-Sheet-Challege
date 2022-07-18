##  Given a collection of numbers and a target number, find all unique combinations in number array where the numbers sum to target. Each number can only be used once in the combination.

### Approach 1: Brute Force

```

                                    f(ind,target,ds)
                                          |
                                        /   \
             f(ind+1,target-arr[ind],ds)     f(ind+1,target,ds)
             
             if(target>=arr[ind])
             
```

But for unique, we have to use hashset and then put it into the list and return due to this space complexity will increase.

Space - o(2^t x klogn), klogn for putting it into the hashset

### Approach 2: Optimal

we gonna try to use subsequence not pick or not pick method

```c++
#include<bits/stdc++.h>
using namespace std;
void recursive(int n, int index, vector<int> &arr, int target, vector<vector<int>> &ans, vector<int> &ds){
    
    if(target == 0){
        ans.push_back(ds);
        return;
    }
    
    for(int i = index; i<n; i++){
        
        if(i > index && arr[i] == arr[i-1])
            continue;
        if(arr[i] > target)
            break;
        ds.push_back(arr[i]);
        recursive(n,i+1,arr, target - arr[i],ans,ds);
        ds.pop_back();
    }
}

vector<vector<int>> combinationSum2(vector<int> &arr, int n, int target)
{
	// Write your code here.
    sort(arr.begin(),arr.end());
    vector<vector<int>> ans;
    vector<int> ds;
    
    recursive(n,0,arr,target,ans,ds);
    
    return ans;
}

```

Time - o(2^K x K), k is avg length </br>
Space - o(k x X),  if we have X combinations then space will be x*k where k is the average length of the combination
