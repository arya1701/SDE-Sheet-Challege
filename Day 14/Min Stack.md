```c++
class MinStack {
public:
    stack<pair<int,int>> st;
    MinStack() {
        
    }
    
    void push(int val) {
        
        int mini = INT_MAX;
        
        if(st.empty())
            mini = val;
        else
            mini = min(st.top().second, val);
        
            st.push({val,mini});
            
    }
    
    void pop() {
        st.pop();
    }
    
    int top() {
        return st.top().first;
    }
    
    int getMin() {
        return st.top().second;
    }
};

```
Time - o(1) </br>
Space - o(2N), because we use pair here also that is another N
