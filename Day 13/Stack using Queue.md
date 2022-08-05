### Using 2 queues

```c++
#include <queue>
class Stack {
   public:
    
    queue<int> q1, q2;
    int size;
    
    Stack() {
        size = 1001;
    }

    /*----------------- Public Functions of Stack -----------------*/

    int getSize() {
        return q1.size();
    }

    bool isEmpty() {
        if(q1.size() == 0)
            return true;
        else
            return false;
    }

    void push(int element) {
        
        q2.push(element);
        while(!q1.empty()){
            q2.push(q1.front());
            q1.pop();
        }
        swap(q1,q2);
    }

    int pop() {
        if(q1.size() == 0)
            return -1;
        else{
           int ele = q1.front();
            q1.pop();
            return ele;
        }
    }

    int top() {
        if(q1.size() == 0)
            return -1;
        else
            return q1.front();
    }
};
```
### Using 1 queue
```c++
#include <queue>
class Stack {
   public:
    
    queue<int> q1;
    int size;
    
    Stack() {
        size = 1001;
    }

    /*----------------- Public Functions of Stack -----------------*/

    int getSize() {
        return q1.size();
    }

    bool isEmpty() {
        if(q1.size() == 0)
            return true;
        else
            return false;
    }

    void push(int element) {
        
        q1.push(element);
        for(int i = 0; i<q1.size()-1; i++){
            q1.push(q1.front());
            q1.pop();
        }
    }

    int pop() {
        if(q1.size() == 0)
            return -1;
        else{
           int ele = q1.front();
            q1.pop();
            return ele;
        }
    }

    int top() {
        if(q1.size() == 0)
            return -1;
        else
            return q1.front();
    }
};
```
