## Return the minimum no of railway station so that no train is kept waiting.

### Approach 1:


```c++
int calculateMinPatforms(int at[], int dt[], int n) {
    // Write your code here.
    
    sort(at,at+n);
    sort(dt,dt+n);
    
    int i = 1;
    int j = 0;
    
    int currentAcquiredPlatform = 1;
    int maxPlatformNeeded = 1;
    
    while(i<n && j<n){
        
        // if the current arrival time < departure time of the last train
        
        if(at[i] <= dt[j]){
            currentAcquiredPlatform++;
            i++; // moving to the 
        }
        // if the current arrival time > departure time means we can use that 
        // empty platform do platform-- and move to the next departure time
        else if(at[i] > dt[j]){
            currentAcquiredPlatform--;
            j++;
        }
        
        maxPlatformNeeded = max(maxPlatformNeeded,currentAcquiredPlatform);
    }
    return maxPlatformNeeded;
}
```
