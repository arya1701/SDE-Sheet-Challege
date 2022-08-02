```c++
vector<int> minHeap(int n, vector<vector<int>>& q) {
    // Write your code here.
    priority_queue<int,vector<int>,greater<int>>pq;
    vector<int>ans;
    for(auto &it: q){
        if(it[0] == 1){
            auto ele = pq.top();
            ans.push_back(ele);
            pq.pop();
        }
        else{
            pq.push(it[1]);
        }
    }
    return ans;
    
}

```
Time - o(logN)
