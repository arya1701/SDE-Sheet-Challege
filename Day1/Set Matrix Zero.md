# There are three approach to solve this question.
## 1. Brute force - not work for larger inputs

```c++

void setZeros(vector<vector<int>> &matrix)
{
  
  // Approach:
  // Traverse through the matrix and if we find any value with 0, we make entire row & col -1,
  	// why -1 ? because it will not in the matrix
  
  // traverse again the matrix & if we find -1 we can confirm this ele we have changed to 0.
  
    int rows = matrix.size();
    int cols = matrix[0].size();
  
   // traversing the matrix
    for(int i = 0;i<rows;i++){
        for(int j = 0;j<cols;j++){
            
          // for every cell, if it contains 0
            if(matrix[i][j] == 0){
              
              
                // we have to make entire col with -1  
                int ind = i-1;
                while(ind>=0){
                    if(matrix[ind][j] != 0){
                        matrix[ind][j] = -1;
                    }
                    ind--;
                }
                ind = i+1;
                while(ind<rows){
                    if(matrix[ind][j] != 0){
                        matrix[ind][j] = -1;
                    }
                    ind++;
                }
                
                // we have to make entire row with -1  
                ind = j-1;
                while(ind>=0){
                    if(matrix[i][ind] != 0){
                        matrix[i][ind] = -1;
                    }
                    ind--;
                }
                ind = j+1;
                while(ind<cols){
                    if(matrix[i][ind] != 0){
                        matrix[i][ind] = -1;
                    }
                    ind++;
                }
                
            }
        }
    }
  // again traversing if we find -1, that means we have to convert to 0
    for(int i = 0;i<matrix.size();i++){
        for(int j = 0;j<matrix[i].size();j++){
            if(matrix[i][j] <=0)
                matrix[i][j] = 0;
        }
    }
}

Time - o(n*m)*o(n+m), for every element in the matrix,we to visit n+m elements i.e row & col
Space - o(1)

```


## 2. Better appraoch - using some extra spaces
```c++
//  Approach
// Instread of visiting every row & col, we take two dummy array
// dummy1 -> size of col
// dummy2 -> size of row

// 1. start traversing the matrix, whenever we find 0, we simply place 0 in row index & col index.
// 2. again linearly traverse the matrix,  for every index (i,j) check out the ith index in row array 
// and jth index in the col array, if any of the index is 0 then make matrix[i][j] to 0

#include <bits/stdc++.h> 
void setZeros(vector<vector<int>> &matrix)
{
	// Write your code here.
    int rows = matrix.size();
    int cols = matrix[0].size();
    
    vector<int> dummy1(rows,-1);
    vector<int> dummy2(cols,-1);
    
    for(int i = 0;i<rows;i++){
        for(int j = 0;j<cols;j++){
            if(matrix[i][j] == 0){
                dummy1[i] = 0;
                dummy2[j] = 0;
             
            }
        }
    }
    for(int i = 0;i<rows;i++){
        for(int j = 0;j<cols;j++){
            if(dummy1[i] == 0 || dummy2[j] == 0){
                matrix[i][j] = 0;
            }
        }
    }
    
   Time - o(n*m + n*m) - we are traversing the array twice
   space - o(n) + o(m) - for taking two dummy array of n and m size
 
}
```
## 3. Best appraoch - without using extra space

```c++
// Approach
// Instead of taking two dummy array, visualize 1st row as first dummy array and 1st col as second dummy array
// 1. Since matrix[0][0] responsible for first row as well as first(0th) col so two avoid wrong condition we took
// col = 0 to check if the 0th column has 0 or not
// matrix[0][0] to check if the 0th row has 0 or not.

#include <bits/stdc++.h> 
void setZeros(vector<vector<int>> &matrix)
{
	// Write your code here.
    int n = matrix.size();
    int m = matrix[0].size();
    
    int col = 1;
    
    for(int i = 0;i<n; i++){
    
        // checking if there is any 0 in the 0th colm
        if(matrix[i][0] == 0)
            col = 0;
        
        for(int j = 1;j<m; j++){
            
            if(matrix[i][j] == 0){
                matrix[i][0] = 0;
                matrix[0][j] = 0;
            }
        }
    }
    // now traversing in the reverse direction because if we start traversing from the start it might changes the further elements 
    //  which is wrong checking if row or col has 0 then we have to change matrix[i][j] = 0
    for(int i=n-1;i>=0;i--){
        for(int j = m-1;j>=1;j--){
            if(matrix[i][0] == 0 || matrix[0][j] == 0){
                matrix[i][j] = 0;
            }
        }
    // at last if we find col = 0 that means we have to change this also
        if(col == 0)
            matrix[i][0] = 0;
    }
}
Time - o(n*m + n*m) - traversing the twice
space - o(1)
```

