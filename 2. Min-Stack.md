## Min Stack

## Problem:
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:
<ul>
  
<li>
  
  `MinStack()` initializes the stack object.
</li>
  
<li>
  
  `void push(int val)` pushes the element `val` onto the stack.
</li>
<li>
  
  `void pop()` removes the element on the top of the stack.
</li>
<li>
  
  `int top()` gets the top element of the stack.
</li>
<li>
  
  `int getMin()` retrieves the minimum element in the stack.
</li>
</ul>

You must implement a solution with `O(1)` time complexity for each function.

 
<p>
<h4>Example 1:</h4>

<h4>Input</h4>
["MinStack","push","push","push","getMin","pop","top","getMin"]
<br/>
[[],[-2],[0],[-3],[],[],[],[]]

<h4>Output</h4>
[null,null,null,null,-3,null,0,-2]

<h4>Explanation</h4>
MinStack minStack = new MinStack(); <br/>
minStack.push(-2);<br/>
minStack.push(0);<br/>
minStack.push(-3);<br/>
minStack.getMin(); // return -3<br/>
minStack.pop();<br/>
minStack.top();    // return 0<br/>
minStack.getMin(); // return -2<br/>
 

<h4>Constraints:</h4>
<em>
-231 <= val <= 231 - 1<br/>
Methods pop, top and getMin operations will always be called on non-empty stacks.<br/>
At most 3 * 104 calls will be made to push, pop, top, and getMin.<br/></em>
</p>



## Solution:
<p>
<h3>Undestanding The Problem:</h3>
We have to Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.
<br/>
<br/>
<h3>Steps:</h3>
<ul>
  <li>Take two stacks one is to store all values and another is to store min values</li>
  <li><strong>Push:</strong> Put the value in normal stack and if the minSTACK is empty then add the value to minSTACK as well. if not empty then add smaller one in both(val or min.top())</li>
  <li><strong>Pop:</strong> remove top() from normal stack as well as from minSTACk</li>
  <li><strong>Top:</strong> Return Normal stack top() element</li>
  <li><strong>getMin():</strong> return minSTACK top() element</li>
</ul>
</p>

<pre>
  <code>
    class MinStack {
    private:
      stack<int> st;
      stack<int> minST;

    public:
      MinStack() {}

      void push(int val) {
          if(minST.empty()){
              minST.push(val);
              st.push(val);
          }
          else {
              st.push(val);
              minST.push(min(val, minST.top()));
          }
      }

      void pop() {
          st.pop();
          minST.pop();
      }

      int top() {
          return st.top();
      }

      int getMin() {
          return minST.top();
      }
  };
  </code>
</pre>
