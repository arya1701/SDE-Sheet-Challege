## You are given an array of ‘N’ integers. You have to find the sum of all the subsets in the non-decreasing order of the given array.

for N, 2<sup>N</sup> subset possible including NULL

### Approach 1: Brute force (using power set algo)

Bit manipulation
How to check ith bit is set or not ?

n = 5 -> 101
and we have to check 2nd bit is set or not ? so for this we have take a &(AND) with 100, jis bit ko check krna h uss bit ke neche one bake sabke neche zero. if the 
result is non zero that means ith bit is set else not set

      5 ----- 1 0 1
 index        2 1 0 
 
 So take & (AND) with 1 0 0
 
              1 0 1
           &  1 0 0
            ---------
              1 0 0
            ---------
            that means 2nd bit is set.
  
 How to find that 100, means other no jiske sath hme AND karna h, for that we have to take left shift by ith ( 1 << i )
 
 finally,
  ``` N & ( 1 << i) != 0  ```  means ith bit is set else not set
  
  ```c++
  string Str = "abc" , Output -  "","a","b","ab","c","ac","bc","abc"
  2^N =  1<<N both are same
  
  for(int i = 0; i<2^N - 1; i++){
    string ans = "";
    
    for(int i =0; i<N; i++ ){
    
    // check evry bit is set or not
    if( i & (1 << j) != 0)
      ans += str[j];
    }
    print(ans);// print every subsequence
  }
  ```


Time - o(2<sup>N</sup> x N) </br>
Space - o(1)


### Approach 2: Using recursion

Intuition: For every index we have two options either to pick the element to add it to your subset(pick) or not pick the element at that index and move to the next 
index(non-pick).

- Traverse through the array
- for each index, two choice - pick or not pick
- pick the element,i.e add the element to the sum or
- Not pick and move to the next element, recursively, until the base condition.
- When we reach the end of the array is the base condition.

```c++
void recursive(vector<int> &num ,int index, vector<int> &ans, int sum){
    int n = num.size();
    if(index == n){
        ans.push_back(sum);
        return;
    }
    // pick the element
    recursive(num, index+1, ans, sum + num[index]);
    // not pick
    recursive(num, index+1, ans, sum);
    
}
vector<int> subsetSum(vector<int> &num)
{
    // Write your code here.
    vector<int>ans;
    recursive(num,0,ans,0);
    sort(ans.begin(),ans.end());
    return ans;
}
```

Time - o(2^N + (2^N log(2^N))), for iterating two choice, for sorting </br>
Space - o(2^N)
