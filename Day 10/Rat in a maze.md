## Return all the possible paths that the rat can take to reach from the source to destination

```c++
void solve(int i, int j, vector<vector<int> > &maze, int n, vector<vector<int>> &visited, vector<vector<int>> &ans,int di[4],int dj[4]){
    
    if(i == n-1 && j == n-1){
        visited[i][j] = 1;
        vector<int>temp;
        for(int m = 0; m<n; m++){
            for(int k = 0; k<n; k++){
                temp.push_back(visited[m][k]);
            }
        }
        ans.push_back(temp);
        visited[i][j] = 0;
        return;
    }
    
    for(int idx = 0; idx<4 ;idx++){
        int newi = i + di[idx];
        int newj = j + dj[idx];
        
        if(newi >= 0 && newj >= 0 && newi < n && newj < n && !visited[newi][newj] && maze[newi][newj] == 1){
            visited[i][j] = 1;
            solve(newi,newj,maze,n,visited,ans,di,dj);
            visited[i][j] = 0;
        }
    }
    
}

vector<vector<int>> ratInAMaze(vector<vector<int>> &maze, int n){
  // Write your code here.
    vector<vector<int>> visited(n,vector<int>(n,0));
    vector<vector<int>> ans;
    int di[4] = {-1, 0, 0, 1};
    int dj[4] = {0, -1, 1, 0};
    if(maze[0][0] == 1)
        solve(0,0,maze,n,visited,ans,di,dj);
    
    return ans;
}
```

Time - o(4^(n x m)) bcoz for every we are trying 4 different ways </br>
Space - o(m x n)
