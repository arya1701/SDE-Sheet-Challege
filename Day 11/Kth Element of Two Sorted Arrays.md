```c++
#include<bits/stdc++.h>
using namespace std;
int ninjaAndLadoos(vector<int> &row1, vector<int> &row2, int n, int m, int k) {
    // Write your code here.
    
    if(n<m)
        return ninjaAndLadoos(row2,row1,m,n,k);
    int low = max(0,k-m); // assuming we have to take something from arr1
    int high = min(k,n); // assuming we can't take all the ele from arr2
    
    while(low <= high){
        int cut1 = (low+high)>>1;
        int cut2 = k - cut1;
        
        int l1 = cut1 == 0 ? INT_MIN: row1[cut1-1];
        int l2 = cut2 == 0 ? INT_MIN: row2[cut2-1];
        int r1 = cut1 == n ? INT_MAX: row1[cut1];
        int r2 = cut2 == m ? INT_MAX: row2[cut2];
 
        if(l1<=r2 && l2<=r1)
            return max(l1,l2);
        else if(l1>r2)
            high = cut1-1;
        else
            low = cut1+1;
    }
    return 1;
}
```
Time - o(log2(min(m,n))
