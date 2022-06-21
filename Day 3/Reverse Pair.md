### We are given an array of size ‘N’. Pair (i, j) will be a Reverse Pair when i < j and 'ARR[i]' > 2 * 'ARR[j]'.
Our task is to find the number of Reverse Pairs present in given 'ARR'.


### Approach 1: Brute force

Using 2 nested For loops the outer loop having i as pointer and the inner loop with j as pointer and verify the given condition.

```c++
#include <bits/stdc++.h> 
int reversePairs(vector<int> &arr, int n){
	// Write your code here.	
    int count = 0;
    for(int i = 0; i<n; i++){
        for(int j = i+1; j<n; j++){
            if(arr[i] > 2 * arr[j])
                count++;
        }
    }
    return count;
}
```

Time - o(N<sup>2</sup>) </br>
space - o(1)

### Approach 2: Optimal 
```c++
#include <bits/stdc++.h> 
int merge(vector<int> &arr, int low, int mid, int high){
    int count = 0;
    int j = mid + 1; // starting pos of the right half array
    
    // iterate over the left half of the array
    for(int i = low; i<= mid; i++){
        // check condition
        // either the right half exhausted or the condition is not fulfilled
        while(j<=high && arr[i] > (2* (long)arr[j])){
            j++;
        }
        // count the no of elements on the left
        // that will contribue the no of pairs of the ith element
        count += (j - (mid+1)); 
    }
        // after computed the total no of pairs for the left and right half
        // together, have to do merge
        
        vector<int> temp;
        int left = low; // first index of the left array
        int right = mid+1; // first index of the right array
        
        while(left <= mid && right<= high){
            if(arr[left] <= arr[right]){
                temp.push_back(arr[left++]);
            }else
                temp.push_back(arr[right++]);
        }
        while(left<= mid)
            temp.push_back(arr[left++]);
        while(right<= high)
            temp.push_back(arr[right++]);
        for(int i = low; i<= high; i++)
            arr[i] = temp[i-low];
        
    return count;
    
}

int mergerSort(vector<int> &arr, int low, int high){
    if(low>=high)
        return 0;
    int mid = (low + high)/2;
    int inv = mergerSort(arr, low, mid); // left recursion
    inv += mergerSort(arr,mid+1, high); // right recursion
    inv += merge(arr,low,mid, high);
    
    return inv;
    
}
int reversePairs(vector<int> &arr, int n){
	// Write your code here.	
    return mergerSort(arr,0,n-1);
}
```
Time - o(NlogN) + o(N) + O(N) // o(N) for merging, o(N) for counting pairs
space - o(N), used temp array in merging
