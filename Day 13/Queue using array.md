```c++
class Queue {
public:
    int frontt;
    int rear;
    int count;
    int *que;
    int n;
    Queue() {
        frontt = 0;
        rear = 0;
        n = 5001;
        count = 0;
        que = new int[n];
    }

    /*----------------- Public Functions of Queue -----------------*/

    bool isEmpty() {
        if(count == 0)
            return true;
        else
            return false;
    }

    void enqueue(int data) {
        if(count == n)
            return; // queue is full
        
        que[rear % n] = data;
        rear++;
        count++;
    }

    int dequeue() {
        if(count == 0)
            return -1; // queue is empty
        int ele = que[frontt%n];
        que[frontt % n] = -1;
        frontt++;
        count--;
        return ele;
    }

    int front() {
        if(count == 0)
            return -1; // empty
        return que[frontt % n];
    }
};
```
