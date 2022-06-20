## We are given a matrix, find the target in the given matrix. 
Note:
- Each row is sorted.
- the first element of a row is greater than the last element of the previous row (if exists).

### Approach 1: Brute force

Linearly traverse the matrix and find the target element, if found return true else false.

Time - o(N*M)<br /> 
space - o(1)

### Approach 2: As we know the row is sorted, apply Binary search

Traverse all the row and do binary search for the target value. In any row, if we find the traget return true else false.

Time - o(N*log<sub>2</sub>M) <br/>
space - o(1)

### Approach 3: Efficient - Use Binary search

As we can that the matrix is row wise and column wise sorted, we can the sequence is increasing monotically. Apply binary search consider 2D matrix as 1D matrix with 
index from 0 to (m*n -1).

```c++
bool findTargetInMatrix(vector < vector < int >> & mat, int m, int n, int target) {
    // Write your code here.
    int low = 0;
    int mid;
    int high = m*n-1;
    
    while(low <= high){
        mid = (low + high) /2;
        
        if(mat[mid/n][mid%n] == target)
            return true;
        if(mat[mid/n][mid%n] < target)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return false;
}
```

Time - O(log(M*N) <br/>
space - o(1)
