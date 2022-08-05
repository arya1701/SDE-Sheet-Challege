### Using two stack where push operation is O(N)
```c++
#include <stack>
class Queue {
    
    public:
    stack<int> s1,s2;
    Queue() {
    }

    void enQueue(int val) {
        while(!s1.empty()){
            s2.push(s1.top());
            s1.pop();
        }
        s1.push(val);
        while(!s2.empty()){
            s1.push(s2.top());
            s2.pop();
        }
    }

    int deQueue() {
        if(s1.empty())
            return -1;
        else{
            int ele = s1.top();
            s1.pop();
            return ele;
        }
    }

    int peek() {
        if(s1.empty())
            return -1;
        else{
            return s1.top();
        }
    }

    bool isEmpty() {
        if(s1.empty())
            return true;
        else 
            return false;
    }
};
```

### Using two stack where push operation is o(1) amortized
```c++
#include <stack>
class Queue {
    
    public:
    stack<int> s1,s2;
    // consider s2 as input and s2 as output
    Queue() {
    }

    void enQueue(int val) {
        
        s1.push(val);
    }

    int deQueue() {
        if(s2.empty()){
            while(!s1.empty()){
                s2.push(s1.top());
                s1.pop();
            }
        }
        if(s2.empty())
            return -1;
        int ele = s2.top();
        s2.pop();
        return ele;
    }

    int peek() {
        if(s2.empty()){
            while(!s1.empty()){
                s2.push(s1.top());
                s1.pop();
            }
        }
        if(s2.empty())
            return -1;
        else 
            return s2.top();
    }

    bool isEmpty() {
        if(s2.empty() && s1.empty())
            return true;
        else 
            return false;
    }
};
```
