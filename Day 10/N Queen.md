### Approach 1:

```c++
bool isSafe(int row, int col, vector<vector<int>>&ds, int n){
    int r = row;
    int c = col;
    while(row >= 0 && col >= 0){
        if(ds[row][col] == 1)
            return false;
        row--;
        col--;
    }
    row = r;
    col = c;
    while(col >= 0){
        if(ds[row][col] == 1)
            return false;
        col--;
    }
    row = r;
    col = c;
    while(row < n && col>= 0){
        if(ds[row][col] == 1)
            return false;
        row++;
        col--;
    }
    return true;
}
void solve(int col, vector<vector<int>>&ds, vector<vector<int>> &ans,int n){
    if(col == n){
        vector<int> temp;
        for(auto x:ds){
            for(auto y:x){
                temp.push_back(y);
            }
        }
        ans.push_back(temp);
        return;
    }
    // for every row
    for(int row = 0; row<n; row++){
        if(isSafe(row,col,ds,n)){
            ds[row][col] = 1;
            solve(col+1,ds,ans,n);
            ds[row][col] = 0;
            
        }
    }    
}
vector<vector<int>> solveNQueens(int n) {
    // Write your code here.
    vector<vector<int>> ans;
    vector<vector<int>> ds(n,vector<int>(n,0));
   
    solve(0,ds,ans,n);
    
    return ans;
    
}
```
This is not the efficient approach because we are using o(n) time extra to move in the left upper diagonal and lower diagnoal direction.

### Approach 2: Optimal using hashing (avoid using extra time o(n))

```c++
void solve(int col, vector<vector<int>>&ds, vector<vector<int>> &ans,int n, vector<int> &left, vector<int> &upper, vector<int> &lower){
    if(col == n){
        vector<int> temp;
        for(auto x:ds){
            for(auto y:x){
                temp.push_back(y);
            }
        }
        ans.push_back(temp);
        return;
    }
    // for every row
    for(int row = 0; row<n; row++){
        if(left[row] == 0 && lower[row+col] == 0 && upper[(n-1)+(col-row)] == 0){
            // we can place the queen
            ds[row][col] = 1;
            left[row] = 1;
            lower[row+col] = 1;
            upper[(n-1)+(col-row)] = 1;
            solve(col+1, ds,ans,n,left,upper,lower);
            ds[row][col] = 0;
            left[row] = 0;
            lower[row+col] = 0;
            upper[(n-1)+(col-row)] = 0;
        }
    }    
}
vector<vector<int>> solveNQueens(int n) {
    // Write your code here.
    vector<vector<int>> ans;
    vector<vector<int>> ds(n,vector<int>(n,0));
    vector<int> left(n,0);
    vector<int> upperDiagonal(2*n-1,0);
    vector<int> lowerDiagonal(2*n-1,0);
    
    
    solve(0,ds,ans,n,left,upperDiagonal, lowerDiagonal);
    
    return ans;
    
}
```
