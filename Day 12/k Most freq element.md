```c++
#include<bits/stdc++.h>
using namespace std;

vector<int> KMostFrequent(int n, int k, vector<int> &arr)
{
    // Write your code here.
    
    vector<int> ans;
    priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>> pq;
    
   unordered_map<int,int> mp;
    
    for(int i = 0;i<n; i++)
        mp[arr[i]]++;
    for(auto x = mp.begin(); x != mp.end(); x++){
        pq.push({x->second, x->first});
        
        if(pq.size() > k)
            pq.pop();
        
    }
    while(!pq.empty()){
        ans.push_back(pq.top().second);
        pq.pop();
    }
    sort(ans.begin(),ans.end());
    return ans;
}
```
