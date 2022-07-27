## Print All Permutations of a String/Array

### Using extra space
```c++
class Solution {
public:
    
    void func(vector<int> &ds, vector<int> &nums, vector<vector<int>> &ans, int freq[]){
        
        int si = nums.size();

        if(ds.size() == si){
            ans.push_back(ds);
            return;
        }
        for(int i = 0;i<si;i++){
            // if freq of that ele is un marked then we pick that
            if(!freq[i]) 
            {
                ds.push_back(nums[i]);
                freq[i] = 1;
                func(ds, nums,ans, freq);
                
                // when we come back form the recrsion then we make sure the element is throw out and unmarked in your freq array
                freq[i] = 0;
                ds.pop_back();
            }
        }
    }
    
    
    vector<vector<int>> permute(vector<int>& nums) {
        
        vector<vector<int>> ans; // for stroing all the permutation
        vector<int> ds;
        int si = nums.size();
        int freq[si]; // freq array initilized with 0
        for(int i = 0;i<si;i++)
            freq[i] = 0;
        
        func(ds, nums, ans, freq);
        return ans;
    }
};
```

### without using extra space
```c++
void recursive(string &s,int ind,vector<string>&res){
	if(ind >= s.size()){
		res.push_back(s);
		return;
	}
	for(int i =ind;i<s.size();i++){
		swap(s[ind],s[i]);
		recursive(s,ind+1,res);
		swap(s[ind],s[i]);
	}
}
vector<string> findPermutations(string &s) {
    // Write your code here.
	vector<string>res;
	recursive(s,0,res);
	return res;
}
```
