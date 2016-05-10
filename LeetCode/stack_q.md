##232. Implement Queue using Stacks
Implement the following operations of a queue using stacks.

push(x) -- Push element x to the back of queue.<br>
pop() -- Removes the element from in front of queue.<br>
peek() -- Get the front element.<br>
empty() -- Return whether the queue is empty.<br>

You must use only standard operations of a stack -- which means only push to top, peek/pop from top, size, and is empty operations are valid.
###Solution
```C
class Queue {
public:
    stack<int> q1,q2;
    // Push element x to the back of queue.
    void push(int x) {
        q1.push(x);
    }

    // Removes the element from in front of queue.
    void pop(void) {
        while(!q1.empty())
        {
            q2.push(q1.top());
            q1.pop();
        }
        q2.pop();
        while(!q2.empty())
        {
            q1.push(q2.top());
            q2.pop();
        }
    }

    // Get the front element.
    int peek(void) {
        while(!q1.empty())
        {
            q2.push(q1.top());
            q1.pop();
        }
        int ret = q2.top();
        while(!q2.empty())
        {
            q1.push(q2.top());
            q2.pop();
        }
        return ret;
    }

    // Return whether the queue is empty.
    bool empty(void) {
        return q1.empty();
    }
};
```
###Lesson
* 
stack: push(item)、emplace(args)、pop()、top()
* 
queue: pop()、front(与栈不同)、back(仅用于队列)、top(仅用于优先级)、push(item)、emplace(args)
* 
双栈实现队列


##225. Implement Stack using Queues   
Implement the following operations of a stack using queues.

push(x) -- Push element x onto stack.<br>
pop() -- Removes the element on top of the stack.<br>
top() -- Get the top element.<br>
empty() -- Return whether the stack is empty.<br>
Notes:<br>
You must use only standard operations of a queue -- which means only push to back, peek/pop from front, size, and is empty operations are valid.
###Solution
```C
class Stack {
public:
    queue<int> q1,q2;
    // Push element x onto stack.
    void push(int x) {
        q1.push(x);
    }

    // Removes the element on top of the stack.
    void pop() {
        int len = q1.size();
        if(len==0)
            return;
        while(--len)        //先自减的原因
        {
            q2.push(q1.front());
            q1.pop();
        }
        q1.pop();
        while(!q2.empty())
        {
            q1.push(q2.front());
            q2.pop();
        }
    }

    // Get the top element.
    int top() {
        int len = q1.size();
        while(--len)
        {
            q2.push(q1.front());
            q1.pop();
        }
        int ret = q1.front();
        q2.push(ret);       //重新压入的原因
        q1.pop();
        while(!q2.empty())
        {
            q1.push(q2.front());
            q2.pop();
        }
        return ret;
    }

    // Return whether the stack is empty.
    bool empty() {
        return q1.empty();
    }
};
```
###Lesson
* 
队列大小：当弹出或者获得顶部元素时
* 
获得顶部元素时需要记录最后一个，然偶在压入到q2中。


[返回目录](README.md)