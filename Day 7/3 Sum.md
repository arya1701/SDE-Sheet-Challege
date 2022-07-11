## Finad all the unique triplets whose sum = 0, such that a+b+c = 0

### Approach 1: Brute force
- Traverse all the triplets and check
- Three-pointers i,j, and k. For every triplet we find the sum of A[i]+A[j]+A[k]. If this sum is equal to zero, we’ve found one of the triplets. 
- Put it into the set data structure and continue

```c++
vector < vector < int >> threeSum(vector < int > & nums) {
  vector < vector < int >> ans;
  vector < int > temp;
  int i, j, k;
  for (i = 0; i < nums.size() - 2; i++) {
    for (j = i + 1; j < nums.size() - 1; j++) {
      for (k = j + 1; k < nums.size(); k++) {
        temp.clear();
        if (nums[i] + nums[j] + nums[k] == 0) {
          temp.push_back(nums[i]);
          temp.push_back(nums[j]);
          temp.push_back(nums[k]);
        }
        if (temp.size() != 0)
          ans.push_back(temp);
      }
    }
  }

  return ans;
}
```

Time - o(n^3 logm), logm for inseting the element into the set </br>
Space - o(M)


### Approach 2: Using hashing
a+b+c = 0 </br>
c = -(a+b)

- Use a hash map to store the no and its count
- Using two loops, i and j. 
- check if c exist in th hashmap or not.


Time - o(n^2 logm), m unique triplets, log for inserting in the set </br>
Space - o(M) + o(N), for set in which are storing the unique triplets, for hashset


### Approach 3: Using Two pointer
## follow up - whose sum means a+b+c = k

b+c= -a

- Sort the array
- take  two two pointer low and high, and check low+high == k - c or not
- if low + high is less than means we have to increase so increase towards right
- else move towards the left


```c++
#include <bits/stdc++.h> 
vector<vector<int>> findTriplets(vector<int>nums, int n, int K) {
	// Write your code here.
     sort(nums.begin(), nums.end());
        
        vector<vector<int>> res;
        
        // moves for a
        
        for(int i = 0;i<(int)(nums.size())- 2;i++){
            
            // i==0 means it is the first element so we considered as a and move forward but if
            // it is not first element then we avoid duplicates by check nums[i] != nums[i-1] 
            // check with the previous elements
            
            if(i == 0 || (i>0 && nums[i] != nums[i-1])){
                
                int low = i+1;
                int hi = (int)(nums.size())-1;
                int sum = K - nums[i]; // that means b+c = -a
                
                while(low<hi){
                    if(nums[low] + nums[hi] == sum){
                        vector<int>temp;
                        temp.push_back(nums[i]);
                        temp.push_back(nums[low]);
                        temp.push_back(nums[hi]);
                        res.push_back(temp);
                        
                        // to avoid duplicates moves low and hi move untill equivalent
                        
                        while(low<hi && nums[low] == nums[low+1])
                            low++;
                        
                        while(low<hi && nums[hi] == nums[hi-1])
                            hi--;
                        // now move high and low
                        low++;hi--;
                    }
                    // if sum is smaller that means move towards right
                    else if(nums[low] + nums[hi] < sum)
                        low++;
                    // if sum is larger that means move towards left
                    else
                        hi--;
                }   
            }
        }
        return res;
}
```

Time - o(N*N) </br>
Space - o(M)
