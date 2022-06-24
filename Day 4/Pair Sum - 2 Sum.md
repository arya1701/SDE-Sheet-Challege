### Given array 'ARR' of size 'N' and an integer 'S'. Task is to return the list of all pairs of elements such that each sum of elements of each pair equals 'S'.

### Approach 1: Brute force

Using two loops, for every i, check on the right of the array.
 ```c++
for (int i = 0; i < nums.size(); ++i) {
   	 for (int j = i + 1; j < nums.size(); ++j) {
   		 if (nums[i] + nums[j] == target) {
   			 res.push_back(i);
   			 res.push_back(j);
   			 break;
   		 }
   	 }

 ```

Time - o(N^2) </br>
Space - o(1)

### Approach 2: Using two pointer

Sort the array, use two variable, one at start and other at end.
Traverse the array, and for each element i, try to find another element amongst the remaining elements, such that the sum of both the elements equals the target. 

First Element: i

So the required second element will be, target – nums[i] and If we find both the elements, we break the loop and return the indices.

 ```c++
 class Solution {
public:
    vector<int> twoSum(vector<int>& original, int target) {
        int n = original.size();
        vector<int> res, nums = original;
        int left = 0,n1= 0 , n2 = 0;
        int right = n-1;
        sort(nums.begin(), nums.end());
        while(left<right){
        	if(nums[left]+nums[right]==target){
                 n1 = nums[left];
                 n2 = nums[right];
            	break;
        	}
        	else if(nums[left]+nums[right]>target)
            	    right--;
        	else
            	    left++;
    	}
        // since we change the original array so we have to find in the orginal array
        for(int i = 0; i<n; i++){
            if(original[i] == n1)
                res.push_back(i);
            else if(original[i] == n2)
                res.push_back(i);

        }
        return res;
            
    }
};
```
Time - (NlognN)</br>
Space - o(N)

### Approach 3: Efficient - Using hashing
Use a hash-map to see if there’s a value (target – i) that can be added to the current array value i to get the sum equals to target.
If target – i is found in the map, we return the current index, and index stored at target – nums[index] location in the map. 

This can be done in constant time using hashing.

 ```c++
 class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        
        // return the index vector
        vector<int> ans;
        
        // hash table
        unordered_map<int,int> table;
        for(int i = 0 ;i<nums.size();i++){
            
            // search the remaining target in the hash table
            if(table.find(target - nums[i]) != table.end()){
                ans.push_back(table[target - nums[i]]);
                ans.push_back(i);
                return ans;
            }
            // store the current element in the table
            table[nums[i]] = i;
        }
        
        return ans;
        
    }
};
 ```
 Time - o(N) </br>
 space - O(N)
 
 ## For all the pairs whose sum == target. 
```c++
#include <bits/stdc++.h> 
vector<vector<int>> pairSum(vector<int> &nums, int target){
   // Write your code here.
    
    vector<vector<int>> ans;
    vector<int> temp;
    unordered_map<int,int> table;
    
    for(int i = 0; i<nums.size(); i++){
        int rem = target - nums[i];
        // search the remaining target in the hash table
            if(table.find(rem) != table.end()){
                int count = table[rem];
                for (int j = 0; j < count; j++){
                    temp.push_back(rem),temp.push_back(nums[i]);
                    sort(temp.begin(),temp.end());
                    ans.push_back(temp);
                    temp.clear();
                }
            }
            // store the current element in the table
            table[nums[i]]++ ;
    }
    sort(ans.begin(),ans.end());
    return ans;
    
}
```
 
