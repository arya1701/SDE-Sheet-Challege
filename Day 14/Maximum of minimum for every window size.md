### Brute Force

```c++
vector<int> maxMinWindow(vector<int> a, int n) {
    // Write your code here.
    vector<int> res;
    vector<int> temp;
    for(int i = 1; i<=n; i++){
        int max_ele = INT_MIN;
        
        for(int j = 0; j<=n-i; j++){
            int mini = a[j];
            
            for(int k = 1; k<i; k++){
                
                if(a[j+k] < mini)
                    mini = a[j+k];
            }
            if(mini > max_ele)
                max_ele = mini;
        }
        res.push_back(max_ele);
    }
    return res;
    
    
}
```
Time - o(n^3)

### Efficient approach
