```c++
bool isValid(int matrix[9][9], int row, int col, int c){
    
    for(int i = 0;i<9;i++){
        if(matrix[row][i] == c)
            return false;
        if(matrix[i][col] == c)
            return false;
        if(matrix[3*(row/3)+i/3][3*(col/3)+i%3] == c)
            return false;
    }
    return true;
}

bool solve(int matrix[9][9]){
    int row = 9, col = 9;
    for(int i = 0;i<row;i++){
        for(int j = 0; j<col; j++){
            
            // try to fill 1 to 9 if valid
            if(matrix[i][j] == 0){
                for(int c = 1;c<=9;c++){
                   if(isValid(matrix,i,j,c)){
                       matrix[i][j] = c;
                       //again call
                       if(solve(matrix) == true)
                           return true;
                       else
                           matrix[i][j] = 0;// means going back
                   }
                }
                return false;
            }
        }
    }
    return true;
}
bool isItSudoku(int matrix[9][9]) {
    // Write your code here.
   solve(matrix);    
}

```
