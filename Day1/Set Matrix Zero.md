# There are three approach to solve this question.
1. Brute force - not work for larger inputs

```

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

// time - o(n*m)*o(n+m), for every element in the matrix,we to visit n+m elements i.e row & col

```


2. Better appraoch - using some extra spaces
3. Best appraoch - without using extra space

