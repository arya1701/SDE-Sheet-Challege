```c++
#include<bits/stdc++.h>
using namespace std;
vector<int> slidingWindowMaximum(vector<int> &nums, int &k)
{
    deque<int> dq;
    vector<int> ans;
    
    for(int i = 0; i<nums.size(); i++){
        
        // remove the out of bound
        if(!dq.empty() && dq.front() == i- k)
            dq.pop_front();
        // remove the ele <= arr[i]
        while(!dq.empty() && nums[dq.back()] < nums[i])
            dq.pop_back();
        
        dq.push_back(i);
        // start taking the maximum
        if(i>= k-1)
            ans.push_back(nums[dq.front()]);
    }
    
    return ans;
}
```
Time - o(N) + O(N), for iteration, in total we are removing out of bounds and also removing ele <= arr[i] i.e N

Space - o(K)
