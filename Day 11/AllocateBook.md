```c++
#include<bits/stdc++.h>
using namespace std;
bool allocationPossible(int mid,vector<int> &time, int n, int k){
    long long allocatedDay = 1;
    long long pages = 0;
    
    for(int i = 0; i<n; i++){
        
        if(time[i] > mid)
            return false;
        if(time[i] + pages > mid){
            allocatedDay += 1;
            pages = time[i];
            if (pages > mid) return false;
        }
        else
            pages += time[i];
    }
    if(allocatedDay > k)
        return false;
    else
        return true;
}
long long ayushGivesNinjatest(int n, int m, vector<int> time) 
{	
	// Write your code here.
//     if (n > m) return -1;
    long long sume = 0;
    
    for(int i = 0; i<m; i++)
        sume += time[i];
    long long low = INT_MIN;
    long long high = sume,mid;
    
    long long res = sume;
    
    while(low <= high){
        mid = low + (high - low) / 2;
        if(allocationPossible(mid,time,m,n)){
            res = mid;
            high = mid - 1;// decrease the barrier move left
        }else
            low = mid + 1; // increase the barrier move right
    }
    return res;
}
```
Time - o(logN x N)
