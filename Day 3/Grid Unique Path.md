## Find the no of ways to reach source to destination by moving right and down steps. 

### Approach 1: Brute force - using recursion

Soruce [0,0] to Destination [m-1,n-1]



```c++
#include <bits/stdc++.h> 

int recursion(int m, int n, int i, int j){
    // Base case
    if(i == m-1 && j == n-1)
        return 1;
    
    if(i >= m || j >= n)
        return 0;
    return recursion(m, n, i, j+1) + recursion(m, n, i+1, j);
}

int uniquePaths(int m, int n) {
	// Write your code here.
    
    int ans = recursion(m,n,0,0);
    return ans;
}
```
Time - exponential, because we try for all possible combination </br>
Space - exponential, stack space tree

### Appraoch 2: Using DP, Recursive + Memorization

```c++
#include <bits/stdc++.h> 

int solution(int m, int n, int i, int j, vector<vector<int>> &dp){
    if(i == m-1 && j == n-1)
        return 1;
    if(i >= m|| j >= n)
        return 0;
    if(dp[i][j] != -1)
        return dp[i][j];
    
    return dp[i][j] = solution(m, n , i+1, j ,dp) + solution(m, n, i, j+1, dp);
        
}
int uniquePaths(int m, int n) {
	// Write your code here.
    vector<vector<int>>dp(m,vector<int>(n,-1));
    
    return solution(m,n,0,0,dp);
}
```
TC:O(m*n) </br>
SC:O(m*n)

#### Bottom Up Approach 
```c++
#include <bits/stdc++.h> 
int uniquePaths(int m, int n) {
	// Write your code here.
    int dp[m][n];
    
    for(int i = 0; i<m; i++){
        for(int j = 0; j<n; j++){
            
            if(i == 0 || j == 0)
                dp[i][j] = 1;
            else
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
        }
    }
    return dp[m-1][n-1];
}
```
