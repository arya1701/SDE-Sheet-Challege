## Start and End time is given, return the maximum no of meetings that can be accomated in the given start and end time.

### Approach 1:  

Sooner the meeting completed, the more chances we have performing much more meetings in that room
- Sort the meetings according to their finishing time, keep maintain the original position
- Take a variable that keep track of the ending time of the last meeting, Initially it would be end time of the first meeting.
- if equals finishing time then sort acc to their meeting number
- Start iterating from the 2nd meeting and compare:
- - if the start time is strictly greater than the last meeting end time, then update last meeting end time with the current meeting end time and increase the count
- - else skip and move ahead

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
vector<int> maximumMeetings(vector<int> &start, vector<int> &end) {
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
        if(ds[i].start > lastMeetingEndTime){
            lastMeetingEndTime = ds[i].end;
            ans.push_back(ds[i].pos);
        }
    }
    
    return ans;
}
```


TIme - o(N) + o(NlogN) + o(N). for traversing both array and put in the data structure, for sort, traverse through the data structure </br>
Space - o(N)
