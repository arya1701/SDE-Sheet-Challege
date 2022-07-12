### Given array 'ARR' of size 'N'. It represents an elevation map wherein 'ARR[i]' denotes the elevation of the 'ith' bar. Print the total amount of rainwater that can be trapped in these elevations.

### Approach 1: Brute force
- For every index, find the min(leftMost, rightmost) - currentHeight.
- leftmost = i to 0
- rightmost = i to n-1

```c++
int trap(vector < int > & arr) {
  int n = arr.size();
  int waterTrapped = 0;
  for (int i = 0; i < n; i++) {
    int j = i;
    int leftMax = 0, rightMax = 0;
    while (j >= 0) {
      leftMax = max(leftMax, arr[j]);
      j--;
    }
    j = i;
    while (j < n) {
      rightMax = max(rightMax, arr[j]);
      j++;
    }
    waterTrapped += min(leftMax, rightMax) - arr[i];
  }
  return waterTrapped;
}
```
Time - o(n^2) </br>
Space - o(1)

### Appraoch 2: Optimized (Prefix sum)
We can pre compute leftMax and rightMax at each index. The complexity can be boiled down to O(1) if we precompute the leftMax and rightMax at each index.
- We can take two array,
- prefix max array, max towards to the left
- suffix max array, max towrds to the right
```c++
int trap(vector < int > & arr) {
  int n = arr.size();
  int prefix[n], suffix[n];
  prefix[0] = arr[0];
  for (int i = 1; i < n; i++) {
    prefix[i] = max(prefix[i - 1], arr[i]);
  }
  suffix[n - 1] = arr[n - 1];
  for (int i = n - 2; i >= 0; i--) {
    suffix[i] = max(suffix[i + 1], arr[i]);
  }
  int waterTrapped = 0;
  for (int i = 0; i < n; i++) {
    waterTrapped += min(prefix[i], suffix[i]) - arr[i];
  }
  return waterTrapped;
}
```
Time - o(n) + o(N) + O(N), for prefix, for suffix, for actual traverse</br>
Space - o(2N)

### Appraoch 3: Optimal using two pointer


```c++
#include <bits/stdc++.h> 
long getTrappedWater(long *arr, int n){
    // Write your code here.
    int l = 0;
    int r = n-1;
    int ans = 0;
    int leftmax = 0,rightmax = 0;
    
    while(l<=r){
        
        if(arr[l] <= arr[r]){
            
            if(arr[l] > leftmax)
                leftmax = arr[l];
            else
                ans += leftmax - arr[l];
            l++;
        }else{
            if(arr[r] >= rightmax)
                rightmax = arr[r];
            else
                ans += rightmax - arr[r];
            r--;
        }
    }
    return ans;
}
```
Intuition: We need a minimum of leftMax and rightMax.So if we take the case when height[l]<=height[r] we increase l++, 
so we can surely say that there is a block with a height more than height[l] to the right of l. 
And for the same reason when height[r]<=height[l] we can surely say that there is a block to the left of r which is at least of height[r].
So by traversing these cases and using two pointers approach the time complexity can be decreased without using extra space.

Time - o(n) </br>
Space - o(1)
