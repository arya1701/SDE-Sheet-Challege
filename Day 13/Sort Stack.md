```c++
void insertIntoStack(stack<int> &st, int ele){
    if(st.empty() || (!st.empty() && st.top() < ele)){
        st.push(ele);
        return;
    }
    int val = st.top();
    st.pop();
    insertIntoStack(st, ele);
    st.push(val);
}
void sortStack(stack<int> &st)
{
    if(st.empty())
        return;
    int ele = st.top();
    st.pop();
    sortStack(st);
    insertIntoStack(st,ele);
}
```
