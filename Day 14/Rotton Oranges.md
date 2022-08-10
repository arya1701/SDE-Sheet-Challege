```c++
#include<bits/stdc++.h>
int minTimeToRot(vector<vector<int>>& grid, int n, int m)
{
    // Write your code here. 
    
    queue<pair<pair<int,int>, int>> q;
    // i, j, time
    int vis[n][m];
    int countFreshOrange = 0;
    for(int i = 0; i<n; i++){
        for(int j = 0; j<m; j++){
            
            if(grid[i][j] == 2){
                q.push({{i,j},0});
                vis[i][j] = 2;
            }else
                vis[i][j] = 0;
            if(grid[i][j] == 1)
                countFreshOrange++;
        }
    }
    
    int ans = 0;
    int drow[] = {-1,0,+1,0};
    int dcol[] = {0,1,0,-1};
    int cnt = 0;
    while(!q.empty()){
        int r = q.front().first.first;
        int c = q.front().first.second;
        int t = q.front().second;
        q.pop();
        ans = max(ans,t);
        
        for(int i = 0;i <4; i++){
            int newr = r + drow[i];
            int newc = c + dcol[i];
            
            if(newr >= 0 && newc >= 0 && newr <n && newc <m && vis[newr][newc]  == 0 && grid[newr][newc] == 1){
                
                q.push({{newr,newc}, t+1});
                vis[newr][newc] = 2;
                cnt++;
                   
            }
        }
    }
    if(countFreshOrange != cnt)
            return -1;
        return ans;
}
```
Time - o(N+M) </br>
Space - o(N+M)
