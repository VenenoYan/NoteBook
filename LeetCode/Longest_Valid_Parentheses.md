### Longest Valid Parentheses
Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.
```C++
For "(()", the longest valid parentheses substring is "()", which has length = 2.

Another example is ")()())", where the longest valid parentheses substring is "()()", length = 4. ```


### Stack method:

```C++
1.入栈：如s.push(x);
2.出栈:如 s.pop().注意：出栈操作只是删除栈顶的元素，并不返回该元素。
3.访问栈顶：如s.top();
4.判断栈空：如s.empty().当栈空时返回true。
5.访问栈中的元素个数，如s.size（）;```