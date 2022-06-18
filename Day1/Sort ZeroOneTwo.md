## Sort an array of 0's, 1's and 2's.

### Approach 1: Using sorting algorithm.

Time - o(NlogN)
space - o(1)

### Approach 2: Count the frequency of 0, 1 and 2 : Counting Sort
1. Find the count of 0,1 and 2 and update count_1, count_2 and count_3
2. Traverse the array again and overwrite count_1 times 1 , count_2 times 2 and similarly 3 in the original array.

Time - o(2*N) traversing the array twice
space - 0(1)

### Approach 3: Using three pointers - Variation of Dutch National Flag algorithm.

1. Three pointer - low,mid, high. Our goal is move all the 0's at the starting, 2's at the end(right) and 1's in the middle (between 0's and 2's)
2. low and mid at 0th index, high at last index (n-1)th index.
3. This algo based on the fact that - [0 to low-1] -> 0 and [high+1 to n] -> 2 and [low to mid-1] -> 1.
4. We will moving mid untill while(mid <= high) and there are three operation possible.

nums[mid] == 0:
  swap(nums[low], nums[mid])
  low++, mid++
nums[mid] == 1:
  mid++
nums[mid] == 2:
  swap(nums[mid],nums[high])
  high--
  
  ```c++
    int low = 0;
    int mid = 0;
    int high = n - 1;
    
    while(mid <= high){
        if(arr[mid] == 0){
            swap(arr[low],arr[mid]);
            low++;mid++;
        }else if(arr[mid] == 1)
            mid++;
        else{
            swap(arr[mid],arr[high]);
            high--;
        }
    }
  ```
  Time - o(N)
  spaec - o(1)

