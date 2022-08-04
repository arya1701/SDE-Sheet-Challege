```c++
#include<bits/stdc++.h>
using namespace std;
vector<int> mergeKSortedArrays(vector<vector<int>>&arr, int k)
{
    // Write your code here.
    vector<int> ans;
    for(int i =0; i<arr.size(); i++){
        
        for(int x : arr[i])
            ans.push_back(x);
    }
    sort(ans.begin(),ans.end());
    return ans;
}

```

### Using heap

```c++
#include<bits/stdc++.h>
using namespace std;
vector<int> mergeKSortedArrays(vector<vector<int>>&arr, int k)
{
    // Write your code here.
    vector<int> ans;
    
    priority_queue<int, vector<int>, greater<int>> pq;
    for(int i =0; i<arr.size(); i++){
        
        for(int x : arr[i])
            pq.push(x);
    }
    while(pq.size()>0){
        ans.push_back(pq.top());
        pq.pop();
    }
    return ans;
}
```
