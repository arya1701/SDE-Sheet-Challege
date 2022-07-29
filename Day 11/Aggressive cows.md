## This problem is similar to the chess tournament on the conding Ninja codestudio platform.

```c++
bool canPlace(int mid, vector<int> &positions , int n ,  int c){
    // for first cow
    int cord = positions[0];
    int count = 1;
    
    for(int i = 1; i<n; i++){
        if(positions[i] - cord >= mid){ // leep at least mid distance
            count++;
            cord = positions[i];
        }
        if(count == c)
            return true;
    }
    return false;
}
int chessTournament(vector<int> positions , int n ,  int c){
	// Write your code here
    sort(positions.begin(),positions.end());
    int low = 1;
    int high = positions[n-1] - positions[0];
    int res = -1;
    while(low <= high){
        int mid = (low + high)/2;
        
        if(canPlace(mid,positions,n,c)){
            res = mid;
            low = mid + 1;
        }
        else
            high = mid - 1;
    }
    return res;
}
```
Time - o(log<sub>2</sub>N x N)
