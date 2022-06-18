## We have to find the sum of the subarray (including empty subarray) having maximum sum among all subarrays.

### Approach 1: Brute force
1. Three loops , two loops for finding all the subarray and third looop for finding the sum of every subarray.

```c++
int max_sum = 0;
for (i = 0; i <= n - 1; i++) {
    for (j = i; j <= n - 1; j++) {
      int sum = 0;
      for (int k = i; k <= j; k++)
        sum = sum + nums[k];
      if (sum > max_sum)
        max_sum = sum;
    }
  }
  return max_sum;
```

Time - o(n^3)
space - o(1)

### Approach 2: Little bit optimize
1. Instead of using the third loop for finding the sum, we can find the sum on the way in two loops only.

```c++
int max_sum = INT_MIN;
for (i = 0; i <= n - 1; i++) {
    int sum = 0;
    for (j = i; j <= n - 1; j++) {
      sum += nums[j]
      if(sum>max_sum)
        max_sum = sum;
    }
}
return max_sum;
```
Time - o(n^2)
space - o(1)

### Approach 3: Using Kadane's Algorithm Optimal
1. Need some variable like max_so_far = nums[0], because single elements can also be a maximum sum
2. max_end_here = 0
Traverse the array, adding the ith ele with mex_end_here and check if it's greater than max_so_far, if yes then update max_so_far. Anytime max_end_here = 0 update 
max_end_here = 0 and finally return the max_so_far.

```c+++
int maxSubArray(vector<int>& nums) {
        long max_so_far = nums[0];
        long max_end_here = 0;
        
        for(int i = 0;i<nums.size();i++){
            max_end_here += nums[i];
            
            if(max_end_here > max_so_far)
                max_so_far = max_end_here;
            
            if(max_end_here < 0)
                max_end_here = 0;
        }
        return max_so_far;
    }
```
Time - o(n)
space - o(1)
