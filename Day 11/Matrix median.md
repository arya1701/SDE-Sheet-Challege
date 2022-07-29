 ```c++
 int countSmallerThanMid(vector<int> &row, int midd){
    int low = 0;
    int high = row.size() - 1;
    
    while(low <= high){
        int mid = (low + high)/2;
        
        if(row[mid] <= midd)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return low;
}
int getMedian(vector<vector<int>> &matrix)
{
    // Write your code here.
    int low = 1;
    int high = 1e9;
    int row = matrix.size();
    int col = matrix[0].size();
    
    while(low <= high){
        int mid = (low + high)/2;
        
        int count = 0;// count the no of ele lesser than equal to mid
        for(int i = 0; i<row; i++){
            count += countSmallerThanMid(matrix[i], mid);
        }
        
        if(count <= (row*col)/2)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return low;
}
```
Time - o(log<sub>2</sub>2<sup>32</sup> x N x log<sub>2</sub>M), 2^32 nearly equal to 10^9 i.e highest interger, N x log<sub>2</sub>M for every row we are implementing Binary search on its col length = o(32  Nlog<sub>2</sub>M)
