### Array arr ig given with some target value, return four numbers a,b,c,d. Such that A+B+C+D == target.

### Appraoch 1: Brute force

- Sort the array
- Use 3 pointer + Binary search on the right half
- Store all the quads that are generated

```c++
vector<vector<int>> fourSum(vector<int>& nums, int target) {
        int n = nums.size();
        
        sort(nums.begin(),nums.end());
      
       set<vector<int>> sv;
        for(int i=0;i<n;i++)
        {
            for(int j=i+1;j<n;j++)
            {
    
                for(int k=j+1;k<n;k++)
                { 
                  
                   int x = (long long)target - 
                           (long long)nums[i]-
                           (long long)nums[j]-(long long)nums[k];
                   
                        if(binary_search(nums.begin()+k+1,nums.end(),x)){
                            vector<int> v;
                            v.push_back(nums[i]);
                            v.push_back(nums[j]);
                            v.push_back(nums[k]);
                            v.push_back(x);
                            sort(v.begin(),v.end());
                            sv.insert(v);
                        }
                }
            }
        }
        vector<vector<int>> res(sv.begin(),sv.end());
        return res;
    }
```
Time - (N^3) log2N + NlogN = NlogN for sorting


### Approach 2: Optimized 

Sort the array, and then fix two pointers, so the remaining sum will be (target – (nums[i] + nums[j])).
Now we can fix two pointers, one front, and another back, and easily use a two-pointer to find the remaining two numbers of the quad.
In order to avoid duplications, we jump the duplicates, because taking duplicates will result in repeating quads. 
We can easily jump duplicates, by skipping the same elements by running a loop.

```c++

// Codestudio

#include <bits/stdc++.h> 
string fourSum(vector<int> nums, int target, int n) {
    // Write your code here.
    vector<vector<int>> ans;
        int sum;
        // if input is empty then return the empty vector
        
        if(nums.empty())
            return "No";
        
        
//         int n = nums.size();
        sort(nums.begin(), nums.end());
        
        // iterating over the vector using two pointer i and j
        for(int i = 0;i<n;i++){
            
            for(int j = i+1;j<n;j++){
                
                
                int target2 = target - nums[i] - nums[j];
                int left = j+1;
                int right = n-1;
                
                while(left<right){
                    
                    int sum = nums[left] + nums[right];
                    
                    if(sum<target2)
                        left ++;
                    else if(sum>target2)
                        right --;
                    else{
                        vector<int>quadruplet(4,0);
                        quadruplet[0] = nums[i];
                        quadruplet[1] = nums[j];
                        quadruplet[2] = nums[left];
                        quadruplet[3] = nums[right];
                        sum = accumulate(quadruplet.begin(),quadruplet.end(),0);
                        return "Yes";
                        
                        
                        // processing the duplicates of number
                        // move left , eliminated duplicate 
                        // similarly for right pointer
                        
                        while(left < right && nums[left] == quadruplet[2])
                            ++left;
                        
                        // similarly for right pointer
                        while(left < right && nums[right] == quadruplet[3])
                        
                            --right;

                    }
                    
                }
                
                //     j     j 
                // ... 2 2 2 2 3 --> move j to 3 processing the duplicate
                // above for loop, move j to 2, so use j+1
                while(j+1 <n && nums[j+1] == nums[j])
                    ++j;
            }
            // similarly, need to cross all the duplicates
            while(i+1<n && nums[i+1] == nums[i])
                ++i;
        
        }
    return "No";
}

```
Time - o(N^3) </br>
Space - o(1)

### Note - For find all unique quadruplets whose sum == target ...Leetcode

```c++
 class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        
        vector<vector<int>> ans;
        
        // if input is empty then return the empty vector
        
        if(nums.empty())
            return ans;
        
        
        int n = nums.size();
        sort(nums.begin(), nums.end());
        
        // iterating over the vector using two pointer i and j
        for(int i = 0;i<n;i++){
            
            for(int j = i+1;j<n;j++){
                
                
                int target2 = target - nums[i] - nums[j];
                int left = j+1;
                int right = n-1;
                
                while(left<right){
                    
                    int sum = nums[left] + nums[right];
                    
                    if(sum<target2)
                        left ++;
                    else if(sum>target2)
                        right --;
                    else{
                        vector<int>quadruplet(4,0);
                        quadruplet[0] = nums[i];
                        quadruplet[1] = nums[j];
                        quadruplet[2] = nums[left];
                        quadruplet[3] = nums[right];
                        ans.push_back(quadruplet);
                        
                        // processing the duplicates of number
                        // move left , eliminated duplicate 
                        // similarly for right pointer
                        
                        while(left < right && nums[left] == quadruplet[2])
                            ++left;
                        
                        // similarly for right pointer
                        while(left < right && nums[right] == quadruplet[3])
                        
                            --right;

                    }
                    
                }
                
                //     j     j 
                // ... 2 2 2 2 3 --> move j to 3 processing the duplicate
                // above for loop, move j to 2, so use j+1
                while(j+1 <n && nums[j+1] == nums[j])
                    ++j;
            }
            // similarly, need to cross all the duplicates
            while(i+1<n && nums[i+1] == nums[i])
                ++i;
        
        }
        return ans;
    }
};
```

