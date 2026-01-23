<h1>Problem:</h1>

<h3>Evaluate Reverse Polish Notation</h3>

You are given an array of strings tokens that represents an arithmetic expression in a <a href="https://en.wikipedia.org/wiki/Reverse_Polish_notation">Reverse Polish Notation</a>.
Evaluate the expression. Return an integer that represents the value of the expression.

<strong>Note</strong> that:

`The valid operators are '+', '-', '*', and '/'.`<br/>
`Each operand may be an integer or another expression.`<br/>
`The division between two integers always truncates toward zero.`<br/>
`There will not be any division by zero.`<br/>
`The input represents a valid arithmetic expression in a reverse polish notation.`<br/>
`The answer and all the intermediate calculations can be represented in a 32-bit integer.`<br/>

Example 1:

<em>Input: tokens = ["2","1","+","3","*"]<br/>
Output: 9<br/>
Explanation: ((2 + 1) * 3) = 9<br/>
Example 2:<br/>

Input: tokens = ["4","13","5","/","+"]<br/>
Output: 6<br/>
Explanation: (4 + (13 / 5)) = 6<br/>
Example 3:<br/>

Input: tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]<br/>
Output: 22<br/>
Explanation: ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22</em>

Constraints:
<ul>
<li>1 <= tokens.length <= 104</li>
<li>tokens[i] is either an operator: "+", "-", "*", or "/", or an integer in the range [-200, 200].</li>
</ul>


<h1>Solution:</h1>
<ul>
  <li>Create a Empty Stack.</li>
  <li>If any number appears store it in Stack.</li>
  <li>If any operator appears, take the last stored numbers and apply the operator and then store the result back.</li>
</ul>

<h3>Code:</h3>
<pre>
  <code>
    class Solution{
    public:
        int evalRPN(vector<string>& tokens) {
            stack<int> st;
            for(string c : tokens){
                if(c == "+"){
                    int a = st.top();
                    st.pop();
                    int b = st.top();
                    st.pop();
                    st.push(b + a);
                }
                else if(c == "-"){
                    int a = st.top();
                    st.pop();
                    int b = st.top();
                    st.pop();
                    st.push(b - a);
                }
                else if(c == "*"){
                    int a = st.top();
                    st.pop();
                    int b = st.top();
                    st.pop();
                    st.push(b * a);
                }
                else if(c == "/"){
                    int a = st.top();
                    st.pop();
                    int b = st.top();
                    st.pop();
                    st.push(b / a);
                }
                else{
                    //<strong>stoi</strong> is used to convert a string into an integer value
                    st.push(stoi(c));
                }
            }
            return st.top();
        }
    };
  </code>
</pre>


































