```c++
int uniqueElement(vector<int> arr, int n)
{
	// Write your code here
    int low = 0;
    int high = n-2;
    
    while(low <= high){
        
        int mid = (low + high) /2;
        
        if(arr[mid] == arr[mid ^ 1]) // we will shrink the left part
            low = mid + 1;
        else
            high = mid - 1;
    }
    return arr[low];
}

```
