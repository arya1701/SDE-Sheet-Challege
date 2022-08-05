```c++
// Stack class.
class Stack {
public:
    int *st;
    int topp;
    int size;
public:
    
    Stack(int capacity) {
        topp = -1;
        size = capacity;
        st = new int[size];
    }

    void push(int num) {
        
        topp++;
        st[topp] = num;
    }

    int pop() {

        if(!isEmpty()){
            return st[topp--];
        }else
            return -1;
    }
    
    int top() {

        if(!isEmpty())
            return st[topp];
        else
            return -1;
    }
    
    int isEmpty() {

        if(topp == -1)
            return 1;
        else
            return 0;
    }
    
    int isFull() {

        if(topp == size)
            return 1;
        else
            return 0;
    }    
};
```
