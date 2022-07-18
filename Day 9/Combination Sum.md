## Return all the unique combination whose sum equal to the target. we can use any no of times of the particular element.

### Approach 1: 

For questions like printing combinations or subsequences, the first thing that should strike your mind is recursion.

How ?
Whenever the problem is related to picking up elements from an array to form a combination, start thinking about the “pick and non-pick” approach.
```
                              f(ind,target,ds)
                                    |
                                 /     \
                            Pick     Not Pick
     f(ind,target - arr[ind],ds)     f(ind+1,target,ds)
     
     if(target >= arr[ind])
     
     when we come from the recursion
     make sure we remove this array 
     of index.
     
```
```c++
void recursion(int index, int target,vector<int> &arr, vector<vector<int>> &ans, vector<int> &ds ,int n){
    if(index == n){
        if(target==0)
            ans.push_back(ds);
        return;
    }
    // picking the element
        ds.push_back(arr[index]);
        recursion(index+1,target - (arr[index]), arr, ans, ds,n);
        ds.pop_back();
    
    // if we not pick the element then we
    recursion(index+1,target,arr,ans,ds,n);
}
vector<vector<int>> findSubsetsThatSumToK(vector<int> arr, int n, int k)
{
    // Write your code here.
    vector<vector<int>> ans;
    vector<int> ds;

    recursion(0,k,arr,ans,ds,n);
    return ans;
}
```

Time - o(2^t x k), k is the avg length of the every combination, 2^t because we can use any no of items of particular elements, suppose t = 10 and ele is 1 so we have 2^t combi </br>
Space - o(k x X), X is no of combination
