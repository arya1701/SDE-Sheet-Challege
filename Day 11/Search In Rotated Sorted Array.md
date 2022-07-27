```c++
int search(int* arr, int n, int key) {
    // Write your code here.
    int low = 0;
    int high = n-1;
    
    while(low <= high){
        int mid = (low+high) >> 1;
        
        if(arr[mid] == key)
            return mid;
        // check the left half is orted or not
        if(arr[low] <= arr[mid]){
            // figured out if the ele lies on the left half or not
            if(key >= arr[low] && key <= arr[mid])
                // eleminate the right half
                high = mid - 1;
            else
                low = mid + 1;
        }
        // check the right half sorted or not
        else{
            if(key >= arr[mid] && key <= arr[high])
                // eleminate the left half
                low = mid + 1;
            else
                high = mid - 1;
        }
        
        
    }
    return -1;
}
```
