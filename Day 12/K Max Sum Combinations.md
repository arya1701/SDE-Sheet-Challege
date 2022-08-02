```c++
#include<bits/stdc++.h>
using namespace std;

class pqueue{
    public:
    int val, idx,jdx;
};
// max priority queue
struct comp{
    bool operator()(pqueue a, pqueue b){
        return a.val < b.val;
    }
};


vector<int> kMaxSumCombination(vector<int> &a, vector<int> &b, int n, int k){
    sort(a.begin(),a.end());
    sort(b.begin(),b.end());
    
    priority_queue< pqueue, vector<pqueue>, comp> pq;
    vector<int> ans;
    
    set<pair<int,int>> s;
    pq.push({a[n-1] + b[n-1], n-1, n-1});
    s.insert({n-1,n-1});
    
    while(ans.size() != k){
        pqueue temp = pq.top();
        pq.pop();
        
        int val = temp.val;
        int i = temp.idx;
        int j = temp.jdx;
        ans.push_back(val);
        // check in the set, it should not be in the set
        if(i > 0 && s.count({i-1,j}) == 0){
            pq.push({a[i-1] + b[j],i-1,j});
            s.insert({i-1,j});
        }
        if(j > 0 && s.count({i,j-1}) == 0){
            pq.push({a[i] + b[j-1],i,j-1});
            s.insert({i,j-1});
        }
    }
    return ans;
    
}
```

```c++
#include<bits/stdc++.h>
using namespace std;
vector<int> kMaxSumCombination(vector<int> &a, vector<int> &b, int n, int k){
	// Write your code here.
    // min heap
    priority_queue<int, vector<int>, greater<int>> pq;
    vector<int>ans(k);
    
    for(int i = 0; i<a.size(); i++){
        for(int j = 0; j<b.size(); j++){
            int sum = a[i] + b[j];
            if(pq.size() < k)
                pq.push(sum);
            else if(sum > pq.top()){
                pq.pop();
                pq.push(sum);
            }
        }
    }
    for(int i = k-1; i>=0; i--){
        ans[i] = pq.top();
        pq.pop();
    }
    return ans;
}
```
