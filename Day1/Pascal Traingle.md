## Given n, we have to print n rows of the pascal traingle


```c++
#include <bits/stdc++.h> 
vector<vector<long long int>> printPascal(int n) 
{
  // Approach
  // ith row has i+1 elem (0 indexing)
  // first and last ele of every row is 1
    vector<vector<long long int>> rows(n);
    for(int i = 0;i<n;i++){
        
        rows[i].resize(i+1);
        // first and last element of every row is 1
        rows[i][0] = rows[i][i] = 1;
        
        // inner elements
        for(int j=1;j<i;j++){
            rows[i][j] = rows[i-1][j-1] + rows[i-1][j];
        }
    }
    return rows;
}

Time - o(n^2)
Space - o(n^2)
```
