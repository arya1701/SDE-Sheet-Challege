### Same as maximum meetings in a room.
Please refer: [https://github.com/arya1701/SDE-Sheet-Challenge/blob/main/Day%208/Maximum%20meetings.md]

```c++
#include <bits/stdc++.h>
using namespace std;
struct meeting{
    int start;
    int end;
    int pos;
};
bool static comparator(meeting m1, meeting m2){
    if(m1.end < m2.end)
        return true;
    else if(m1.end > m2.end)
        return false;
    else if(m1.pos < m2.pos)
        return true;
    else
        return false;
}
int maximumActivities(vector<int> &start, vector<int> &end) {
    // Write your code here.
    // Write your code here.
    vector<int> ans;
    int n = start.size();
    meeting ds[n];
    
    // putting into the data structure
    for(int i = 0; i<n; i++){
        ds[i].start = start[i];
        ds[i].end = end[i];
        ds[i].pos = i+1;
    }
    
    // sort acc to their finishing time
    sort(ds,ds+n, comparator);
    
    // traversing the ds
    int lastMeetingEndTime = ds[0].end;
    
    // 1st meeting always be performed
    ans.push_back(ds[0].pos);
    
    // traversing from 2nd meeting
    for(int i = 1; i<n; i++){
        if(ds[i].start >= lastMeetingEndTime){
            lastMeetingEndTime = ds[i].end;
            ans.push_back(ds[i].pos);
        }
    }
    
    return ans.size();
}
```
TIme - o(N) + o(NlogN) + o(N). for traversing both array and put in the data structure, for sort, traverse through the data structure </br>
Space - o(N)
