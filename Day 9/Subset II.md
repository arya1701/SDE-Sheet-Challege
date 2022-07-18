## Given an integer array nums that may contain duplicates, return all possible subsets (the power set). The solution set must not contain duplicate subsets. Return the solution in any order.


### Approach 1: Brute force

For every index, two choice whether to pick or not pick the element at that index. This will help us in generating all possible combinations but does not take care of the duplicates.
Hence we will use a set to store all the combinations that will discard the duplicates.

Time - O( 2^n *(m log (m) )). 2^n  for generating every subset and m* log(m)  to insert into set where m = 2^N. After this, we have to convert the set of combinations back into a list of list /vector of vectors which takes more time.

Space - O(2^n * k) to store every subset of average length k. 


### Approach 2: Optimal

We are trying to generate of 0 size list at the first level, then 1 size at the 2nd level and so on ...
so everytime we call recursion, the sublist we are getting is one of the subset, avoid duplicates

```
    ds -> data structure of size s
    f(index,ds)
        | if we pick any ith index then in the next recusion call it will be i+1 and it ranges from (i = index to n-1) ds.add(arr[i])
        | next recursion call
    f(i+1,ds+1)
```

```c++

#include<bits/stdc++.h>
using namespace std;

void recursive(int n, int index, vector<int> &nums, vector<vector<int>> &ans, vector<int> &ds){
    ans.push_back(ds); // put empty ds
    
    for(int i = index; i<n; i++){
        // if we not picking, if curr equal to previous , for the first time we pick that index and after that we didn't pick that same element
            if(i!= index && nums[i] == nums[i-1])
                continue;
            
            // if we pick that index so put that into our data structure 
            ds.push_back(nums[i]);
            recursive(n,i+1,nums,ans,ds);
            // remove the ele that we added, because we would not want in the next recursion
            ds.pop_back();
    }
}

vector<vector<int>> uniqueSubsets(int n, vector<int> &arr)
{
    // Write your code here.
    vector<vector<int>> ans; // to store the answer store all the subsets
    vector<int> ds;  // empty data structure
    
    sort(arr.begin(),arr.end());
    recursive(n,0,arr,ans,ds);
    
    return ans;
    
}
```

TIme - o(2^N x K), for generating every subset, and put into the some ds, K is the average size of the subset </br>\
Space - o(2^Nx K), to store every subset of average length k. Auxiliary space is O(n)  if n is the depth of the recursion tree.
