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
### Another way
```c++
#include<bits/stdc++.h>
using namespace std;
class pqueue{
    public:
        int ele; //key
        int freq; // val
};
struct comp{
    bool operator()(pqueue a, pqueue b){
        return a.freq < b.freq;
    }
};

vector<int> KMostFrequent(int n, int k, vector<int> &arr)
{
    // Write your code here.
    
    vector<int> ans;
    priority_queue<pqueue,vector<pqueue>,comp> pq;
    
   unordered_map<int,int> mp;
    
    for(int i = 0;i<n; i++)
        mp[arr[i]]++;
    for(auto x: mp){
        pq.push({x.first, x.second});
    }
    while(ans.size() != k){
        pqueue temp = pq.top();
        int elem = temp.ele;
        int elefreq = temp.freq;
        ans.push_back(elem);
        pq.pop();
    }
    sort(ans.begin(),ans.end());
    return ans;
}
```
