# Stack-Related_Question-DSA--Stacl_All_question

Example:
'''
Input: s = “[()]{}{[()()]()}” 
Output: true
Explanation: All the brackets are well-formed


Input: s = “[(])” 
Output: false
Explanation: 1 and 4 brackets are not balanced because 
there is a closing ‘]’ before the closing ‘(‘

'''
LOGIC:  BAS 2 STEPS KA LOGIC HAI 
1. OPEN BRACKETS KO PUSH KARO
2. JAISE HI CLOSED BRACKET AAYE THEN COMPARE KARO STACK KI TOP SE MIL JAAYE TOH STACK SE POP KAR DO .


```c++
// C++ program to check for balanced brackets.
#include <bits/stdc++.h>
using namespace std;

// Function to check if brackets are balanced
bool ispar(const string& s) {  // Pass string by reference
  
    // Declare a stack to hold the previous brackets.
    stack<char> stk;
    for (int i = 0; i < s.length(); i++) {
        
        // Check if the character is an opening bracket
        if (s[i] == '(' || s[i] == '{' || s[i] == '[') {
            stk.push(s[i]); 
        } 
      
        else {
            // If it's a closing bracket, check if the stack is non-empty
            // and if the top of the stack is a matching opening bracket
            if (!stk.empty() && 
                ((stk.top() == '(' && s[i] == ')') ||
                 (stk.top() == '{' && s[i] == '}') ||
                 (stk.top() == '[' && s[i] == ']'))) {
                stk.pop(); // Pop the matching opening bracket
            }
            else {
                return false; // Unmatched closing bracket
            }
        }
    }
    
    // If stack is empty, return true (balanced), otherwise false
    return stk.empty();
}

int main() {
  
    string s = "{()}[]";

    // Function call
    if (ispar(s))
        cout << "true";
    else
        cout << "false";
    return 0;
}

```



# Evaluation of Postfix Expression

### Examples:

Input: str = “2 3 1 * + 9 -“
Output: -4
Explanation: If the expression is converted into an infix expression, it will be 2 + (3 * 1) – 9 = 5 – 9 = -4.


Input: str = “100 200 + 2 / 5 * 7 +”
Output: 757


YEH BHI 2 STEPS KA LOGIC HAI 
1. JAB TAK NUMBER DEKHE PUSH KAR DO STACK
2. JAISE HI SIGN DEKHE(*%-+) TOH STACK SE TOP KI TWO NUMBER NIKAL KAR OPERATON PERFORM KAR KI VAPS PUSH KAR DO STACK ME


```C++
// C++ program to evaluate value of a postfix expression
#include <bits/stdc++.h>
using namespace std;

// The main function that returns value 
// of a given postfix expression
int evaluatePostfix(string exp)
{
    // Create a stack of capacity equal to expression size
    stack<int> st;

    // Scan all characters one by one
    for (int i = 0; i < exp.size(); ++i) {
        
        // If the scanned character is an operand 
        // (number here), push it to the stack.
        if (isdigit(exp[i]))
            st.push(exp[i] - '0');

        // If the scanned character is an operator, 
        // pop two elements from stack apply the operator
        else {
            int val1 = st.top();
            st.pop();
            int val2 = st.top();
            st.pop();
            switch (exp[i]) {
            case '+':
                st.push(val2 + val1);
                break;
            case '-':
                st.push(val2 - val1);
                break;
            case '*':
                st.push(val2 * val1);
                break;
            case '/':
                st.push(val2 / val1);
                break;
            }
        }
    }
    return st.top();
}

// Driver code
int main()
{
    string exp = "231*+9-";
  
    // Function call
    cout << "postfix evaluation: " << evaluatePostfix(exp);
    return 0;
}

```


# Implement Stack using Queues (STACK BNAO QUESUE SE)

### STEPS:
Follow the below steps to implement the push(s, x) operation:  
Enqueue x to q2. 
One by one dequeue everything from q1 and enqueue to q2.  
Swap the queues of q1 and q2.

```C++
/* Program to implement a stack using
two queue */
#include <bits/stdc++.h>

using namespace std;

class Stack {
    // Two inbuilt queues
    queue<int> q1, q2;

public:
    void push(int x)
    {
        // Push x first in empty q2
        q2.push(x);

        // Push all the remaining
        // elements in q1 to q2.
        while (!q1.empty()) {
            q2.push(q1.front());
            q1.pop();
        }

        // swap the names of two queues
        queue<int> q = q1;
        q1 = q2;
        q2 = q;
    }

    void pop()
    {
        // if no elements are there in q1
        if (q1.empty())
            return;
        q1.pop();
    }

    int top()
    {
        if (q1.empty())
            return -1;
        return q1.front();
    }

    int size() { return q1.size(); }
};

// Driver code
int main()
{
    Stack s;
    s.push(1);
    s.push(2);
    s.push(3);

    cout << "current size: " << s.size() << endl;
    cout << s.top() << endl;
    s.pop();
    cout << s.top() << endl;
    s.pop();
    cout << s.top() << endl;

    cout << "current size: " << s.size() << endl;
    return 0;
}

```






