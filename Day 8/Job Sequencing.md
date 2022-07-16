## Given a set of N jobs where each job comes with a deadline and profit. Find the number of jobs done and the maximum profit that can be obtained. Each job takes a single unit of time and only one job can be performed at a time.

### Approach - 
- maximize profit achieved with the higher profits. So
- Sort the profit in the decreasing order
- take a array of max days needed and initialize with the -1
- For every job check if it can be performed on its last day.
- If possible mark that index with the job id and add the profit to our answer. 
- If not possible, loop through the previous indexes until an empty slot is found.


Intuition - we try to complete the jobs on the last day so that we can do another jobs in the previous days.
```c++
#include<bits/stdc++.h>

static bool comparator(vector<int>a, vector<int> b){
    return a[1] > b[1];
}

int jobScheduling(vector<vector<int>> &jobs)
{
    // Write your code here
    int n = jobs.size();
    sort(jobs.begin(), jobs.end(), comparator);
    
    int maxDay = jobs[0][0];
    for(int i = 1; i<n; i++)
        maxDay = max(maxDay,jobs[i][0]);
    int maxProfit = 0;
    vector<int> days(maxDay+1, -1);
//     memset(Days,-1, sizeof(Days));
    for(int i = 0; i<n; i++){
        // find the day untill we can complete that job
        for(int j = jobs[i][0]; j>0; j--){
            
            if(days[j] == -1)// no job completed on this day
            {
                days[j] = 1; // jobs done on this job
                maxProfit += jobs[i][1];
                break;
            }
        }
    }
    return maxProfit;
}

```


Time - o(nlogn) + o(NxM), for sorting, O(N*M) since we are iterating through all N jobs and for every job we are checking from the last deadline, say M deadlines in the worst case. </br>
Space - o(M)
