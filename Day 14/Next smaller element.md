```c++
#include<stack>
vector<int> nextSmallerElement(vector<int> &arr, int n) {
    // Write your code here
    
    vector<int> ans(n);
    stack<int> st;
    
    for(int i = n-1; i>=0; i--){
        
        while(!st.empty() && st.top() >= arr[i])
            st.pop();
        if(st.empty() == false)
            ans[i] = st.top();
        else
            ans[i] = -1;
        st.push(arr[i]);
    }
    
    return ans;

}
```
