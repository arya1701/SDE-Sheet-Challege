## Merge Interval

### Approach 1: Brute force

1. Sort the interval
2. Using two loops, first loop for interating over the interval array and another for comparing with next interval and merge.
3. Push into data structure.

```c++
sort(intervals.begin(), intervals.end());
    for(int i = 0; i<intervals.size()-1; i++){
        for(int j = i+1; j<intervals.size(); j++){
            
            if(intervals[i][1] >= intervals[j][0]){
                intervals[i][1] = max(intervals[i][1],intervals[j][1]);
                intervals.erase(intervals.begin() + j);
                j--;
            }   
        }
    }
    return intervals;

```

Time - o(NlogN) + o(N^2)
Space - o(N)

### Approach 2: Optimal 

Simple iterate over the array, if the data structure is empty insert the interval in the data structure.
If the last element in the data structure overlaps with the current interval then we merge the intervals by updating the last element in the data structure, 
and if  not overlap with the last element simply insert it into the data structure.

```c++
vector<vector<int>> ds;
    if(intervals.size() == 0)
        return ds;
    sort(intervals.begin(),intervals.end());
    vector<int> temp = intervals[0];
    
    for(auto it:intervals){
        
        if(it[0] <= temp[1]){
            temp[1] = max(it[1],temp[1]);
        }else{
            ds.push_back(temp);
            temp = it;
        }
    }
    ds.push_back(temp);
    
    return ds;
```
Time- o(NlogN) + o(N)
space - o(N)

#### Intuition: 
Because we have sorted the intervals, the intervals which will be merging are bound to be adjacent and We kept on merging simultaneously 
as we were traversing through the array and when the element was non-overlapping then inserted the element in the data structure.

### Appraoch 3: without using extra space

```c++
 int count = 0;
    if(intervals.size() == 0)
        return intervals;
    sort(intervals.begin(),intervals.end());
    for(int i = 1; i<intervals.size(); i++){
        
        if(intervals[count][1] >= intervals[i][0])
            intervals[count][1] = max(intervals[count][1],intervals[i][1]);
        else
            intervals[++count] = intervals[i];
    }
    while(intervals.size() != count+1){
        intervals.pop_back();
    }
    
    return intervals;
```
Time - o(NlogN) + o(N)
space - o(1)
