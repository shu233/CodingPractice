Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack.

Example:
```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

```Python
# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(x)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```

---
### My Answer
```Python
class MinStack(object):

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.stack = []

    def push(self, x):
        """
        :type x: int
        :rtype: None
        """
        self.stack.append(x)

    def pop(self):
        """
        :rtype: None
        """
        self.stack.pop()

    def top(self):
        """
        :rtype: int
        """
        return self.stack[-1]

    def getMin(self):
        """
        :rtype: int
        """
        return min(self.stack)
```
Success: 860 ms, faster than 20.43% ; 15.4 MB, less than 93.33%

---
### Other Solution
```Python
class MinStack(object):

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.items = []
        self.min = []

    def push(self, x):
        self.items.append(x)
        if not self.min or x <= self.min[-1]:
            self.min.append(x)

    def pop(self):
        if not self.items:
            return None
        
        item = self.items.pop()
        
        if item == self.min[-1]:
            self.min.pop() 
        
        return item 
    
    def top(self):
        if not self.items:
            return None
        return self.items[-1]

    def getMin(self):
        if not self.min: 
            return None
        return self.min[-1]
```
52 ms, faster than 86.81% ; 15.6 MB, less than 68.89% 
