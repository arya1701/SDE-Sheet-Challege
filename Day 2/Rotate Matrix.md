## Rotate the matrix by 90 degree.

### Approach 1: Brute force

1 2 3  ----->       7 4 1

4 5 6  ----->       8 5 2

7 8 9  ----->       9 6 8

1. take the another matrix
2. take the 1st row and put in the last col, take the 2nd row put in the 2nd last col, 3rd row in the 3rd last col.

 ```c++
 vector<vector<int>> rotated(n, vector<int>(n,0));
   for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
      rotated[j][n - i - 1] = matrix[i][j];
    }
  }
  
 ```
 Time - o(n^2)
 space - 0(n^2)
 
 ### Approach 1: Optimal without using extra space
 
 1. Find the transpose of the matrix
 2. Now reverse every row

```c++
// Transpose
for(int i = 0;i<row;i++){
  for(int j = 0;j<i;j++){
    swap(matrix[i][j],matrix[j][i]);
    }
  }
// Reverse
  for(int i = 0;i<row ;i++)
    reverse(matrix[i].begin(),matrix[i].end());
```


Time - o(n^2) + o(n^2) ~ o(n^2), for reverese and transpose

space - o(1)

 
 
