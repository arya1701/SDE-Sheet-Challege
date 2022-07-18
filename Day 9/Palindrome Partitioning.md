## Given a string S, partition it such that every substring of the partition is palindrome. Return all the possible partition of S.

Approach - Recursive

Wheneven we do partition make sure that partition is palindrome. We are doing same thing for every partition, thinking out for recursion here. Yes we can use recursion

- Try to do partition whereever it is possible.
- Call the recursion for the left out string

whenever we do partiotion right at the end it means we are able to generate a paritition where every substring is a palindrome.

```c++
bool checkPalindrome(string s, int left, int right){
    while(left <= right){
        if(s[left++] != s[right--])
            return false;
    }
    return true;
}
void recursion(int n, int index, string s, vector<vector<string>> &ans, vector<string> &ds){
    if(index == n){
        ans.push_back(ds);
        return;
    }
    
    for(int i = index; i<n; i++){
        
        // check if index to i is palindrome or not
        // if yes then add to current ds and call the next recursion
        if(checkPalindrome(s,index,i)){
            ds.push_back(s.substr(index,i-index+1));
            recursion(n,i+1,s,ans,ds);
            ds.pop_back();
        }
    }
}

vector<vector<string>> partition(string &s) 
{
    // Write your code here.
    vector<vector<string>> ans;
    vector<string> ds;
    int n = s.size();
    
    recursion(n,0,s,ans,ds);
    return ans;
}
```
Time - O( (2^n) *k*(n/2) ) ,O(2^n) to generate every substring, O(n/2)  to check if the substring generated is a palindrome. O(k) is for inserting the palindromes in another data structure, where k  is the average length of the palindrome list.

Space - O(k * x),The depth of the recursion tree is n, so the auxiliary space required is equal to the O(n).
