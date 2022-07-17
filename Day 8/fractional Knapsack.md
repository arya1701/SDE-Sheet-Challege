## Return the maximum value we can acheive by putting W weight in the bag. We can take fraction of the weight. One item can be picked only one time.

### Approach: Greedy

- sort according to the value/weight in the descending order
- Try to pick the item, if we able to pick the item completely then pick it else take a fraction of that item

```c++
#include<bits/stdc++.h>
using namespace std;

struct item{
    int weight;
    int value;
};
static bool comparator(pair<int,int>A, pair<int,int> B){
    
    double r1 = (double) A.second / (double) A.first;
    double r2 = (double) B.second / (double) B.first;
    return r1 > r2;
}
double maximumValue (vector<pair<int, int>>& items, int n, int w)
{
    // Write your code here.
    // ITEMS contains {weight, value} pairs.
    
    // sort in the decreasing order acc to val/weight
    sort(items.begin(),items.end(),comparator);
    int currWeight = 0;
    double ans = 0.0;
    int N = items.size();
    for(int i = 0; i<N; i++){
        
        if(currWeight + items[i].first <= w){
            currWeight += items[i].first;
            ans += items[i].second;
        }else{
            // taking the fraction
            
            int remaining = w - currWeight;
            // remaining * current (val/weight) and add into the ans
            
            ans += ((double)remaining/(double)items[i].first)*items[i].second;
            break;
        }
    }
    return ans;       
}
```

Time - o(nlogn) + o(n) </br>
Space - o(1)
